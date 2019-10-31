+++
title = "IIT Delhi's fatal liability"
date = "2019-06-02"
description = "How secure is IIT Delhi from Man-in-the-middle attacks?"
categories = ["security"]
tags = ["adventure", "college", "mitm", "ssl"]
+++

How secure is IIT Delhi from Man-in-the-middle (MITM) attacks?

I'm publishing this 6 months after privately emailing IITD sysadmin
notifying them about a critical vulnerability, to have them fix
it properly.

### Facts

1. The institute asks its users to install a CA certificate issued by
itself to secure internal communications
1. The official download link for the CA certificate is hosted on an
unencrypted [plain HTTP page]
(http://www.cc.iitd.ac.in/CSC/index.php?option=com_content&view=article&id=53&Itemid=57)

### SSL certificates and MITM attacks

Before we continue, let's understand how SSL (CA) certificates work
([source](https://www.entrustdatacard.com/pages/ssl)).

1. A browser attempts to connect to a website (i.e. a web server)
secured with SSL. The browser requests that the web server identify
itself.
1. The web server sends the browser a copy of its SSL certificate.
1. The browser checks to see whether or not it trusts this SSL
certificate. If so, it sends a message to the web server.
1. The web server sends back a digitally signed acknowledgment to
start an SSL encrypted session.
1. Encrypted data is shared between the browser and the web server.

Focus on the 3rd step.

> ***The browser checks to see whether or not it trusts the SSL
> certificate.***

How?

Our computer comes with a small list of certificates pre-installed with
the operating system. They are called **Trusted Root Certificates** and
belong to organizations called **Certificate Authorities (CA)**. The
CAs have the authority to digitally sign a web server's certificate
implying to the world that they trust it. Thereby, the following
***chain of trust*** is formed ---

1. You trust the browser
1. Browser trusts the OS
1. OS trusts the CAs
1. CAs trust their root certificates
1. Any one of the root certificates trusts the web server's certificate

And this is how the browser ultimately trusts a web server. Looks
pretty simple, right? Yes, indeed.
However, this simplicity comes with a very interesting and challenging
possibility.

> ***What if one of those root certificates belong to a malicious
> actor?***

In that case, it's game over! All the communication between your
computer and **any other web server** is compromised, even if it
happens over HTTPS.

1. A malicious actor installs his bad certificate as a trusted root on
your computer.
1. You send a request to any web server. Cerficate exchange is about to
begin.
1. Malicious actor intercepts the request and pretends to be the said
web server and responds with his certificate. Since his certificate is
already present on your system, you trust it.
1. He also initiates another connection with the web server pretending
to be you.
1. All further communcations between you and the web server go through
him.

The malicious actor is sitting in the middle of you and the web server,
and neither of you knows about it. This is called a **Man in the middle
(MITM) attack** and it is one of the most dangerous ones out there.


### Back to IIT Delhi

Since the official link to download the CA certificate is published on
a [plain HTTP page]
(http://www.cc.iitd.ac.in/CSC/index.php?option=com_content&view=article&id=53&Itemid=57)
, anyone can inject a malicious link instead. The content of this page
can also be modified to show modified SHA1 & MD5 hashes. An uninformed
user will follow that link to download the malicious certificate and
install it as a Trusted Root on his machine **compromising all of his
future communications**.

### Vulnerability reporting

I sent the following email to the sysadmin sharing my concerns on
**Nov 29, 2018**.

<img
    class="post-image"
    src="/img/iitd-ca-vulnerability-email.png"
    alt="IIT Delhi CA vulnerability email"
>

### Response

I received no response. However, the relevant page was updated
accordingly on **Nov 30, 2018 (within a day)**, with the following
changes ---

- The download link was migrated to HTTPS
- SHA1 and MD5 fingerprint hashes added

<img
    class="post-image"
    src="/img/iitd-ca-vulnerability-patched.png"
    alt="IIT Delhi CA vulnerability patched"
>

### Existing issue

Although the certificate download link has been migrated to HTTPS, the
page on which it is hosted is still served on plain HTTP. A grave
vulnerability, [as explained above](#back-to-iit-delhi).

### Proposals

- All connections on the IITD public website should be served over
HTTPS. A free SSL certificate can be generated using [Certbot]
(https://certbot.eff.org/) from LetsEncrypt CA.
- All HTTP requests must automatically be redirected to HTTPS.
- The servers should also be set up with HSTS enabled, so that all of
the IITD resources are only available over HTTPS.
- Fingerprints --- Since [SHA1](https://shattered.io) and [MD5 aren't
secure]
(https://security.stackexchange.com/questions/19906/is-md5-considered-insecure)
, SHA2 should be used instead.
- Everyone in the IITD campus should be informed about the risks
associated with using an insecure connection.

### Conclusion

It is still fairly easy to do everlasting MITM attacks inside IIT Delhi
campus. Since most of the users have no idea about this issue, the
ensuing disaster would be enormous. IIT Delhi should follow other IITs
such as [Kanpur](https://iitk.ac.in/), [Madras](https://www.iitm.ac.in/)
, [Roorkee](https://www.iitr.ac.in/) who serve their pages over HTTPS.
