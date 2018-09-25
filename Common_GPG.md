# Common GPG Commands

## Sign and Encrypt a Message For Email

Place your message in `<FILENAME>` and run the following command:

~~~
$ gpg --armor --encrypt --sign --recipient "<RECIPIENT_FINGERPRINT|RECIPIENT_EMAIL>" --output <FILENAME>.gpg <FILENAME>
~~~

## Decrypt, Verify, and Read a Message From Email

~~~
$ gpg --decrypt <FILENAME>.gpg
~~~

## Encrypt a Local File

~~~
$ gpg --encrypt --recipient "<RECIPIENT_FINGERPRINT|RECIPIENT_EMAIL>" --output <FILENAME>.gpg <FILENAME>
~~~

## Decrypt a Local File

~~~
$ gpg --decrypt --output <FILENAME> <FILENAME>.gpg
~~~

## Sign a Message For Email

~~~
$ gpg --armor --sign --recipient "<RECIPIENT_FINGERPRINT|RECIPIENT_EMAIL>" --output <FILENAME>.asc <FILENAME>
~~~

## Verify a Message From Email

~~~
$ gpg --verify <FILENAME>.asc
~~~
