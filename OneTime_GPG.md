# One-Time GPG Commands

## Set Default Keyserver

Default location to send and receive public keys:

~~~
$ mkdir ~/.gnupg
$ chmod 0700 ~/.gnupg
$ echo "keyserver hkp://keys.gnupg.net" >> ~/.gnupg/gpg.conf
~~~

## Create GPG Keypair

Create a signing and encryption key:

~~~
$ gpg --expert --full-gen-key
~~~

## Add An Authentication Subkey

This can be used for SSH authentication:

~~~
$ gpg --expert --edit-key <YOUR_FINGERPRINT>
> addkey
>> 11
>> a
>> s
>> q
>> 1
>> 10y
> y
> y
> save
~~~

## Backup Public Key

Keep this some place safe:

~~~
$ gpg --armor --output ~/Desktop/public.asc --export <YOUR_FINGERPRINT>
~~~

# Publish Your Public Key

~~~
gpg --send-keys <YOUR_FINGERPRINT>>
~~~

## Backup Secret Keys

Keep this in two safe places:

~~~
$ gpg --armor --output ~/Desktop/secret.asc --export-secret-keys <YOUR_FINGERPRINT>
~~~

## Create/Backup Revocation Certificate

Keep this in two safe places:

~~~
$ gpg --armor --output ~/Desktop/revoke.asc --gen-revoke <YOUR_FINGERPRINT>
> y
> 0
>> Revocation certificate generated when key was created
>>
> y
~~~

\pagebreak

## Push Keys to Your OpenPGP Token

Backup your keys before you do this, or they will be unrecoverable:

~~~
$ gpg --edit-key <YOUR_FINGERPRINT>
> toggle
> keytocard
>> y
>> 1
> key 1
> keytocard
>> 2
> key 1
> key 2
> keytocard
>> 3
> save
~~~

## Customize OpenPGP Token

~~~
$ gpg --card-edit

gpg/card> admin
Admin commands are allowed

gpg/card> name
Cardholder's surname: <LASTNAME>
Cardholder's given name: <FIRSTNAME>

gpg/card> lang
Language preferences: en

gpg/card> sex
Sex ((M)ale, (F)emale or space): <M/F/ >

gpg/card> url
URL to retrieve public key: http://keys.gnupg.net/pks/lookup?op=get&search=0x<LAST_16_OF_FINGERPRINT>

gpg/card> login
Login data (account name): <COMMON_USERNAME>

gpg/card> forcesig

gpg/card> passwd

1 - change PIN
2 - unblock PIN
3 - change Admin PIN
4 - set the Reset Code
Q - quit

Your selection? 1
PIN changed.

1 - change PIN
2 - unblock PIN
3 - change Admin PIN
4 - set the Reset Code
Q - quit

Your selection? 4
Reset Code set.

1 - change PIN
2 - unblock PIN
3 - change Admin PIN
4 - set the Reset Code
Q - quit

Your selection? q

gpg/card> q
~~~

## Revoke Your Key

You would only run this command if:

1) Your key was stolen
2) You made a new key, and already signed it with your old one
3) Both 1 and 2

~~~
$ gpg --import revoke.asc
$ gpg --send-keys <YOUR_FINGERPRINT>>
~~~

