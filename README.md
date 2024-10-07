# The dataset of Ethereum payload-based transaction phishing

This is the repository for paper "Dissecting Payload-based Transaction Phishing on
Ethereum" accepted to NDSS 2025.

## Dataset

[Dataset](https://github.com/HypoopyH/PTXPhish/tree/main/dataset) contains the dataset we used in our experiments. Feel free if you have any questions.

| Category                       |                   |                     | Target Assets | Spread Method | Num  |
|--------------------------------|-------------------|---------------------|---------------|---------------|------|
| Exploiting legitimate contract | Ice phishing      | Approve             | ERC20         | website       | 1247 |
|                                |                   | Permit              | ERC20         | website       | 814  |
|                                |                   | SetApproveForAll    | NFT           | website       | 508  |
|                                | NFT order         | Bulk transfer       | NFT           | website       | 37   |
|                                |                   | Proxy upgrade       | NFT           | website       | 108  |
|                                |                   | Free buy order      | ERC20 & NFT   | website       | 464  |
| Deploying phishing contract    | Address Poisoning | Zero value transfer | ERC20         | Transaction   | 104  |
|                                |                   | Fake token transfer | ERC20         | Transaction   | 100  |
|                                |                   | Dust value transfer | ERC20         | Transaction   | 22   |
|                                | Payable Function  | Airdrop function    | ETH           | Transaction   | 788  |
|                                |                   | Wallet function     | ETH           | Transaction   | 808  |
| Benign                         | -                 | -                   | -             | -             | 13557 |

The open-source ground-truth dataset is in the **./dataset/PTXPHISH.xlsx**

## Detection Bot/Rules

Our detection system is published in [Forta](https://app.forta.network/bot/0x9ba66b24eb2113ca3217c5e02ac6671182247c354327b27f645abb7c8a3e4534?search=0x9ba66b24eb2113ca3217c5e02ac6671182247c354327b27f645abb7c8a3e4534), and it is free to subsribe.

### Description

This bot monitors:

* ice-phishing - This is a special type of phishing attack in which a user is not tricked into disclosing private information but rather is tricked into signing an on-chain transaction that gives an attacker control over the user's digital assets. This often involved signing an approval transaction. Once the transaction is signed and incorporated into a block the attacker can proceed to transfer a user’s digital assets to their own wallet.
* Nft-order - Seaport is a protocol to trade tokens. Seaport allows users to create offers by merely signing a transaction and not submitting it on-chain (it is structured this way as a gas saving measure). Traditionally, users think signing a transaction and not submitting it on-chain is a safe operation. This is not the case. In this attack, the scammer tricks the user into signing an offer that offers their digital assets (e.g. a set of NFT) for a value well below market price. The scammer then executes the order on the users behalf causing the user to lose their digital assets.
* Address-poisoning - In this attack the scammer examines the transaction history of the user and submits 0 value transfers to or from the user from an address that looks similar to an address in the user's history. Since the value is 0, it does not require any approvals. The end result is that the transaction history for a user's wallet is now poisoned with addresses the attacker controls. A user may accidentally transfer tokens or native assets to those attacker controlled addresses (some variations of the attack exist where the attacker transfers a small amount as opposed to 0 amount to the user). This threat category is used for labeling poisoning addresses
* Payble-function - This is similar to ice phishing, but does not involve a token contract. Here the user is simply tricked in signing and submitting a transaction on-chain that transfers assets to the scammer.

## Citation

If you use the related dataset or the insights we observed in our paper. Please considering cite our paper.

```
@inproceedings{chen2025dissecting,
title={Dissecting Payload-based Transaction Phishing on Ethereum},
author={Chen, Zhuo and Hu, Yufeng and He, Bowen and Luo, Dong and Wu, Lei and Zhou, Yajin},
booktitle={Network and Distributed Systems Security (NDSS) Symposium},
year={2025}
}
```

