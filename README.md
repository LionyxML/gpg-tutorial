# GPG - Tutorial [Under Development]

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

### Generating a key pair

Several generators are provided, explore it with:

```
gpg --help | grep genera
```

The recommended way is to:

```
gpg --full-generate-key
```

Follow the instructions and voilà.

### Encrypting and decrypting

Remember, to encrypt you are always usig a public key, to list all available public keys in your system use

```
gpg -k
```

or

```
gpg --list-keys
```

or

```
gpg fingerprint
```

Let's encrypt a message to ourself using the key generated on our last step.

Create a file FILENAME with some text inside it.

Issue:

`gpg --recipient RECIPIENT_EMAIL --encrypt FILENAME`

Your encrypted file will be stored as FILENAME.gpg.

Remember, only the person with the PRIVATE key can decrypt it.

You can now delete your original message.

Try to open FILENAME.gpg and you will only see `garbage` as our encrypted file.

Now to decrypt your message:

`gpg --decrypt --output FILENAME FILENAME.gpg`

You have to provide the FILENAME to your output or it will be printed to standard
output (aka your terminal).

Tada! As you own the FILENAME.gpg private signature in your GPG "keychain", gpg
will automatically use it to decrypt.
