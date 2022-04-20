# Luckypost specification

This document is a work-in-progress, it is missing information and some of its
information may be changed as development progresses.

The "lucky" prefix is named after the creator's late pet cat of the
same name, the name was chosen as an attempt to make Lucky
posthumously famous. Because of this it is a name that carries a
sentiment that cannot be replicated by big tech companies.


## Example

The following is an example of a short discussing consisting of two luckyposts:

```
ae3mzuya4u57o2nw7 2022-01-05 19:14:12 en.icecream alice
<Peppermint is the best icecream flavor
@agmxl5djhznzshm5eaha4co252zf4zqhbb3g2dqvv2enag542qxsq
!a16+37ctvYjf75E5M1JzGr27D4cbzZ7dPh7qoroRhYVN5Xd4iyNNoV1AnW7qWFTbAemwcY8qcAcYvmU8T5JGDGM1VFin

ahbb3g2dqvv2ena 2022-01-05 19:14:12 en.icecream bob
"hokeypokey.jpg" 640x480 143,385 al5djhznzshm5eaha4
^ae3mzuya4u57o2nw7
>Peppermint is the best icecream flavor
<Nope, it's hokey pokey!
@agmxl5djhznzshm5eaha4co252zf4zqhbb3g2dqvv2enag542qxsq
!a16+4Rq3SEd9KSjfLvvwFEWSFowDzPiGXbqcgF5nsxV7RQsonEg8a9FWyj6vNCbMHjWQBwCCQEjKbGQiouhouwdFBkaJ
```


## Canonical form

A post must be restored to its canonical form before processing.

1. All whitespace of any length must be replaced with a single space character
2. All whitespace following a greater-than (`>`), less-than (`<`) or caret (`^`) symbol must be removed
3. Any leading or proceeding whitespace must be removed

A quick (but imperfect) way of telling if a post is in its canonical form is to check if there's any newlines or linebreaks in it, these are typically added by luckypost-enhanced software for presentation purposes. 


## Whitespace

Characters considered to be whitespace by this document are the following:

* Newline character (`\n`)
* Carriage return (`\r`)
* Space character (` `)


## Header

* `2020-01-25 23:59:59`: [Timestamp](#timestamp)
* `en.test`: [Channel name](#channel-name)
* `alice`: [Author name](#author-name)
* `"hokeypokey.jpg" 640x480 143,385 al5djhznzshm5eaha4`: [File attachment](#file-attachment)

Immediately following the header is the post's [body](#body) which is then
followed by the post's [footer](#footer).


## Body

Each section of the body begins with a greater-than (`>`), less-than (`<`) or caret (`^`) symbol, it's not possible to use these symbols in the body for any other purpose.

The greater-than (`>`) symbol indicates that the following text is quoted.

The caret (`^`) symbol is a reference to another post by its [post ID](#post-id).

The less-than (`<`) symbol indicates that the following text is not quoted and not a reference to another post.


The end of the body is detected by finding the start of the footer, not vice-versa.

Following the body is the post's [footer](#footer).


## Footer

* `@apprjxgf2be36vx5b7qnupey7axp44sp253ujnqhubqskpdlet7ta`: [Author address](#author-address)
* `!a16+cNZ+5tJCqrptbC9ySs1cf4sTC5JN1chcYHf7yAbY74DmNifWodoHZY73Ao5fa8TXL8Tk7Eyib8kDfoG4U8KRaTqcQkF9`: [Tail](#tail)


## Timestamp

Each post's [header](#header) contains a timestamp.

The timestamp is in `YYYY-MM-DD HH:MM:SS` format (24 hour).

The timezone is UTC.

### Example

`2020-01-25 23:59:59`



## Channel name

Each post's [header](#header) contains a channel name.

A channel name contains between two and eight channel name parts.

Each channel name part must:

* Consist of lowercase letters a~z and digits 0~9
* Be 2 characters or longer
* Be 32 characters or shorter

The first word in the channel name must be a ISO 639-1 code indicating the primary language used in discussion. If an ISO 639-1 code is not available for the intended language the three-characters-long ISO 639-2 code may be used as a fallback.

### Example

`en.test`


## Author name

Each post's [header](#header) contains an author name.

An author's name contains no whitespace.

An author's name must consist only of the following characters: `ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789-_`

An author's name must be at least 2 characters long.

An author's name must not be longer than 32 characters.

### Examples

* `bob`
* `AliceSmith`
* `charlie_lastname`
* `xXx1337hacker1337xXx`


## File attachment

Files can optionally be attached


## Author address

Each post's [footer](#footer) contains the author's address.

An author's address is prefixed with an at sign symbol (`@`). The characters that follow uniquely identifies the [account](#account) that created the post.


## Tail

Each post's [footer](#footer) contains a tail.

The tail contains densely packed information that isn't much use to human readers.

Each part of the tail is separated by the plus symbol (`+`).

The first part of the tail is the [post's fingerprint specification](#post-fingerprint-specification).

The last part of the tail is the [post's signature](#signature).

The middle parts of the tail are [extensions](#extensions).


## Signature

Each post's [tail](#tail) contains a cryptographic signature at the very end of the post.

The signature is Base58-encoded with padding removed.

The signature is used by the account's encryption scheme to authenticate the post and its author's address.


## Extensions

Each post's [tail](#tail) contains zero or more extensions.

Each extension contains a CHRP indicating the [extension ID](#extension-id), no data is required to follow the CHRP.

Each extension must be at least 1 character long (inclusive of CHRP).

An extension is a [CHRP](#compact-human-readable-prefix-chrp)ed string that may consist of:

* Lowercase letters a~z
* Uppercase letters A~Z 
* Digits 0~9


### Extension ID

Each extension has an associated extension ID to uniquely differentiate its strings from the strings of other extensions.

Each extension ID is a [CHRP](#compact-human-readable-prefix-chrp).


### Registered extensions

* `a`: Amateur networks only (empty, keep off of internet and commercial networks)
* `c`: Country (2-letter country code, all-caps)
* `p`: Proof-of-work (CHRP of hash type followed by PoW stamp)


## Account

A luckypost account is equivalent to a cryptocurrency wallet in that it is entirely derived from a passphrase.

A passphrase is a password that must be unique and strong enough to resist brute-force cracking attempts.

Users that share the same passphrase share the same account.

There is no account recovery, the user must ensure their passphrase is safely backed up.


## Post ID

Each post is uniquely identified by a post ID.

A post ID consists of a [CHRP](#compact-human-readable-prefix-chrp) representing the [post fingerprinting algorithm](#post-fingerprinting-algorithms) to use followed by fingerprint data.

The length of the post ID's fingerprint is specified in the footer of the post.

### Example

`am45rtgthx6wi6h5q`

In this example the `a`-type post fingerprinting algorithm is used followed by the fingerprint consisting 16 characters.

### Security vs compactness

The longer the fingerprint is the more resistant it is to a [post collision](#post-collision) attack.

The shorter the fingerprint is the more pleasant it is to use.

A compromise between the two is necessary, this is decided by the creator of each luckypost.


## Post fingerprint specification

The post fingerprint specification uses a CHRP to specify the post fingerprinting algorithm.

## Post fingerprinting algorithms

In order to generate a [post ID](#post-id) the post must be uniquely fingerprinted using a cryptographic hashing function.

The output of the hashing function is [LB32](#lb32-encoding) encoded.


### Registered post fingerprint algorithms

Each registered algorithm has an assigned [CHRP](#compact-human-readable-prefix-chrp).

Algorithms marked "**insecure**" must not be used unless compromised security is a desired quality.

It is possible that algorithms currently thought of as being secure will be compromised at some point in the future.

* `a`: SHA2-256
* `b`: SHA3-256
* `1a`: MD5 (**insecure**)
* `1b`: SHA1 (**insecure**)


## LB32 encoding

"LB32" refers to binary data encoded using Base32 with a lowercase character set and padding removed.

Base32 was chosen due to not needing mixed case characters, this simplifies typing them in using a keyboard.

## Post collision

A post collision occurs when a post with the same [post ID](#post-id) as an existing post is encountered.

With a sufficient post ID [fingerprint](#post-fingerprint-specification) length the probability of this happening is practically non-existent even in the presence of well-resourced adversaries.

If client software encounters a post collision it will ignore the post it encountered in favor of the post it already has.

Because of each node's preference for the post it already has anyone wanting to jam communication of a particular post must generate a collision before the target post has spread throughout the network.

Due to this time constraint the length requirement can be tolerably lower than typical applications of cryptographic hashing.

## Compact human-readable prefix (CHRP)

In the interest of future-proofing it is necessary to allow for cryptography to be replaced as needed with minimal service disruption.

The [signature](#signature) and [post ID](#post-id) both use encryption but also need to be compact.

A CHRP (pronounced "chirp") serves both these future-proofing and compactness requirements when specifying the type of encryption being used.

A CHRP is always between 1 and 10 characters long (inclusive).

If all 26 letters of the English alphabet are used a CHRP can represent 104 trillion different values.

### Single-character CHRP

If the CHRP starts with anything other than digits 1 through 9 (excluding 0) it is a single-character CHRP.

A single-character CHRP consists of just a single character.

### Multi-character CHRP

If the CHRP starts with a digit between 1 and 9 inclusive it is a multi-character CHRP.

The first character in a multi-character CHRP indicates the number of following characters that are part of the CHRP.

A CHRP starting with "1" will be two characters long including the "1".

### Examples

* `a`: Single-character CHRP
* `1a`: Multi-character CHRP
* `9aaabbbccc`: Multi-character CHRP (max length)
* `0`: Single-character CHRP
