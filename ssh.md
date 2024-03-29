## SSH

### Working with SSH Keys

You should probably by using something more modern and performant than RSA (and don't use DSA
anymore).  The e-mail address is just a comment and is optional, but can help you keep track of
which keys you use for what.  And of course you should always protect your keys with a passphrase.

`ssh-keygen -t ed25519 -C "your_email@example.com"`

If you need RSA:

`ssh-keygen -t rsa -b 4096 -C "your_email@example.com"`

If you need to change (or add) a passphrase:

`ssh-keygen -p -f <private_key>`

If you want to see the type of key and its length:

`ssh-keygen -l -f key.pub`

You can always regenerage the public key from any private key if needed:

`ssh-keygen -y -f .ssh/private_key > .ssh/key.pub`

### Rsync with SSH

This trick can be useful for silent rsync in a cron job.  Storing the SSH options in a variable can
be useful if you need to do some ad hoc rsync commands from the CLI, but also makes a shell script
somewhat more readable.
```
SSH="ssh -o StrictHostKeyChecking=no -o UserKnownHostsFile=/dev/null"
rsync -az --delete -e "$SSH" server01.example.com:/var/data/ /var/data/
```
