+++
title = "GnuPG setup"
date = "2019-12-26"
description = "Have you ever wondered about your identity on the internet?"
tags = ["tutorial"]
+++

Have you ever wondered about your identity on the internet? You can assume any alias, impersonate anyone, and be lost. It's a good thing, anonymity. However, there are times when you need to prove that you are real. For example, when communicating with your family members on the other side of the continent.

- How do you convince someone that you are in fact you
- How to share secrets securely over an insecure connection

Phil Zimmermann in 1991, attempted to solve these problems in his PGP (Pretty Good Privacy) suite. It ignited a revolution in the privacy world. Activists, journalists and tech enthusiats all over the world were encrypting and decryting their emails seamlessly. It was beautiful. A user only needed to take special care of all of his public/private keys. For a long time people were using it. Then GNU came with GnuPG in 1999. It allowed users to manage all of their private keys and all the public keys in a secure wallet.

GnuPG works very similar to Git, except it doesn't maintain versions. You can generate a key pair in your ~/.gnupg directory (wallet) and upload your public keys (repository) to a keyserver (GitHub). You tell others your key-id (repository link), and others import (clone) your public keys (repository) in their wallet. The secret keys (.env) are not uploaded online and only you know them.


GNU Privacy Guard is a neat solution to.

### Install

Get the latest GnuPG 2.x on your machine.

- Debian/Ubuntu ```sudo apt-get install gnupg2```
- Arch ```pacman -S gnupg```
- Fedora ```yum|dnf install gnupg```
- Nix ```nix-env -iA nixpkgs.gnupg```

Ensure you're always using gpg2 by aliasing it to gpg in ```~/.bashrc```

```alias gpg='gpg2'```

Now source it. ```source ~/.bashrc```

### Initialize

Create ```~/.gnupg``` using one of the following ---

- Backup: If you have a backup of .gnupg directory, copy it in ~/.gnupg
- New: If you do not have a backup, run ```gpg -k```

Now go check ~/.gnupg and its contents.

Copy gpg.conf and gpg-agent.conf from this directory to ~/.gnupg

### Generate keys

Create a new primary key gpg --expert --full-gen-key

- Use >=4096 bit RSA for primary key
- Use >=2048 bit RSA for sub keys

Edit keys using gpg --expert --edit-key <uid>

- Add new subkeys using addkey
- Change passwords using passwd
- Type help for more options

Create one subkey each for Authentication, Encryption, Signing.

List gpg keys by ---

- Public keys: gpg -k
- Private keys: gpg -K. If # appears after sec or ssb, then it means private key is not present for that key-id

Get keygrip of the keys gpg -k --with-keygrip <uid>

### SSH support

To use GnuPG for SSH, you must create an Authentication subkey, marked as [A].

Add the following to ~/.bashrc

export GPG_TTY=$(tty)
unset SSH_AGENT_PID
if [ "${gnupg_SSH_AUTH_SOCK_by:-0}" -ne $$ ]; then
  export SSH_AUTH_SOCK="${HOME}/.gnupg/S.gpg-agent.ssh"
fi
gpg-connect-agent /bye

Source ~/.bashrc source ~/.bashrc

To generate sshcontrol file, type ssh-add -l. Check sshcontrol file in ~/.gnupg

Add keygrip of your authentication subkey to sshcontrol file in a new line

Export SSH public key to be put on the servers' ~/.ssh/authorized_keys gpg --export-ssh-key <key-id>

You may now be able to SSH directly into the server.

### Backup

Before backing up, you must change passwords of the primary key & sub keys. Keep a strong >40 char pass phrase.

*** VERY IMPORTANT *** Backup the whole ~/.gnupg directory to a safe & secure place

After backup has been created, you must change passwords of the primary key & sub keys to a relatively easier >15 char pass phrase.

### Deleting secret keys

Now delete the unnecessary private keys. To delete the private keys ---

- Find out the of the keys using the above command
- Delete ~/.gnupg/private-keys-v1.d/.key





I do not know how GPG works (code, logic, database, etc). I just know how to make it work for general use. Let's begin.

Install gnupg2 (latest).
Alias gpg = gpg2

Init the ~/.gnupg directory using `gpg -k`.

chmod 600 for the files and 700 for directories.

Explain files in gnupg (private_keys.d, sshcontrol, pubring, gpg.cong, gpg-agent.conf, etc).

Explain public and private keys.

Generate a primary key. Explain RSA vs Elliptic and tell to choose RSA if you're a beginer.
Generate subkeys.

Explain backing up the private keys, and keygrips.

Explain keyservers.

Explain ssh setup.

GPG setup in Github/Gitlab.

### Debug gnupg

gpgconf

gpg-connect-agent





Why should I have different subkeys for Encryption, Authentication & Signing?
Encryption keys must be escrowed, Signing keys must not be escrowed.
