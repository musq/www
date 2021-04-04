---
layout: post
title: GnuPG demystified
categories: Tutorial
---

What is your identity?

## Table of contents



## Introduction

Who are you? How do you prove to others that you are who you are.
Generally people know your face, recognize your voice or trust your
signature making ability. These methods work best for humans. What if
you had to identify yourself to a computer? The reason you might want to
do that is to establish secure communication with a person on the other
side of the world. You would require a computer and would need to trust
all the networking and communications infrastructure. This is
impossible! This is where PGP comes to play its role.

### Pretty Good Privacy

Pretty Good Privacy (PGP) is an encryption program that provides
cryptographic privacy and authentication for data communication. PGP is
used for signing, encrypting, and decrypting texts, e-mails, files,
directories, and whole disk partitions and to increase the security of
e-mail communications.

Phil Zimmermann created the first version of PGP encryption in 1991. The name, "Pretty Good Privacy" was inspired by the name of a grocery store, "Ralph's Pretty Good Grocery", featured in radio host Garrison Keillor's fictional town, Lake Wobegon.
Zimmermann had been a long-time anti-nuclear activist, and created PGP encryption so that similarly inclined people might securely use BBSs and securely store messages and files. No license was required for its non-commercial use. , and the complete source code was included with all copies.
PGP found its way onto the Internet and rapidly acquired a considerable following around the world. Users and supporters included dissidents in totalitarian countries, civil libertarians in other parts of the world, and the 'free communications' activists who called themselves cypherpunks.

https://en.wikipedia.org/wiki/Pretty_Good_Privacy

Shortly after its release, PGP encryption found its way outside the United States, and in February 1993 Zimmermann became the formal target of a criminal investigation by the US Government for "munitions export without a license". At the time, cryptosystems using keys larger than 40 bits were considered munitions within the definition of the US export regulations; PGP has never used keys smaller than 128 bits, so it qualified at that time. Penalties for violation, if found guilty, were substantial.
Zimmermann challenged these regulations in an imaginative way. He published the entire source code of PGP in a hardback book,[23] via MIT Press, which was distributed and sold widely. Anybody wishing to build their own copy of PGP could cut off the covers, separate the pages, and scan them using an OCR program (or conceivably enter it as a type-in program if OCR software was not available), creating a set of source code text files. One could then build the application using the freely available GNU Compiler Collection. PGP would thus be available anywhere in the world. The claimed principle was simple: export of munitions—guns, bombs, planes, and software—was (and remains) restricted; but the export of books is protected by the First Amendment. The question was never tested in court with respect to PGP.
After several years, the investigation of Zimmermann was closed without filing criminal charges against him or anyone else.

### Symmetric cryptography

A  cryptographic system that uses the same cryptographic keys for both
encryption of plaintext and decryption of ciphertext. The keys may be
identical or there may be a simple transformation to go between the two
keys.[1] The keys, in practice, represent a shared secret between two or
more parties that can be used to maintain a private information link.
e.g. AES, CAST5
Advantage - they are really fast.
Disadvantage - both parties have access to the same secret, making it
vulnerable

https://en.wikipedia.org/wiki/Symmetric-key_algorithm

### Public-key cryptography

Also known as asymmetric cryptography. uses pairs of keys: public keys which may be disseminated widely, and private keys which are known only to the owner. The generation of such keys depends on cryptographic algorithms based on mathematical problems to produce one-way functions. Effective security only requires keeping the private key private; the public key can be openly distributed without compromising security.[1]

https://en.wikipedia.org/wiki/Public-key_cryptography

In such a system, any person can encrypt a message using the receiver's public key, but that encrypted message can only be decrypted with the receiver's private key.

Robust authentication is also possible. A sender can combine a message with a private key to create a short digital signature on the message. Anyone with the sender's corresponding public key can combine the same message and the supposed digital signature associated with it to verify whether the signature was valid, i.e. made by the owner of the corresponding private key.
Public key algorithms are fundamental security ingredients in modern cryptosystems, applications and protocols assuring the confidentiality, authenticity and non-repudiability of electronic communications and data storage. They underpin various Internet standards, such as Transport Layer Security (TLS), S/MIME, PGP, and GPG. Some public key algorithms provide key distribution and secrecy (e.g., Diffie–Hellman key exchange), some provide digital signatures (e.g., Digital Signature Algorithm), and some provide both (e.g., RSA).

Advantage - easy to manage and distribute
Disadvantage - really slow and resource heavy in execution

#### RSA

RSA (Rivest–Shamir–Adleman) is one of the first public-key cryptosystems and is widely used for secure data transmission. In such a cryptosystem, the encryption key is public and it is different from the decryption key which is kept secret (private). In RSA, this asymmetry is based on the practical difficulty of the factorization of the product of two large prime numbers, the "factoring problem".


#### Elliptic curves

Elliptic-curve cryptography (ECC) is an approach to public-key cryptography based on the algebraic structure of elliptic curves over finite fields. ECC requires smaller keys compared to non-EC cryptography (based on plain Galois fields) to provide equivalent security.[1]
Discrete logarithms are quickly computable in a few special cases. However, no efficient method is known for computing them in general. Several important algorithms in public-key cryptography base their security on the assumption that the discrete logarithm problem over carefully chosen groups has no efficient solution.
NIST published several curves they believed to be secure enough, but
people got suspicious of how the coefficients for these curves were
chosen. So, those curves are now discouraged to use. Use ed25519 curve.

#### Digital signatures

(https://www.gnupg.org/gph/en/manual/x215.html  Some public-key ciphers[1] could be used to sign documents. The signer encrypts the document with his private key. Anybody wishing to check the signature and see the document simply uses the signer's public key to decrypt the document. This algorithm does satisfy the two properties needed from a good hash function, but in practice, this algorithm is too slow to be useful.

An alternative is to use hash functions designed to satisfy these two important properties. SHA and MD5 are examples of such algorithms. Using such an algorithm, a document is signed by hashing it, and the hash value is the signature. Another person can check the signature by also hashing their copy of the document and comparing the hash value they get with the hash value of the original document. If they match, it is almost certain that the documents are identical.)


## GnuPG basics

GNU Privacy Guard (GnuPG) is a tool GnuPG is a hybrid-encryption software program because it uses a combination of conventional symmetric-key cryptography for speed, and public-key cryptography for ease of secure key exchange, typically by using the recipient's public key to encrypt a session key which is used only once. This mode of operation is part of the OpenPGP standard and has been part of PGP from its first version.

GnuPG encrypts messages using asymmetric key pairs individually generated by GnuPG users. The resulting public keys may be exchanged with other users in a variety of ways, such as Internet key servers. They must always be exchanged carefully to prevent identity spoofing by corrupting public key ↔ "owner" identity correspondences. It is also possible to add a cryptographic digital signature to a message, so the message integrity and sender can be verified, if a particular correspondence relied upon has not been corrupted.

GnuPG also supports symmetric encryption algorithms. By default, GnuPG uses the AES symmetrical algorithm since version 2.1,[6] CAST5 was used in earlier versions. GnuPG does not use patented or otherwise restricted software or algorithms. Instead, GnuPG uses a variety of other, non-patented algorithms.[7]

### Basics

Public key - RSA, ElGamal, DSA
Cipher - 3DES, IDEA (since versions 1.4.13 and 2.0.20), CAST5, Blowfish, Twofish, AES-128, AES-192, AES-256, Camellia-128, -192 and -256 (since versions 1.4.10 and 2.0.12)
Hash - MD5, SHA-1, RIPEMD-160, SHA-256, SHA-384, SHA-512, SHA-224
Compression - Uncompressed, ZIP, ZLIB, BZIP2


- Keypairs (public + private)
-- Public keys are used for encryption and verifuing signatures
-- Private keys are used to decrypt and generate signatures
- Primary key
- Subkey (self signed by primary key)
- Roles - C (certify means signing other keys), A, E, S
- Key ID (short + long)
- fingerprint
- keygrip
- uid
- Certification vs. signing - ‘Signing’ is an action against arbitrary data. ‘Certification’ is the signing of another key. Ironically, the act of certifying a key is universally called “key signing”. Just embrace the contradiction. Self sign vs Cross sign
- Key certificate
- Key packet
- Trust vs Validity https://www.gnupg.org/gph/en/manual/x334.html#AEN384
-- Web of trust
- Key revocation - If disaster strikes, and you need to revoke the subkey for whatever reason, do the following:
Multiple Subkeys per Machine vs. One Single Subkey for All Machines
One might be tempted to have one subkey per machine so that you only need to exchange the potentially compromised subkey of that machine. In case of a single subkey used on all machines, it needs to be exchanged on all machines in case of a compromising.

But this only works for signing subkeys. If you have multiple encryption subkeys, gpg is said to encrypt only for the most recent encryption subkey and not for all known and not revoked encryption subkeys.
- Keyserver
- Signign parties

### Subkeys

https://wiki.debian.org/Subkeys

Subkeys make key management easier. The master key pair is quite important: it is the best proof of your identity online, at least for Debian, and if you lose it, you'll need to start building your reputation from scratch. If anyone else gets access to your private master key or its private subkey, they can make everyone believe they're you: they can upload packages in your name, vote in your name, and do pretty much anything else you can do. This can be very harmful for Debian. You might dislike it as well. So you should keep all your private keys safe.

Subkeys make this easier: you already have an automatically created encryption subkey and you create another subkey for signing, and you keep those on your main computer. You publish the subkeys on the normal keyservers, and everyone else will use them instead of the master keys for encrypting messages or verifying your message signatures. Likewise, you will use the subkeys for decrypting and signing messages.

You will need to use the master keys only in exceptional circumstances, namely when you want to modify your own or someone else's key. More specifically, you need the master private key:

when you sign someone else's key or revoke an existing signature,
when you add a new UID or mark an existing UID as primary (When you have multiple user IDs, one of the user IDs is made the primary user ID. Passwords and Keys will attach the primary user ID by default with your key information, while encrypting or signing, unless you explicitly choose another user ID instead. https://help.gnome.org/users/seahorse/stable/pgp-userid-primary.html.en),

when you create a new subkey,
when you revoke an existing UID or subkey,
when you change the preferences (e.g., with setpref) on a UID,

when you change the expiration date on your master key or any of its subkey, or
when you revoke or generate a revocation certificate for the complete key.
(Because each of these operation is done by adding a new self- or revocation signatures from the private master key.)

So in case your subkey gets stolen while your master key remains safe, you can revoke the compromised subkey and replace it with a new subkey without having to rebuild your reputation and without reducing reputation of other people's keys signed with your master key.

> gpg automatically uses the newest subkey to sign/encrypt.

## GPG configurations

> GnuPG makes key management an ease. You can manage it just like you
> manage code in Git and GitHub.


# Client specific options

--default-key name
If this option is not used, the default key is the first key found in the secret keyring. If there is no secret key available for any of the specified values, GnuPG will not emit an error message but continue as if this option wasn’t given.

--default-recipient-self
Use the default key as default recipient if option --recipient is not used and don’t ask if this is a valid one.

-v, --verbose
Give more information during processing. If used twice, the input data is listed in detail.

-q, --quiet
Try to be as quiet as possible.

--batch
--no-batch
Use batch mode. Never ask, do not allow interactive commands. --no-batch disables this option.
It is highly recommended to use this option along with the options --status-fd and --with-colons for any unattended use of gpg.

--no-tty
Make sure that the TTY (terminal) is never used for any output. This option is needed in some cases because GnuPG sometimes prints warnings to the TTY even if --batch is used.

--yes
Assume "yes" on most questions.

--no
Assume "no" on most questions.

--list-options parameters
This is a space or comma delimited string that gives options used when listing keys and signatures (that is, --list-keys, --check-signatures, --list-public-keys, --list-secret-keys, and the --edit-key functions). Options can be prepended with a no- (after the two dashes) to give the opposite meaning. Common important options are:

    show-usage
    This is a list of letters indicating the allowed usage for a key (E=encryption, S=signing, C=certification, A=authentication). Defaults to yes.

    show-uid-validity
    Display the calculated validity of user IDs during key listings. Defaults to yes.

    show-unusable-uids
    Show revoked and expired user IDs in key listings. Defaults to no.

    show-unusable-subkeys
    Show revoked and expired subkeys in key listings. Defaults to no.

    show-sig-expire
    Show signature expiration dates (if any) during --check-signatures listings. Defaults to no.

--verify-options parameters
This is a space or comma delimited string that gives options used when verifying signatures. Options can be prepended with a ‘no-’ to give the opposite meaning. Common important options are:

    show-policy-urls
    Show policy URLs in the signature being verified. Defaults to yes.

    show-keyserver-urls
    Show any preferred keyserver URL in the signature being verified. Defaults to yes.

    show-uid-validity
    Display the calculated validity of the user IDs on the key that issued the signature. Defaults to yes.

    show-unusable-uids
    Show revoked and expired user IDs during signature verification. Defaults to no.

    show-primary-uid-only
    Show only the primary user ID during signature verification. That is all the AKA lines as well as photo Ids are not shown with the signature verification status.

--keyring file
Add file to the current list of keyrings. If file begins with a tilde and a slash, these are replaced by the $HOME directory. If the filename does not contain a slash, it is assumed to be in the GnuPG home directory ("~/.gnupg" if --homedir or $GNUPGHOME is not used).

Note that this adds a keyring to the current list. If the intent is to use the specified keyring alone, use --keyring along with --no-default-keyring.

If the option --no-keyring has been used no keyrings will be used at all.

--primary-keyring file
Designate file as the primary public keyring. This means that newly imported keys (via --import or keyserver --recv-from) will go to this keyring.

--trustdb-name file
Use file instead of the default trustdb. If file begins with a tilde and a slash, these are replaced by the $HOME directory. If the filename does not contain a slash, it is assumed to be in the GnuPG home directory (~/.gnupg if --homedir or $GNUPGHOME is not used).

--homedir dir
Set the name of the home directory to dir. If this option is not used, the home directory defaults to ~/.gnupg. It is only recognized when given on the command line. It also overrides any home directory stated through the environment variable GNUPGHOME or (on Windows systems) by means of the Registry entry HKCU\Software\GNU\GnuPG:HomeDir.

--display-charset name
Set the name of the native character set. This is used to convert some informational strings like user IDs to the proper UTF-8 encoding. Note that this has nothing to do with the character set of data to be encrypted or signed; GnuPG does not recode user-supplied data. If this option is not used, the default character set is determined from the current locale. A verbosity level of 3 shows the chosen set. Valid values for name are:

    iso-8859-1
    This is the Latin 1 set.

    iso-8859-2
    The Latin 2 set.

    iso-8859-15
    This is currently an alias for the Latin 1 set.

    koi8-r
    The usual Russian set (RFC-1489).

    utf-8
    Bypass all translations and assume that the OS uses native UTF-8 encoding.

--options file
Read options from file and do not try to read them from the default options file in the homedir (see --homedir). This option is ignored if used in an options file.

--no-options
Shortcut for --options /dev/null. This option is detected before an attempt to open an option file. Using this option will also prevent the creation of a ~/.gnupg homedir.

--trust-model {pgp|classic|tofu|tofu+pgp|direct|always|auto}
Set what trust model GnuPG should follow. The models are:

    pgp
    This is the Web of Trust combined with trust signatures as used in PGP 5.x and later. This is the default trust model when creating a new trust database.

    classic
    This is the standard Web of Trust as introduced by PGP 2.

    tofu
    TOFU stands for Trust On First Use. This is just like the confirmation message when you connect to a ssh server for the first time. In this trust model, the first time a key is seen, it is memorized. If later another key with a user id with the same email address is seen, both keys are marked as suspect. In that case, the next time either is used, a warning is displayed describing the conflict, why it might have occurred (either the user generated a new key and failed to cross sign the old and new keys, the key is forgery, or a man-in-the-middle attack is being attempted), and the user is prompted to manually confirm the validity of the key in question.

    Because a potential attacker is able to control the email address and thereby circumvent the conflict detection algorithm by using an email address that is similar in appearance to a trusted email address, whenever a message is verified, statistics about the number of messages signed with the key are shown. In this way, a user can easily identify attacks using fake keys for regular correspondents.

    When compared with the Web of Trust, TOFU offers significantly weaker security guarantees. In particular, TOFU only helps ensure consistency (that is, that the binding between a key and email address doesn’t change). A major advantage of TOFU is that it requires little maintenance to use correctly. To use the web of trust properly, you need to actively sign keys and mark users as trusted introducers. This is a time-consuming process and anecdotal evidence suggests that even security-conscious users rarely take the time to do this thoroughly and instead rely on an ad-hoc TOFU process.

    In the TOFU model, policies are associated with bindings between keys and email addresses (which are extracted from user ids and normalized). There are five policies, which can be set manually using the --tofu-policy option. The default policy can be set using the --tofu-default-policy option.

    The TOFU policies are: auto, good, unknown, bad and ask. The auto policy is used by default (unless overridden by --tofu-default-policy) and marks a binding as marginally trusted. The good, unknown and bad policies mark a binding as fully trusted, as having unknown trust or as having trust never, respectively. The unknown policy is useful for just using TOFU to detect conflicts, but to never assign positive trust to a binding. The final policy, ask prompts the user to indicate the binding’s trust. If batch mode is enabled (or input is inappropriate in the context), then the user is not prompted and the undefined trust level is returned.

    tofu+pgp
    This trust model combines TOFU with the Web of Trust. This is done by computing the trust level for each model and then taking the maximum trust level where the trust levels are ordered as follows: unknown < undefined < marginal < fully < ultimate < expired < never.

    By setting --tofu-default-policy=unknown, this model can be used to implement the web of trust with TOFU’s conflict detection algorithm, but without its assignment of positive trust values, which some security-conscious users don’t like.

    direct
    Key validity is set directly by the user and not calculated via the Web of Trust. This model is solely based on the key and does not distinguish user IDs. Note that when changing to another trust model the trust values assigned to a key are transformed into ownertrust values, which also indicate how you trust the owner of the key to sign other keys.

    always
    Skip key validation and assume that used keys are always fully valid. You generally won’t use this unless you are using some external validation scheme. This option also suppresses the "[uncertain]" tag printed with signature checks when there is no evidence that the user ID is bound to the key. Note that this trust model still does not allow the use of expired, revoked, or disabled keys.

    auto
    Select the trust model depending on whatever the internal trust database says. This is the default model if such a database already exists. Note that a tofu trust model is not considered here and must be enabled explicitly.

--tofu-default-policy {auto|good|unknown|bad|ask}
The default TOFU policy (defaults to auto). For more information about the meaning of this option, see trust-model-tofu.

--completes-needed n
Number of completely trusted users to introduce a new key signer (defaults to 1).

--marginals-needed n
Number of marginally trusted users to introduce a new key signer (defaults to 3)

--max-cert-depth n
Maximum depth of a certification chain (default is 5).

--keyid-format {none|short|0xshort|long|0xlong}
Select how to display key IDs. "none" does not show the key ID at all but shows the fingerprint in a separate line. "short" is the traditional 8-character key ID. "long" is the more accurate (but less convenient) 16-character key ID. Add an "0x" to either to include an "0x" at the beginning of the key ID, as in 0x99242560. Note that this option is ignored if the option --with-colons is used.

--auto-check-trustdb
--no-auto-check-trustdb
If GnuPG feels that its information about the Web of Trust has to be updated, it automatically runs the --check-trustdb command internally. This may be a time consuming process. --no-auto-check-trustdb disables this option.

--agent-program file
Specify an agent program to be used for secret key operations. The default value is determined by running gpgconf with the option --list-dirs. Note that the pipe symbol (|) is used for a regression test suite hack and may thus not be used in the file name.

--dirmngr-program file
Specify a dirmngr program to be used for keyserver access. The default value is /usr/local/bin/dirmngr.

--no-autostart
Do not start the gpg-agent or the dirmngr if it has not yet been started and its service is required. This option is mostly useful on machines where the connection to gpg-agent has been redirected to another machines. If dirmngr is required on the remote machine, it may be started manually using gpgconf --launch dirmngr.

--lock-once
Lock the databases the first time a lock is requested and do not release the lock until the process terminates.

--lock-multiple
Release the locks every time a lock is no longer needed. Use this to override a previous --lock-once from a config file.

--limit-card-insert-tries n
With n greater than 0 the number of prompts asking to insert a smartcard gets limited to N-1. Thus with a value of 1 gpg won’t at all ask to insert a card if none has been inserted at startup. This option is useful in the configuration file in case an application does not know about the smartcard support and waits ad infinitum for an inserted card.

--no-random-seed-file
GnuPG uses a file to store its internal random pool over invocations. This makes random generation faster; however sometimes write operations are not desired. This option can be used to achieve that with the cost of slower random generation.

--no-greeting
Suppress the initial copyright message.

--no-secmem-warning
Suppress the warning about "using insecure memory".

--no-permission-warning
Suppress the warning about unsafe file and home directory (--homedir) permissions. Note that the permission checks that GnuPG performs are not intended to be authoritative, but rather they simply warn about certain common permission problems. Do not assume that the lack of a warning means that your system is secure.

Note that the warning for unsafe --homedir permissions cannot be suppressed in the gpg.conf file, as this would allow an attacker to place an unsafe gpg.conf file in place, and use this file to suppress warnings about itself. The --homedir permissions warning may only be suppressed on the command line.

--require-cross-certification
--no-require-cross-certification
When verifying a signature made from a subkey, ensure that the cross certification "back signature" on the subkey is present and valid. This protects against a subtle attack against subkeys that can sign. Defaults to --require-cross-certification for gpg.

--expert
--no-expert
Allow the user to do certain nonsensical or "silly" things like signing an expired or revoked key, or certain potentially incompatible things like generating unusual key types. This also disables certain warning messages about potentially incompatible actions. As the name implies, this option is for experts only. If you don’t fully understand the implications of what it allows you to do, leave this off. --no-expert disables this option.


# OpenPGP protocol specific options

-t, --textmode
--no-textmode
Treat input files as text and store them in the OpenPGP canonical text form with standard "CRLF" line endings. This also sets the necessary flags to inform the recipient that the encrypted or signed data is text and may need its line endings converted back to whatever the local system uses. This option is useful when communicating between two platforms that have different line ending conventions (UNIX-like to Mac, Mac to Windows, etc). --no-textmode disables this option, and is the default.

--personal-cipher-preferences string
Set the list of personal cipher preferences to string. Use gpg --version to get a list of available algorithms, and use none to set no preference at all. This allows the user to safely override the algorithm chosen by the recipient key preferences, as GPG will only select an algorithm that is usable by all recipients. The most highly ranked cipher in this list is also used for the --symmetric encryption command.

--personal-digest-preferences string
Set the list of personal digest preferences to string. Use gpg --version to get a list of available algorithms, and use none to set no preference at all. This allows the user to safely override the algorithm chosen by the recipient key preferences, as GPG will only select an algorithm that is usable by all recipients. The most highly ranked digest algorithm in this list is also used when signing without encryption (e.g. --clear-sign or --sign).

--personal-compress-preferences string
Set the list of personal compression preferences to string. Use gpg --version to get a list of available algorithms, and use none to set no preference at all. This allows the user to safely override the algorithm chosen by the recipient key preferences, as GPG will only select an algorithm that is usable by all recipients. The most highly ranked compression algorithm in this list is also used when there are no recipient keys to consider (e.g. --symmetric).

--s2k-cipher-algo name
Use name as the cipher algorithm for symmetric encryption with a passphrase if --personal-cipher-preferences and --cipher-algo are not given. The default is AES-128.

--s2k-digest-algo name
Use name as the digest algorithm used to mangle the passphrases for symmetric encryption. The default is SHA-1.

# Key related options

--recipient name
-r
Encrypt for user id name. If this option or --hidden-recipient is not specified, GnuPG asks for the user-id unless --default-recipient is given.

--hidden-recipient name
-R
Encrypt for user ID name, but hide the key ID of this user’s key. This option helps to hide the receiver of the message and is a limited countermeasure against traffic analysis. If this option or --recipient is not specified, GnuPG asks for the user ID unless --default-recipient is given.

--encrypt-to name
Same as --recipient but this one is intended for use in the options file and may be used with your own user-id as an "encrypt-to-self". These keys are only used when there are other recipients given either by use of --recipient or by the asked user id. No trust checking is performed for these user ids and even disabled keys can be used.

--group {name=value}
Sets up a named group, which is similar to aliases in email programs. Any time the group name is a recipient (-r or --recipient), it will be expanded to the values specified. Multiple groups with the same name are automatically merged into a single group.

The values are key IDs or fingerprints, but any key description is accepted. Note that a value with spaces in it will be treated as two different values. Note also there is only one level of expansion — you cannot make an group that points to another group. When used from the command line, it may be necessary to quote the argument to this option to prevent the shell from treating it as multiple arguments.

# Input and Output

--armor
-a
Create ASCII armored output. The default is to create the binary OpenPGP format.

--no-armor
Assume the input data is not in ASCII armored format.

--output file
-o file
Write output to file. To write to stdout use - as the filename.

--with-colons
Print key listings delimited by colons. Note that the output will be encoded in UTF-8 regardless of any --display-charset setting. This format is useful when GnuPG is called from scripts and other programs as it is easily machine parsed. The details of this format are documented in the file doc/DETAILS, which is included in the GnuPG source distribution.

--with-fingerprint
Same as the command --fingerprint but changes only the format of the output and may be used together with another command.

--with-subkey-fingerprint
If a fingerprint is printed for the primary key, this option forces printing of the fingerprint for all subkeys. This could also be achieved by using the --with-fingerprint twice but by using this option along with keyid-format "none" a compact fingerprint is printed.

--with-icao-spelling
Print the ICAO spelling of the fingerprint in addition to the hex digits.

--with-keygrip
Include the keygrip in the key listings. In --with-colons mode this is implicitly enable for secret keys.


# Doing things one doesn't usually do

-n
--dry-run
Don’t make any changes (this is not completely implemented).

--list-only
Changes the behaviour of some commands. This is like --dry-run but different in some cases. The semantic of this option may be extended in the future. Currently it only skips the actual decryption pass and therefore enables a fast listing of the encryption keys.

-i
--interactive
Prompt before overwriting any files.

--debug-level level
Select the debug level for investigating problems. level may be a numeric value or by a keyword:

none
No debugging at all. A value of less than 1 may be used instead of the keyword.

basic
Some basic debug messages. A value between 1 and 2 may be used instead of the keyword.

advanced
More verbose debug messages. A value between 3 and 5 may be used instead of the keyword.

expert
Even more detailed messages. A value between 6 and 8 may be used instead of the keyword.

guru
All of the debug messages you can get. A value greater than 8 may be used instead of the keyword. The creation of hash tracing files is only enabled if the keyword is used.

How these messages are mapped to the actual debugging flags is not specified and may change with newer releases of this program. They are however carefully selected to best aid in debugging.

--debug flags
Set debugging flags. All flags are or-ed and flags may be given in C syntax (e.g. 0x0042) or as a comma separated list of flag names. To get a list of all supported flags the single word "help" can be used.

--debug-all
Set all useful debugging flags.

--enable-progress-filter
Enable certain PROGRESS status outputs. This option allows frontends to display a progress indicator while gpg is processing larger files. There is a slight performance overhead using it.

--status-fd n
Write special status strings to the file descriptor n. See the file DETAILS in the documentation for a listing of them.

--status-file file
Same as --status-fd, except the status data is written to file file.

--logger-fd n
Write log output to file descriptor n and not to STDERR.

--log-file file
--logger-file file
Same as --logger-fd, except the logger data is written to file file. Use socket:// to log to a socket. Note that in this version of gpg the option has only an effect if --batch is also used.

--attribute-fd n
Write attribute subpackets to the file descriptor n. This is most useful for use with --status-fd, since the status messages are needed to separate out the various subpackets from the stream delivered to the file descriptor.

--attribute-file file
Same as --attribute-fd, except the attribute data is written to file file.

--comment string
--no-comments
Use string as a comment string in cleartext signatures and ASCII armored messages or keys (see --armor). The default behavior is not to use a comment string. --comment may be repeated multiple times to get multiple comment strings. --no-comments removes all comments. It is a good idea to keep the length of a single comment below 60 characters to avoid problems with mail programs wrapping such lines. Note that comment lines, like all other header lines, are not protected by the signature.

--emit-version
--no-emit-version
Force inclusion of the version string in ASCII armored output. If given once only the name of the program and the major number is emitted, given twice the minor is also emitted, given thrice the micro is added, and given four times an operating system identification is also emitted. --no-emit-version (default) disables the version line.

--set-filename string
Use string as the filename which is stored inside messages. This overrides the default, which is to use the actual filename of the file being encrypted. Using the empty string for string effectively removes the filename from the output.

--for-your-eyes-only
--no-for-your-eyes-only
Set the ‘for your eyes only’ flag in the message. This causes GnuPG to refuse to save the file unless the --output option is given, and PGP to use a "secure viewer" with a claimed Tempest-resistant font to display the message. This option overrides --set-filename. --no-for-your-eyes-only disables this option.

--use-embedded-filename
--no-use-embedded-filename
Try to create a file with a name as embedded in the data. This can be a dangerous option as it enables overwriting files. Defaults to no. Note that the option --output overrides this option.

--cert-digest-algo name
Use name as the message digest algorithm used when signing a key. Running the program with the command --version yields a list of supported algorithms. Be aware that if you choose an algorithm that GnuPG supports but other OpenPGP implementations do not, then some users will not be able to use the key signatures you make, or quite possibly your entire key.

--disable-cipher-algo name
Never allow the use of name as cipher algorithm. The given name will not be checked so that a later loaded algorithm will still get disabled.

--disable-pubkey-algo name
Never allow the use of name as public key algorithm. The given name will not be checked so that a later loaded algorithm will still get disabled.

--throw-keyids
--no-throw-keyids
Do not put the recipient key IDs into encrypted messages. This helps to hide the receivers of the message and is a limited countermeasure against traffic analysis.2 On the receiving side, it may slow down the decryption process because all available secret keys must be tried. --no-throw-keyids disables this option. This option is essentially the same as using --hidden-recipient for all recipients.

--passphrase-repeat n
Specify how many times gpg will request a new passphrase be repeated. This is useful for helping memorize a passphrase. Defaults to 1 repetition.

--passphrase-fd n
Read the passphrase from file descriptor n. Only the first line will be read from file descriptor n. If you use 0 for n, the passphrase will be read from STDIN. This can only be used if only one passphrase is supplied.

Note that since Version 2.0 this passphrase is only used if the option --batch has also been given. Since Version 2.1 the --pinentry-mode also needs to be set to loopback.

--passphrase-file file
Read the passphrase from file file. Only the first line will be read from file file. This can only be used if only one passphrase is supplied. Obviously, a passphrase stored in a file is of questionable security if other users can read this file. Don’t use this option if you can avoid it.

Note that since Version 2.0 this passphrase is only used if the option --batch has also been given. Since Version 2.1 the --pinentry-mode also needs to be set to loopback.

--passphrase string
Use string as the passphrase. This can only be used if only one passphrase is supplied. Obviously, this is of very questionable security on a multi-user system. Don’t use this option if you can avoid it.

Note that since Version 2.0 this passphrase is only used if the option --batch has also been given. Since Version 2.1 the --pinentry-mode also needs to be set to loopback.

--pinentry-mode mode
Set the pinentry mode to mode. Allowed values for mode are:

    default
    Use the default of the agent, which is ask.

    ask
    Force the use of the Pinentry.

    cancel
    Emulate use of Pinentry’s cancel button.

    error
    Return a Pinentry error (“No Pinentry”).

    loopback
    Redirect Pinentry queries to the caller. Note that in contrast to Pinentry the user is not prompted again if he enters a bad password.

--command-fd n
This is a replacement for the deprecated shared-memory IPC mode. If this option is enabled, user input on questions is not expected from the TTY but from the given file descriptor. It should be used together with --status-fd. See the file doc/DETAILS in the source distribution for details on how to use it.

--command-file file
Same as --command-fd, except the commands are read out of file file

--no-default-keyring
Do not add the default keyrings to the list of keyrings. Note that GnuPG will not operate without any keyrings, so if you use this option and do not provide alternate keyrings via --keyring or --secret-keyring, then GnuPG will still use the default public or secret keyrings.

--no-keyring
Do not use any keyring at all. This overrides the default and all options which specify keyrings.

--skip-verify
Skip the signature verification step. This may be used to make the decryption faster if the signature verification is not needed.

--with-key-data
Print key listings delimited by colons (like --with-colons) and print the public key data.

--list-signatures
--list-sigs
Same as --list-keys, but the signatures are listed too. This command has the same effect as using --list-keys with --with-sig-list. Note that in contrast to --check-signatures the key signatures are not verified. This command can be used to create a list of signing keys missing in the local keyring; for example:

      gpg --list-sigs --with-colons USERID | \
        awk -F: '$1=="sig" && $2=="?" {if($13){print $13}else{print $5}}'
--fast-list-mode
Changes the output of the list commands to work faster; this is achieved by leaving some parts empty. Some applications don’t need the user ID and the trust information given in the listings. By using this options they can get a faster listing. The exact behaviour of this option may change in future versions. If you are missing some information, don’t use this option.

--show-session-key
Display the session key used for one message. See --override-session-key for the counterpart of this option.

We think that Key Escrow is a Bad Thing; however the user should have the freedom to decide whether to go to prison or to reveal the content of one specific message without compromising all messages ever encrypted for one secret key.

You can also use this option if you receive an encrypted message which is abusive or offensive, to prove to the administrators of the messaging system that the ciphertext transmitted corresponds to an inappropriate plaintext so they can take action against the offending user.

--override-session-key string
--override-session-key-fd fd
Don’t use the public key but the session key string respective the session key taken from the first line read from file descriptor fd. The format of this string is the same as the one printed by --show-session-key. This option is normally not used but comes handy in case someone forces you to reveal the content of an encrypted message; using this option you can do this without handing out the secret key. Note that using --override-session-key may reveal the session key to all local users via the global process table. Often it is useful to combine this option with --no-keyring.

--ask-sig-expire
--no-ask-sig-expire
When making a data signature, prompt for an expiration time. If this option is not specified, the expiration time set via --default-sig-expire is used. --no-ask-sig-expire disables this option.

--default-sig-expire
The default expiration time to use for signature expiration. Valid values are "0" for no expiration, a number followed by the letter d (for days), w (for weeks), m (for months), or y (for years) (for example "2m" for two months, or "5y" for five years), or an absolute date in the form YYYY-MM-DD. Defaults to "0".

--ask-cert-expire
--no-ask-cert-expire
When making a key signature, prompt for an expiration time. If this option is not specified, the expiration time set via --default-cert-expire is used. --no-ask-cert-expire disables this option.

--default-cert-expire
The default expiration time to use for key signature expiration. Valid values are "0" for no expiration, a number followed by the letter d (for days), w (for weeks), m (for months), or y (for years) (for example "2m" for two months, or "5y" for five years), or an absolute date in the form YYYY-MM-DD. Defaults to "0".

--list-config
Display various internal configuration parameters of GnuPG. This option is intended for external programs that call GnuPG to perform tasks, and is thus not generally useful. See the file doc/DETAILS in the source distribution for the details of which configuration items may be listed. --list-config is only usable with --with-colons set.


## Dirmngr configuration

--options file
Reads configuration from file instead of from the default per-user configuration file. The default configuration file is named dirmngr.conf and expected in the home directory.

--homedir dir
Set the name of the home directory to dir. This option is only effective when used on the command line. The default is the directory named .gnupg directly below the home directory of the user unless the environment variable GNUPGHOME has been set in which case its value will be used. Many kinds of data are stored within this directory.

-v
--verbose
Outputs additional information while running. You can increase the verbosity by giving several verbose commands to DIRMNGR, such as -vv.

--log-file file
Append all logging output to file. This is very helpful in seeing what the agent actually does. Use socket:// to log to socket.

--debug-level level
Select the debug level for investigating problems. level may be a numeric value or by a keyword:

    none
    No debugging at all. A value of less than 1 may be used instead of the keyword.

    basic
    Some basic debug messages. A value between 1 and 2 may be used instead of the keyword.

    advanced
    More verbose debug messages. A value between 3 and 5 may be used instead of the keyword.

    expert
    Even more detailed messages. A value between 6 and 8 may be used instead of the keyword.

    guru
    All of the debug messages you can get. A value greater than 8 may be used instead of the keyword. The creation of hash tracing files is only enabled if the keyword is used.

How these messages are mapped to the actual debugging flags is not specified and may change with newer releases of this program. They are however carefully selected to best aid in debugging.

--debug flags
Set debugging flags. This option is only useful for debugging and its behavior may change with a new release. All flags are or-ed and may be given in C syntax (e.g. 0x0042) or as a comma separated list of flag names. To get a list of all supported flags the single word "help" can be used.

--debug-all
Same as --debug=0xffffffff

--keyserver name
Use name as your keyserver. This is the server that gpg communicates with to receive keys, send keys, and search for keys. The format of the name is a URI: ‘scheme:[//]keyservername[:port]’ The scheme is the type of keyserver: "hkp" for the HTTP (or compatible) keyservers, "ldap" for the LDAP keyservers, or "mailto" for the Graff email keyserver. Note that your particular installation of GnuPG may have other keyserver types available as well. Keyserver schemes are case-insensitive. After the keyserver name, optional keyserver configuration options may be provided. These are the same as the --keyserver-options of gpg, but apply only to this particular keyserver.

Most keyservers synchronize with each other, so there is generally no need to send keys to more than one server. The keyserver hkp://keys.gnupg.net uses round robin DNS to give a different keyserver each time you use it.

If exactly two keyservers are configured and only one is a Tor hidden service (.onion), Dirmngr selects the keyserver to use depending on whether Tor is locally running or not. The check for a running Tor is done for each new connection.

If no keyserver is explicitly configured, dirmngr will use the built-in default of hkps://hkps.pool.sks-keyservers.net.












## GPG commmands

### Install GPG

Install gpg2 (for ubuntu)
sudo apt-get install gnupg2

Alias
alias gpg='gpg2'

source ~/.bashrc

# Create ~/.gnupg directory
gpg -k


# Generate new keys
gpg --expert --full-gen-key
# You must set up gpg.conf and gpg-agent.conf before generating a new
key

# Edit existing keys
gpg --expert --edit-key <uid>

https://www.gnupg.org/documentation/manuals/gnupg/Specify-a-User-ID.html
- keyid
- uid (=Heinrich Heine <heinrichh@uni-duesseldorf.de>)
- email (<heinrichh@uni-duesseldorf.de>)
- partial email (@heinrichh)
- keygrip (&D75F22C3F86E355877348498CDC92BD21010A480)
- substring [default] (Heine or \*Heine)

# Add subkeys each for Authentication, Encryption and Sigining


# List public keys
gpg -k

# List private keys
gpg -K
If # appears after sec or ssb, then it means private key is not present for that key-id

# Get keygrip
gpg -k --with-keygrip <uid>

# Export public
gpg -a --export <uid>

# Export private
gpg -a --export-secret-keys <uid>


### Use gpg-agent for SSH

### Use OpenKeychain in android

## GPG Internals

- gpg
- gpg-agent
- pinentry
- dirmngr
- keyring

### Packet anatomy

Describe what's inside a packet

## Beware

Don't use key ids to identify keys (use user ids and fingerprints)
https://debian-administration.org/users/dkg/weblog/105

Use phone to verify fingerprints (use icao spelling)

Don't use keyservers
https://gist.github.com/rjhansen/67ab921ffb4084c865b3618d6955275f
A keyserver might be able to detect your social circle if you use
keyservers. Doing refresh-keys tells the keyserver about all the keys
coming from an ip, so they might be able to deduce who you talk to.

Don't encrypt and sign using the same key
https://serverfault.com/a/399366

Never keep your primary secret key on your computer lying around with a
weak password.

# Future of OpenPGP

What's new in RFC4880bis?










Key signing parties:
https://www.debian.org/events/keysigning
People should only sign a key under at least two conditions:
1. The key owner convinces the signer that the identity in the UID is indeed their own identity by whatever evidence the signer is willing to accept as convincing. Usually this means the key owner must present a government issued ID with a picture and information that match up with the key owner. (Some signers know that government issued ID's are easily forged and that the trustability of the issuing authorities is often suspect and so they may require additional and/or alternative evidence of identity).
2. The key owner verifies that the fingerprint and the length of the key about to be signed is indeed their own.

```bash
gpg --keyserver keyring.debian.org --recv-keys 0xDEADBEEF
gpg --edit-key 0xDEADBEEF
In GnuPG select all uids to sign with uid n, where n is the number of the uid shown in the menu. You can also press enter to sign all the uids.
To sign a key, enter sign. You will then be shown the fingerprint and length of they key which you have to compare with the one you've got from the person you met.
When asked for the level of certification, choose "casual".

Quit GnuPG with save
gpg --list-sigs 0xDEADBEEF
You should see your own name and fingerprint (in short form) in the output.
gpg --export --armor 0xDEADBEEF > someguys.key

If someone signs your key in this manner, you can add it to the Debian keyring by doing:
gpg --import --import-options merge-only mysigned.key
gpg --keyserver keyring.debian.org --send-keys <your key id>
```

Beware:
It is nice to get more signatures on ones key, and it is tempting to cut a few corners along the way. But having trustworthy signatures is more important than having many signatures, so it's very important that we keep the keysigning process as pure as we can. Signing someone else's key is an endorsement that you have first-hand evidence of the keyholder's identity. If you sign it when you don't really mean it, the Web of Trust can no longer be trusted.

TOFU example:

d522d0c 8 weeks ago feat(gitignore): Add python rules to global list (Ashish Ranjan)
b47f180 9 weeks ago fix(shell): Revert Ignore commands beginning with spaces from history (Ashish Ranjan)
~/projects/dotfiles/src (dev *+% u+1) $ g sh d522d0c
The email address "ashish@tug.ro" is associated with 2 keys!  Please
indicate whether this email address should be associated with key
B53024D7CE16B789CE40591B041335F0C6976479 or whether you think someone is
impersonating "ashish@tug.ro".

This key's user IDs:
  Ashish Ranjan (tug.ro/key-old) <ashish@tug.ro> (policy: auto)
  Ashish Ranjan <ashish72@pm.me> (policy: auto)
  Ashish Ranjan (yourbro) <ashish28ranjan@protonmail.com> (policy: auto)

Statistics for keys with the email address "ashish@tug.ro":
  B530 24D7 CE16 B789 CE40  591B 0413 35F0 C697 6479 (this key):
    Encrypted 0 messages.
    Messages verified over the past 1 day: 1.
  2486 D81A 43BE 694B DC05  5C21 418B D98E 013B 49A9 (policy: auto):
    Encrypted 0 messages.
    Messages verified over the past 1 day: 1.

Normally, an email address is associated with a single key.  However,
people sometimes generate a new key if their key is too old or they think
it might be compromised.  Alternatively, a new key may indicate a
man-in-the-middle attack!  Before accepting this association, you should
talk to or call the person to make sure this new key is legitimate.

(G)ood, (A)ccept once, (U)nknown, (R)eject once, (B)ad?





https://www.cs.bham.ac.uk/~mdr/teaching/modules/security/lectures/PGP.html

gpg automatically uses the newest subkey to sign/encrypt.
If you want to force use a subkey, append ! to force using the specified
primary or secondary key and not to try and calculate which primary or
secondary key to use.


- Define identity

- public key cryptography (assymetric)
- symetric cryptography
- GnuPG uses hybrid ciphers (https://www.gnupg.org/gph/en/manual/x209.html)
- post quantum cryptography
- Digital signatures (https://www.gnupg.org/gph/en/manual/x215.html  Some public-key ciphers[1] could be used to sign documents. The signer encrypts the document with his private key. Anybody wishing to check the signature and see the document simply uses the signer's public key to decrypt the document. This algorithm does satisfy the two properties needed from a good hash function, but in practice, this algorithm is too slow to be useful.

An alternative is to use hash functions designed to satisfy these two important properties. SHA and MD5 are examples of such algorithms. Using such an algorithm, a document is signed by hashing it, and the hash value is the signature. Another person can check the signature by also hashing their copy of the document and comparing the hash value they get with the hash value of the original document. If they match, it is almost certain that the documents are identical.)
- history of PGP, RSA, and Phil Zimmerman
- Primary key vs Subkey
- Public keys are used for encryption and verifuing signatures
- Private keys are used to decrypt and generate signatures
- Key ID, fingerprint, keygrip, uid
- Certification vs. signing - ‘Signing’ is an action against arbitrary data. ‘Certification’ is the signing of another key. Ironically, the act of certifying a key is universally called “key signing”. Just embrace the contradiction.
- RSA vs ECC
- ephemeral keys
- encryption keys must be escrowed, signing keys must not be escrowed

Desribe GnuPG components

Trust vs Validity
https://www.gnupg.org/gph/en/manual/x334.html#AEN384

Desribe subkeys
https://wiki.debian.org/Subkeys

Subkeys make key management easier. The master key pair is quite important: it is the best proof of your identity online, at least for Debian, and if you lose it, you'll need to start building your reputation from scratch. If anyone else gets access to your private master key or its private subkey, they can make everyone believe they're you: they can upload packages in your name, vote in your name, and do pretty much anything else you can do. This can be very harmful for Debian. You might dislike it as well. So you should keep all your private keys safe.

Subkeys make this easier: you already have an automatically created encryption subkey and you create another subkey for signing, and you keep those on your main computer. You publish the subkeys on the normal keyservers, and everyone else will use them instead of the master keys for encrypting messages or verifying your message signatures. Likewise, you will use the subkeys for decrypting and signing messages.

You will need to use the master keys only in exceptional circumstances, namely when you want to modify your own or someone else's key. More specifically, you need the master private key:

when you sign someone else's key or revoke an existing signature,
when you add a new UID or mark an existing UID as primary (When you have multiple user IDs, one of the user IDs is made the primary user ID. Passwords and Keys will attach the primary user ID by default with your key information, while encrypting or signing, unless you explicitly choose another user ID instead. https://help.gnome.org/users/seahorse/stable/pgp-userid-primary.html.en),

when you create a new subkey,
when you revoke an existing UID or subkey,
when you change the preferences (e.g., with setpref) on a UID,

when you change the expiration date on your master key or any of its subkey, or
when you revoke or generate a revocation certificate for the complete key.
(Because each of these operation is done by adding a new self- or revocation signatures from the private master key.)

So in case your subkey gets stolen while your master key remains safe, you can revoke the compromised subkey and replace it with a new subkey without having to rebuild your reputation and without reducing reputation of other people's keys signed with your master key.


- generate revocation certificate
- import/export public/private key
- encrypt/decrypt (https://www.gnupg.org/gph/en/manual/x110.html)
- make/verify signatures (https://www.gnupg.org/gph/en/manual/x135.html)
- web of trust (trust levels)
- key expiration time
- certify other keys
- distribute keys using keyservers (mention keyserver poisioning)
- export-ownertrust/import-ownertrust - update-trustdb


- GnuPG commands
gpg -k
gpg -K
gpg --armor --export ashish
gpg --expert --edit-keys ashish passwd


If you are switching between X and tty often you may want to run
gpg-connect-agent updatestartuptty /bye > /dev/null
to set it to the current environment. e.g. to get pinentry-curses to
work, run this command


Create GPG keys (use gpg2, i.e. GnuPG 2.1 or later)
- Before creating a new key, you must set gpg.conf like
personal-digest-preferences, etc.
- Create a primary key with no expiry
- Add uid
- Set primary uid in case you added multiple uids
- Create subkeys with expiry of 6months or 1 year, not more than that
- Remove private key by deleting their corresponding keygrip.key


Key revocation
If disaster strikes, and you need to revoke the subkey for whatever reason, do the following:

1. Mount the encrypted USB drive.
1. export GNUPGHOME=/media/yourdrive
1. gpg --edit-key YOURMASTERKEYID
1. At the gpg> prompt, list the keys (list), select the unwanted one (key 123), and generate a revocation certificate (revkey), then save.
1. Send the updated key to the keyservers as above.

### Multiple Subkeys per Machine vs. One Single Subkey for All Machines
One might be tempted to have one subkey per machine so that you only need to exchange the potentially compromised subkey of that machine. In case of a single subkey used on all machines, it needs to be exchanged on all machines in case of a compromising.

But this only works for signing subkeys. If you have multiple encryption subkeys, gpg is said to encrypt only for the most recent encryption subkey and not for all known and not revoked encryption subkeys.

Set up Remote Forward of GPG keys through SSH
https://wiki.gnupg.org/AgentForwarding

Backup ~/.gnupg
Do not backup ~/.gnupg/random_seed
Set up a strong password of your keys
gpg --expert --edit-keys ashish passwd
Perform backup
umask 077; tar -cf $HOME/gnupg-backup.tar -C $HOME .gnupg

When you need to use the master keys, mount the encrypted USB drive, and set the GNUPGHOME environment variable:

export GNUPGHOME=/media/something
gpg -K
or use the --homedir command-line argument:

gpg --homedir=/media/something -K
The latter command should now list your private key with sec and not sec#.


How to manage your keys
https://www.gnupg.org/documentation/manuals/gnupg/OpenPGP-Key-Management.html


Signing subkey cross certification
https://gnupg.org/faq/subkey-cross-certify.html


Use GPG as SSH Agent
https://incenp.org/notes/2015/gnupg-for-ssh-authentication.html


Don't use key ids to identify keys (use user ids and fingerprints)
https://debian-administration.org/users/dkg/weblog/105

Use phone to verify fingerprints (use icao spelling)

Don't use keyservers
https://gist.github.com/rjhansen/67ab921ffb4084c865b3618d6955275f

Don't encrypt and sign using the same key
https://serverfault.com/a/399366

Never keep your primary secret key on your computer lying around with a
weak password.

Key signing parties:
https://www.debian.org/events/keysigning
People should only sign a key under at least two conditions:
1. The key owner convinces the signer that the identity in the UID is indeed their own identity by whatever evidence the signer is willing to accept as convincing. Usually this means the key owner must present a government issued ID with a picture and information that match up with the key owner. (Some signers know that government issued ID's are easily forged and that the trustability of the issuing authorities is often suspect and so they may require additional and/or alternative evidence of identity).
2. The key owner verifies that the fingerprint and the length of the key about to be signed is indeed their own.

```bash
gpg --keyserver keyring.debian.org --recv-keys 0xDEADBEEF
gpg --edit-key 0xDEADBEEF
In GnuPG select all uids to sign with uid n, where n is the number of the uid shown in the menu. You can also press enter to sign all the uids.
To sign a key, enter sign. You will then be shown the fingerprint and length of they key which you have to compare with the one you've got from the person you met.
When asked for the level of certification, choose "casual".

Quit GnuPG with save
gpg --list-sigs 0xDEADBEEF
You should see your own name and fingerprint (in short form) in the output.
gpg --export --armor 0xDEADBEEF > someguys.key

If someone signs your key in this manner, you can add it to the Debian keyring by doing:
gpg --import --import-options merge-only mysigned.key
gpg --keyserver keyring.debian.org --send-keys <your key id>
```

Beware:
It is nice to get more signatures on ones key, and it is tempting to cut a few corners along the way. But having trustworthy signatures is more important than having many signatures, so it's very important that we keep the keysigning process as pure as we can. Signing someone else's key is an endorsement that you have first-hand evidence of the keyholder's identity. If you sign it when you don't really mean it, the Web of Trust can no longer be trusted.


OpenPGP vs Signal:
1. Time - Signal is real time communication (so is able to offer forward
   secrecy). OpenPGP is for archived communications as well.
1. Space - Signal is centralized, OpenPGP is decentralized. Data at rest
   vs data in motion
1. Anonymity - Signal requires phone numbers, so strongly tied identity

Explain signing.
Give other examples of how to explain public key cryptography.
Talk about threat modeling. What are you trying to protect? From
whom? What resources does the adversary have?

OpenPGP consists of three main parts. First, OpenPGP specifies a collection of cryptographic algorithms for encrypting and decrypting data,
generating and verifying digital signatures, and deriving keys from passwords (so-called key derivication functions or KDFs). These are built on
top of more basic cryptographic building blocks like SHA-1 (a hash algorithm), AES (a symmetric cipher), and RSA (an asymmetric cipher, which
is also known as a public-key algorithm). For the most part, the specification does not define these algorithms; it simply says which algorithms
should be used where and how to use them. Second, OpenPGP defines a
packet-based message format. This format is used not only for exchanging encrypted messages, but also for transferring keys and key meta-data.
Finally, OpenPGP includes functionality to help manage keys. This functionality includes the ability to revoke a key, and to sign keys.

In particular, because data at rest may be accessed asynchronously with respect
to the encryption, there is no possibility to negociate parameters on the fly
When you access the data 10 years later, your implementation needs
to support that now old encryption algorithm; there is no way to go back
in time and say to your former self, "could you use this implementation
instead?"
An additional consequence is that upgrading the cryptography becomes very difficult. It is not possible to completely deprecate old algorithms, because old messages (like our backup) still need to be decrypted

Forward secrecy works
by mutating the key material in time. This scheme is fine if you never need
to decrypt old messages (as is typically the case for data transferred via
HTTPS, say), but doesn’t work at all for data at rest. Perfect secrecy becomes even more complicated when a user has multiple devices, and all devices should be able to decrypt all messages. OpenPGP doesn’t require that those devices somehow synchronize their
state after the private key is copied. But, some type of synchronization is
necessary for forward secrecy

OpenPGP is designed to allow unbuffered message processing. First, it allows an
OpenPGP implementation to run on memory constrainted systems while
being confident that the implementation can in practice process arbitrarily
large messages. Second, it ensures that streaming tools can be used, e.g.,
something like ... | gpg -e -r key | ssh .... Finally, this property helps avoid some denial of service attacks, which might otherwise be
possible by crafting a malicious message

An OpenPGP message is basically a sequences of packets. OpenPGP defines 17 different packet types that are used to not only encrypt and sign
messages, but also to transfer keys and key signatures or certifications,
which are used in the web of trust.

OpenPGP is a hybrid cryptosystem. A hybrid cryptosystem first encrypts
data using a symmetric encryption algorithm like AES with a random socalled session key, and then encrypts the session key using the recipient’s
public key. The result is stored in a so-call public-key encrypted session key
(PK-ESK) packet.
2 reasons to do this. First, public key encryption is thousands of times slower than symmetric encryption. Second, it is not unusual to encrypt a message to multiple recipients.
if law enforcement forces you to reveal the encryption key for
some messages, it is sufficient to provide the session keys for decrypting the
subpoenaed messages
Finally, using hybrid encryption, it is possible to encrypt to both public
keys and passwords. To encrypt a message using a password, OpenPGP
specifies a key derivation function (S2K), which is used to generate a symmetric key. (This is saved in a so-called symmetric-key encrypted session key
(SK-ESK) packet.) OpenPGP allows the symmetric key to be used directly
as the session key, but it can just as well be used to encrypt a session key.
In practice, this is primarily interesting to ensure that the sender is able to
later decrypt the contents of the message by also encrypting the session key
to her public key

4.4.2 Algorithm
Encryption in OpenPGP is a more or less standard hybrid encryption
scheme:
1. A random session key is generated.
2. For each recipient, the OpenPGP implementation encrypts the session key using the recipient’s public key, and emits a public-key encrypted session key (PK-ESK) packet.
3. If the data should be encrypted using a password, the same thing is
done, but instead of emitted a PK-ESK packet, a session-key encrypted
session key (SK-ESK) packet is emitted.
4. Encrypt the actual data using the session key.
OpenPGP supports multiple symmetric encryption algorithms. To determine which one to use, the OpenPGP implementation selects one from
the intersection of the recipients’ preferred algorithms. This information
isn’t negotiated in real time with the recipients (even when this might
in theory be possible), but is stored alongside the recipient’s public key
(specifically, in a user ID’s self-signature). Typically, this is just a list of
the algorithms that the OpenPGP implementation that generated the key
supports at the time the key was created, but it can be updated to reflect
changes in the implementation, and may be customized by expert users.
Since all implementations are required to at least support TripleDES, and it
appears implicitly at the end of the list, the intersection is never empty

**List down all the allowed tag values, ctb values, etc. in OpenPGP**

Explain page 25-30 in advanced intro to gnupg pdf
page 32-35 for signatures.

https://davesteele.github.io/gpg/2014/09/20/anatomy-of-a-gpg-key/
https://davesteele.github.io/gpg/2015/08/01/intermediate-gpg/

https://wiki.debian.org/Subkeys
https://cheatsheets.chaospixel.com/gnupg/
https://wiki.archlinux.org/index.php/GnuPG
https://rudd-o.com/linux-and-free-software/protecting-your-private-master-key-in-gnupg-2-1-and-later
https://blogs.gentoo.org/mgorny/2018/05/12/on-openpgp-gnupg-key-management/
https://incenp.org/notes/2015/gnupg-for-ssh-authentication.html
https://eklitzke.org/using-gpg-agent-effectively
https://devhints.io/gnupg

https://begriffs.com/posts/2016-11-05-advanced-intro-gnupg.html
https://gnupg.org/ftp/people/neal/an-advanced-introduction-to-gnupg/an-advanced-introduction-to-gnupg.pdf
https://evil32.com/
https://blog.cryptographyengineering.com/2014/08/13/whats-matter-with-pgp/
https://medium.com/@mshelton/how-to-lose-friends-and-anger-journalists-with-pgp-b5b6d078a315
https://arstechnica.com/information-technology/2016/12/op-ed-im-giving-up-on-pgp/
https://arstechnica.com/information-technology/2016/12/signal-does-not-replace-pgp/
https://debian-administration.org/users/dkg/weblog/104
https://jilliancyork.com/2017/08/03/i-dont-want-to-give-out-my-phone-number-a-gendered-security-issue/
