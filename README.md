# Bitcoinolog: Reason about Bitcoin addresses with Prolog

## Offline Bitcoin wallet creation

*Bitcoinolog* uses [Prolog](https://www.metalevel.at/prolog) and
OpenSSL to create Bitcoin addresses and private&nbsp;keys with several
nice properties:

  - generated keys are **cryptographically&nbsp;secure** to the extent that
    OpenSSL guarantees this property
  - the Prolog code is **short** and uses **no external programs**
  - keys can be generated **offline**, on a machine that has no
    Internet&nbsp;connection.

Bitcoinolog requires SWI-Prolog **7.5.10** or&nbsp;later.

To try it, download [**`bitcoinolog.pl`**](bitcoinolog.pl)
and&nbsp;run:

    $ swipl bitcoinolog.pl

Here is an example query that you can try:

    ?- repeat,
           new_private_key(PrivateKey),
           private_key_to_public_key(PrivateKey, PublicKey),
           public_key_to_address(PublicKey, Address),
           private_key_to_wif(PrivateKey, WIF),
           portray_clause((address_key(A, K) :- A=Address, K=WIF)),
           false.

This Prolog query *generates* Bitcoin addresses and private&nbsp;keys
in Wallet Import Format&nbsp;(WIF), yielding:

    address_key(A, B) :-
         A='1Nis7V58Mb839kXb9RZMDzAN6ZTQbNfGC4',
         B='L1T3AnvHDtaAhkr9zxKokKzqphx26cvdoU8HbEifsWH6chy4bzYS'.
    address_key(A, B) :-
         A='1D34yFJGRtiLuW2abwPBfks4cCi1Usp9a3',
         B='L5NUQyHr5zaJgG9ALbVGD1tcxodf51kUvQDANcNhpej1itV9KNLD'.
    address_key(A, B) :-
         A='12TUkSL2yyiiAD2f4zAcGDQPev2FSQmVwF',
         B='KyR4Ut96DFadt1LbdZNFzCLuJ2Hw9KSeX6wfMv2dnQwgympWZyyU'.
    address_key(A, B) :-
         A='1HySx6JBQKZoPqjUPVnbitFASKJjdAWWzx',
         B='Kxcr5G39Y7jUvsmsoDK5TnezsQ4FkTcYRVTcxzTT3uLYKnHFYiVh'.

For more information, visit:

[**https://www.metalevel.at/bitcoinolog/**](https://www.metalevel.at/bitcoinolog/)

**Video**: https://www.metalevel.at/prolog/videos/bitcoinolog

## Elliptic Curve Cryptography in Prolog

Bitcoinolog uses
[**`library(crypto)`**](http://eu.swi-prolog.org/pldoc/man?section=crypto)
for hashing and reasoning over *elliptic&nbsp;curves*.

Alternatively, you can use [**`ecclog.pl`**](ecclog.pl) for reasoning
over elliptic&nbsp;curves *in&nbsp;Prolog*. Simply use the `ecc_`
predicates instead of those starting with&nbsp;`crypto_`:

  - `crypto_curve_generator/2` &rightarrow; `ecc_curve_generator/2`
  - `crypto_curve_order/2` &rightarrow; `ecc_curve_order/2`
  - etc.

Internally, `library(ecc)` uses
[CLP(ℤ)&nbsp;constraints](https://www.metalevel.at/prolog/clpz)
to&nbsp;facilitate
[declarative&nbsp;debugging](https://www.metalevel.at/prolog/debugging).

