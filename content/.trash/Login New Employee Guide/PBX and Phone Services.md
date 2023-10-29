Complex phone systems are managed by a PBX. PBXs manage:
- Call routing
- Extension and phone setup
- Call recordings
- Time conditions for company hours and holidays.

Login Currently uses 3 different PBX systems. But are working on migrating them all to 1. (Kazoo Community Edition)
- Logix (Asterisk backend)
- Cloud Kazoo (2600hz backend) *2600hz is a company
- Kazoo Community edition (Login Backend, we manage our own pbx)

## Logix

Logix has a front end GUI and a command line interface

The top section of our PBX masterlist shows Logix clients. Just click on the customer's URL to be taken to the Logix GUI for that PBX

& Kazoo (See wiki for web links)

## 2600 Kazoo (Cloud)

- usr: logintech Pass: logintac+!

## Kazoo Community Edition(On Prem)

[https://portal.kz.login.bz](https://portal.kz.login.bz/ "https://portal.kz.login.bz/")

```
`david.thomas@login.bz
proven-murkiness-parakeet
Login-Kazoo-Services`
```

logix

- Each customer has own login website

Masterlist: [https://wiki.login.bz/index.php/PBX_Masterlist](https://wiki.login.bz/index.php/PBX_Masterlist "https://wiki.login.bz/index.php/PBX_Masterlist")

PBX: Changes

- Require 24 hours notice to make change to voicemail etc.

PBX: Voicemail

- Customer can delete messages one by one or we can delete them all

- Can set up voicemails to be delete after they have been emailed

PBX: CRD (Call Routing Diagram)

ATA (Analog Telephone Adapter)

- Connects phone line to ethernet

- Setup available on the wiki

Look up caller ID for a phone number (External)

#!/usr/bin/env bash

# lookup a CNAM
```
wget

--tries=1

--timeout=1.0

-0 $f@.out

'[[https://cnam.login.bz/cnam_api.php?provider=opencnam&number=](https://cnam.login.bz/cnam_api.php?provider=opencnam&number= "https://cnam.login.bz/cnam_api.php?provider=opencnam&number=")'

KaTeX parse error: Expected '}', got '&' at position 57: …ovider=opencnam&̲number=%27

KaTeX parse error: Expected '}', got '&' at position 57: …ovider=opencnam&̲number=%27

{0)]

echo >> $f@1.out

echo;

cat stef.out

exit:
```



```
#!/usr/bin/env bash
wget --tries=1 --timeout=1.0 -O ${@}.out \

'[[https://cnam.login.bz/cnam_api.php?provider=opencnam&number=](https://cnam.login.bz/cnam_api.php?provider=opencnam&number= "https://cnam.login.bz/cnam_api.php?provider=opencnam&number=")'

KaTeX parse error: Expected 'EOF', got '&' at position 58: …ovider=opencnam&̲number=%27

KaTeX parse error: Expected 'EOF', got '&' at position 58: …ovider=opencnam&̲number=%27

{@})

echo >> ${@}.out

echo; cat ${@}.out

exit;
```
be sure to chmod +x filename.sh, then, for example:

•/cnam-lookup.sh5204166400


### Bria Account Setup

go to: (clientname).cust.login.com or check here: [https://wiki.login.bz/index.php/PBX_Masterlist](https://wiki.login.bz/index.php/PBX_Masterlist "https://wiki.login.bz/index.php/PBX_Masterlist")

click Apps > Extensions

Create user in stretto (counterpath) [https://strettoadmin.cloudprovisioning.com/stretto/](https://strettoadmin.cloudprovisioning.com/stretto/ "https://strettoadmin.cloudprovisioning.com/stretto/") (need creds)

create password in diceware password generator [https://diceware.dmuth.org/](https://diceware.dmuth.org/ "https://diceware.dmuth.org/")

fill out username and email

create extentions in bria

ib stretto, add account > fill out username and password