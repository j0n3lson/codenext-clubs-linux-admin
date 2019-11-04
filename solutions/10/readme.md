
# Level 10

## <a name='Overview'></a>Overview

This level is a short one but introduces basic concepts of cryptography.

<!--NOTE: Do not edit table of content's. This is auto generated using an vscode-extension. -->
## <a name='TableofContents'></a>Table of Contents
<!-- vscode-markdown-toc -->
* [Overview](#Overview)
* [Table of Contents](#TableofContents)
* [Completing the Level Goal](#CompletingtheLevelGoal)
	* [Command Demo](#CommandDemo)
	* [ Command Breakdown](#CommandBreakdown)
* [Learning Byte: Cryptography](#LearningByte:Cryptography)
	* [What is Cryptography all about?](#WhatisCryptographyallabout)
	* [How `base64` encoding helps ensure message integrity](#Howbase64encodinghelpsensuremessageintegrity)
	* [Applications of Cryptography](#ApplicationsofCryptography)
* [Discussion Points](#DiscussionPoints)
* [Learn More](#LearnMore)

<!-- vscode-markdown-toc-config
	numbering=false
	autoSave=true
	/vscode-markdown-toc-config -->
<!-- /vscode-markdown-toc -->

## <a name='CompletingtheLevelGoal'></a>Completing the Level Goal

The level instructions tell us that the data is base64 encoded which means we
should look at the `base64` utility. Specifically the `base64`1 utility has
the `-d or --decode` flag which takes encoded data and decodes it.

### <a name='CommandDemo'></a>Command Demo

![Decoding text with the base64 command](base64.gif)

### <a name='CommandBreakdown'></a> Command Breakdown

You can't *decode* data that hasn't already been *encoded*:

```bash
# First let's create a file with some content"
tmp$ echo "there is some content" > test1.txt

# Try to decode it? No joy!
/tmp$ base64 -d test1.txt
��base64: invalid input
```

If the input data is different, the resulting *encoding* (or output) will be
different:

```bash
/tmp$ echo "here is some more content" > test2.txt
/tmp$ cat test1.txt
there is some content
/tmp$ cat test2.txt 
here is some more content

# With no flag, the base64 command just encodes the file contents.
# Notice the output string is different.
/tmp$ base64 test1.txt
dGhlcmUgaXMgc29tZSBjb250ZW50Cg==

/tmp$ base64 test2.txt
aGVyZSBpcyBzb21lIG1vcmUgY29udGVudAo=
```

It doesn't care if the file contains data or text, encoding will produce a
string either way. It also doesn't care about size, here we have an 8K data
file:

```bash

# Here's an 8KB file
jnelso@jnelso-glaptop2:/tmp$ du -h randomfile.txt 
8.0K	randomfile.txt

# It's a file that contains data
jnelso@jnelso-glaptop2:/tmp$ file randomfile.txt 
randomfile.txt: data

# It's full of random data
jnelso@jnelso-glaptop2:/tmp$ tail -n 1 randomfile.txt 
5dÛz�Ov�s������M	���_jnelso@jnelso-glaptop2:/tmp$ 

# And base64 doesn't really care :0
jnelso@jnelso-glaptop2:/tmp$ base64 randomfile.txt 
M73CJ+G2EwC1LYTh93+YCbysYVtOqQ9Eet4do3igk0RLxrRa9QV06pLKUNtLpAyejV4UBlwC2Fr3
ML+FBR/fOfMfyFaToe37Hh/WRq3jwE/kMikcdwWM7a18crQ7rQVY+WnpfRwPHmYUaF1sg0phYu+q
ncjCKRfaFlSbvw6gDrlWvrWS6f79hnifNw0YtmfjUkmWII6xPIgQHALyYaTOMoC7BlI9RXz1VIsk
2rTQDbPxSKw/Gm1YXu6C5hpOhW3XP6CH5ROVtsLqbscDG8dzbqdn78q8XrdTAV4mv0LDMXV5J/WN
vXaIPbsVROKlfAPTgIlOtCa7CJVOxUFaDkrOW9kMl+nQ5btnMkk7ClziKU2NwAIb9+wCWbLfViTZ
uQM1TxoWRNBX50LWbKcVYhlteYv6CdEIc7Kle0/PtjNp+jYwqpXvEvLd1DoQYeHyMd1m59WSOb5V
RtZDDF3ufsaA8pjTGvEv5xcJ3OD5mSZWS/404slp/ORw5j4zJb/8Oj5tBM/FUGI5+7yU28PblDpp
KcPQLYIg+7j3cEgBCLhWaI32kS/ANsL36FTV9tsu24fjhI/3B0fXnM1Dt+4kABXu8hB/MjcEPNMO
sGRl0eiYvRo61+X3YCEYPwzZxWOMSB6WP+SFtD/qMrjO+6qp5UeJn8HqGeKQTqwNTVQ330JQagXf
gSUWk2KDaUGXOPVzD/B7nCpoQbcwM4mnCmODzRFI5Pdw7p31KXGklVn0bTZB1shP81Txmbo6rZ25
N+8clOa43Z9kqV2TQChkxITw4LQsXIOu9BWh6EGZFL9Qmd2yJeV5hDablLbFW3AfLOuIh1aBF+bm
XICil8UIpSB10nm5U7gDIyiovvnL6e4VME8YczgQETnpaojIprrnay2vRqj7h4G6oiPZn1kQRfHO
JKynxriocJ70iMJIz7TbC9GkWbGBa0t+Wma4L1UF5w3dk0sDP6XExhzy/Q5EMmpjoFgnsofGbNbG
kHQCch4bECWcxVPnaiEczB7dvFZnF+jx7JOHBIFD9+zmvTwfR0lwoAIe4LMDCndsYy7lCstiFZdw
9R/cf7cb0qZTikYlTRsDUC6GPfFxZTL4FkShlr4l0q/F5eCCj4uawh8r0UF6BkVd8FD8cK9QJEwB
...
# The base64 encoding of this 8KB file is pretty long...
```

## <a name='LearningByte:Cryptography'></a>Learning Byte: Cryptography

### <a name='WhatisCryptographyallabout'></a>What is Cryptography all about?

You've probablly heard a lot lately about information security. On the news,
you may hear reports of company X getting hacked or social security numbers
being leaked. Cryptography is a method of protecting information and
communications using codes.

Generally, cryptography is focused on 4 key areas:

1. **Confidentiality**: If Bob sent a message to Alice then *only* Alice should
be able to read it.

2. **Integrity**: If Bob sends a message, Alice needs to be sure that someone
else didn't change the message (either when it was sent over the network or
when it was stored on a computer someplace).

3. **Non-Repudidation**: If Alice sends a message to Bob, she shouldn't be able
to claim later that it wasn't her who sent it.

4. **Authentication**: Both Bob and Alice should be able to confirm each other's
identity when talking to each other.

Confidentiality and Integrity and integrity are among the most important
topics in cyber security. A "secret" message that any one can read is *not*
very confidential and it's not very secure. Likewise, if random person can
change the message without anyone knowing, the message itself cannot be
trusted.

### <a name='Howbase64encodinghelpsensuremessageintegrity'></a>How `base64` encoding helps ensure message integrity

Encoding with base64 does not cover confidentiality since anyone that can run
the `base64` utility can also decode your message.

However, base64 encoding does help with integrity. At it's simplest level,
the base64 encoding algorithm looks at each chunk of data in the file and
computes a single printable character to represent each chunk. As you've seen
in the [command breakdown](#CommandBreakdown), if the data changes, so does
the encoding.

Alice can tell if a message from Bob has been messed with if Bob sends both
the origional message *and* the base64 encoding of the message. When Alice
get's the message, she base64 encodes the message and then compares the
string to the one Bob gave her. If they match, the message is the same,
otherwise, something changed.

### <a name='ApplicationsofCryptography'></a>Applications of Cryptography

Cryptographic solutions are literally everywhere. Here are just a few places
you'll see it show up:

* **Confidentiality with WIFI**: The data you send via WIFI is encrypted with
[AES](https://www.comparitech.com/blog/information-security/wpa2-aes-tkip/).

* **Non-Repudiation in Bitcoin**: ECDSA is used to [secure Bitcoin](https://en.bitcoin.it/wiki/Elliptic_Curve_Digital_Signature_Algorithm)

* **Authentication for Webservers**: It underlies [SSL (Secure Sockets Layer)](https://www.digicert.com/ssl/) which help secure web servers (e.g. http**s** vs http).

* **JWT for Web Auth and Integrity**: JWT or [JSON Web Tokens](https://auth0.com/learn/json-web-tokens/) are used to to secure web apps. Specifically, cryptographically signed JWTs are sent between clients and web servers. JWT is used in lots of places, most notabely Google's [OAuth2](https://developers.google.com/identity/protocols/OpenIDConnect) which lets you "Sign in with Google". (Fun fact: JWT uses base64 encoding)

## <a name='DiscussionPoints'></a>Discussion Points

Thinks about sending a text message to a friend:

* Is your text message Confidential? Why? Why not?
* Can you verify the Integrity of your text message?
* What could affect the integrity of the text message you sent?

## <a name='LearnMore'></a>Learn More

* [Search Security: Cryptography](https://searchsecurity.techtarget.com/definition/cryptography)
* [Base64 Encoding Algorithm](http://www.herongyang.com/Encoding/Base64-Encoding-Algorithm.html)
* [Alice and Bob](https://en.wikipedia.org/wiki/Alice_and_Bob)