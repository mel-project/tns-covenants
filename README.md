# [WIP] Covenants for TNS (Themelio Naming System)

The Themelio Naming System (TNS) is a hierarchical, polycentric, and extensible naming system with strong endogenous trust, built on top of the Themelio blockchain. Like [ENS](https://ens.domains/) on Ethereum, it's intended as a general-purpose naming system with much stronger security and decentralization than traditional centralized solutions like DNS or the Web PKI. Unlike ENS, though, most components of TNS are off-chain, yet TNS is significantly more trustless and neutral due to its immutable, on-chain root of trust.

This repository hosts _on-chain_ components of TNS. Right now, the only part is the _root trie_, in `trie.melo`.

## Structure of the root trie

The root trie is an on-chain data structure that keeps track of the first-come, first-serve **initial registration** of the names, by a trie embedded in the transaction graph. This trie maps 64-bit unique identifiers, which correspond to the first 64 bits of the hash of the name, to an "NFT" (a unique custom token whose total supply is 1) that represents the freely transferable name.

In particular, we have a **root transaction**, which has 2 outputs. Any of these outputs can only be spent by a transaction that _itself_ has 256 outputs, etc until we have a 7-level tree of transactions, each with 256 outputs. These final outputs must then create an "NFT", by creating a coin denominated in a custom token, with a value of 1.

This trie is then looked up _byte-by-byte, by the first 64 bits / 8 bytes of the hash of the name_. For example, given the name `example.mel`, the hash is `8f d6 40 e8 99 98 2b ba...`. Thus, the asset representing the name is:

the NFT created by the

- **186th** (`ba`) output of the transaction spending the
- **43rd** (`2b`) output of the transaction spending the
- **152nd** (`98`) output of the transaction spending the
- **153rd** (`99`) output of the transaction spending the
- **232nd** (`e8`) output of the transaction spending the
- **64th** (`40`) output of the transaction spending the
- **214th** (`d6`) output of the transaction spending the
- **143rd** (`8f`) output of the _root transaction_

The first transaction that moves this NFT must have a 24-byte/192-bit value in its `data` field, which supplies the remaining 256 bits of the name's blake3 hash. This avoids any ambiguities that might come from 64-bit hash collisions.

This only gives you an NFT that represents _custody_ of a particular name. Tracking what is actually _bound_ to that name is TBD.
