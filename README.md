# [WIP] Covenants for TNS (Themelio Naming System)

The Themelio Naming System (TNS) is a hierarchical, polycentric, and extensible naming system with strong endogenous trust, built on top of the Themelio blockchain. Like [ENS](https://ens.domains/) on Ethereum, it's intended as a general-purpose naming system with much stronger security and decentralization than traditional centralized solutions like DNS or the Web PKI. Unlike ENS, though, most components of TNS are off-chain, yet TNS is significantly more trustless and neutral due to its immutable, on-chain root of trust.

This repository hosts _on-chain_ components of TNS. Right now, the only part is the _root trie_, in `trie.melo`.

## Structure of the root trie

The root trie is an on-chain data structure that keeps track of the **initial registration** of the names, by a binary trie embedded in the transaction graph. In particular, we have a **root transaction**
