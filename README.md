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

### Encrypting messages to OTHERS

Well, you can only encrypt messages to others having their PUBLIC key imported
to our GPG Keychain.

The person provides you with their `PUBLICKEY.key.gpg`.

First, we need to import it to your Keychain with:

```
gpg --import PUBLICKEY.key.gpg
```

You can see it now with `gpg -k`.

Now we encrypt our FILE to the other person with:

```
gpg --recipient NEW_PERSON_EMAIL --encrypt FILE
```

GPG may now complain that it is not sure the person is who you think it is.

Let's just ignore this for a while and proceed with 'y'.

There you have it, your FILE.gpg.

Well... let's try to decrypt it :)

```
gpg --decrypt --output FILE FILE.gpg
```

It will fail! Why? Well, you do not own the private key to that encrypted file.

So please, always remember that messages to others will be forever in "others
hand". If you delete your original file. Well well..

### Assigning others public keys

Remember I said not to worry and just say "y" to not being able to verify the
other person public key?

Now, let's worry.

I can `gpg -k` on my computer. And get in touch, let's say, by phone, or running
into the other person cubicle and ask him/her:
"This is your imported key here I my keychain, this number is above your name".

Him/her can run `gpg-k` on their machine and confirm it to you!

Of course it is just an example of how to do it. But sometimes you simple have
to "trust" the source of that public key. This is the reason why people often
publish it in their OWN websites, to provide credibility.

Well. So the public keyfile IS from that person for sure. It will be a pain in
the \*\*\* keep track of who you trust and who you doesn't.

For that, we may certify the key for gpg:

```
gpg --sign-key OTHER_PERSON_EMAIL
```

Well it will try do sign it with your own key. But you may have another key and
wanted to sign with that one... actually sign-key is part of the `--edit-key`.

You could also:

```
gpg --edit-key OTHER_PERSON_EMAIL
```

It is an interactive program... you could issue:

```
fpr
```

To get the fingerprint anc check if this is true to your recipient, and:

```
sign
check
save
```

Remember you use your PRIVATE key to sign.

If you have several, you can choose the one you're using to sign with:

`gpg --local-user YOUR_OTHER_EMAIL --sign file`

You can add more `--local-user` to sign it with multiple users.

With the other persons public key signed by you, you can now directly encrypt
without being prompted with the warning.

### Sending my public key to others

Well all gpg related stuff are usually under your `~/.gnupg` directory.

But we almost never want to mess with it directlly (and remember to back it up).

To provide others your public key export it with:

```
gpg --output my_public_key_filename.gpg --export USER_EMAIL
```

This will create a binary key file, if you want something more "copy/paste/view"
like, we can armor our key in ASCII with:

```
gpg --armor --export USER_EMAIL
```

And now you can copy/paste it in your own web site and even use it as part of
your e-mail signature.

### Frontends

Lots of frontends provide "user friendly" interfaces to gpg. You can try:
https://www.gpgfrontend.pub/
