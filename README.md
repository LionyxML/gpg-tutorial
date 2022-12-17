# GPG - Tutorial

### Official Docs

- https://gnupg.org

### Install

GnuPG is most probabily already installed if you're under Linux or MacOS. To check
it go to your terminal and issue this command:

```
gpg --version
```

If not installed (ie: this command returns a not found like error message),
check the official docs for installation.

### The concept

Basically you will generate a `pair of keys`:

- Private (also known as secret key)
- Public

These keys will be used in this manner:

1. To encrypt a file:

```
secretMessage = encrypt(originalMessage, publicKey)
```

2. To decrypt a file:

```
originalMessage = decrypt(message, privateKey)
```

As you can see, you have do keep your privateKey private to your self. It means,
under your possession and not share it with anyone. This ensures you're the only
`real and true READER` of messages. See it. Everyone can use your public key to
encrypt data and be an official `ISSUER` to you. But you're the only one who
will be able do decrypt it.

You can and should send your publicKey to everyone you want to be able to
write you encrypt messages.

There's even servers dedicated to host public keys. A very famous one is:

- https://keys.openpgp.org

Another important concept is that you're not restricted to ONE pair of keys, but
you can generate as many as you wish. You could for example, have sets of
distinct pairs for:

- Your private e-mail
- Your file with other passwords
- Your work e-mail
- Credentials to a repository
- Another repository
- Access to your crytpo wallet

And so on...
