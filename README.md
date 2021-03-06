# Luckypost

A luckypost is a compact human-readable text-based data structure designed for
decentralized and trust-less authenticated public text-based discussion.

This is a Python library for creating, parsing and verifying luckyposts, it also
provides a basic command-line interface. 

This library is intended to be used by luckynet clients.


# Installation

You'll need a Python interpreter along with the pip package installer.

`python -m pip install luckypost`


# Usage

A command-line interface is provided to access the library's functionality, this
is intended for luckynet developers, not users (but users are welcome to use 
it if they want).

## Hello world
`python -m luckypost create en.test authorname "<Hello world!"`

The user will then be prompted to enter their passphrase, alternatively it can
be specified on the command line with the `-p` argument.

## Verification

`python -m luckypost verify "2022-04-20 05:06:21 en.test authorname <Hello world! @afw43if2j7b5r34ktfpiasofk5jg2zo3gqhlcl6s2hre2xl7ntbba !a16+K7HPXucuCQMiV4676N43VLFzFpU1RBLDgdhFJgNrHYm8NBqz85pnWLYTv9PjsnWcut33CtY13vEY54ycUY5rJhA"`

If the given luckypost is authentic then its ID and POWER levels will also be shown.

## PoW mining

`python -m luckypost mine a afw43if2j7b5r34ktfpiasofk5jg2zo3gqhlcl6s2hre2xl7ntbba`

The `a` is the type of hashing algorithm to use, in this case SHA256.

Extensions and their respective POWER levels will be printed out as
higher-levelled nonces are discovered.

### Using

Take the extension and include it when creating a post using the `-x` argument.

`python -m luckypost create en.test authorname "<Hello world!" -x pabzPrL12m`

### Environmental impact

Luckypost is not a cryptocurrency, proof-of-work calculations are only used to
distinguish an account from those belonging to spammers. There is no financial
incentive to mine higher POWER levels.
