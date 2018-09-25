# Rare GPG Commands

## Use OpenPGP Token On a New Computer

Import your public key:

~~~
$ gpg --card-edit

gpg/card> fetch
gpg/card> q
~~~

Trust your key:

~~~
$ gpg --edit-key <YOUR_FINGERPRINT>
> trust
>> 5
>> y
> save
~~~

## Receive a Recipient's Public Key

Search For a Recipient's Public Key:

~~~
$ gpg --search-keys "<RECIPIENT_NAME>"
~~~

## Receive a Recipient's Public Key

Receive the key:

~~~
$ gpg --recv-keys <RECIPIENT_FINGERPRINT>
~~~

\pagebreak

## Sign a Public Key

Confirm their identity:

~~~
Ask for two forms of government photo ID
~~~

Confirm their fingerprint:

~~~
$ gpg --fingerprint <RECIPIENT_FINGERPRINT>
~~~

Sign the key:

~~~
$ gpg --sign-key --ask-cert-level <RECIPIENT_FINGERPRINT>
~~~

Export a signed/encrypted key, to mail back to the RECIPIENT:

~~~
$ gpg --armor --export <RECIPIENT_FINGERPRINT> | gpg --sign --encrypt -r <RECIPIENT_FINGERPRINT> --armor --output <RECIPIENT_FINGERPRINT>-signedBy-<YOUR_FINGERPRINT>.asc
~~~

## Receive a Signed Public Key

If someone sends you a signed public key, import it with this command:

~~~
gpg --decrypt <YOUR_FINGERPRINT>-signedBy-<RECIPIENT_FINGERPRINT>.asc | gpg --import
~~~

Publish your newly signed key:

~~~
gpg --send-keys <YOUR_FINGERPRINT>>
~~~

