# SatsChain Bridge

## Table of Contents

- [SatsChain Bridge](#satschain-bridge)
  - [Table of Contents](#table-of-contents)
  - [Introduction](#introduction)
  - [Architecture](#architecture)
    - [Overview](#overview)
    - [Components](#components)
      - [Taproot](#Taproot)
      - [Bitcoin SPV](#Bitcoin SPV)
      - [Index](#Index)
      - [Bridge Contract](#bridge-contract)
      - [User Interface](#user-interface)
      - [Backend Services](#backend-services)
  - [Fundamental Principles](#fundamental-principles)
    - [Cross-Chain Asset Transfer](#cross-chain-asset-transfer)
    - [Security Mechanisms](#security-mechanisms)
    - [Fee Structure](#fee-structure)
  - [User Operations](#user-operations)
    - [Connecting Wallet](#connecting-wallet)
    - [Initiating a Transfer](#initiating-a-transfer)
    - [Monitoring Transaction Status](#monitoring-transaction-status)
    - [Withdrawing Assets](#withdrawing-assets)
  - [Troubleshooting](#troubleshooting)
  - [FAQ](#faq)

## Introduction

**SatsChain Bridge** (decentralized bridge) is an advanced technical solution designed to achieve decentralized asset transfer between Bitcoin assets (including BTC, BRC20, RUNES, etc.) and **SatsChain**.

For BTC assets, **SatsChain Bridge** adopts Taproot, Bitcoin SPV (Simplified Payment Verification) and BFT（Byzantine Fault Tolerance) technology to achieve fully decentralized cross-chain asset transfer. This approach not only improves the security and privacy of cross-chain operations, but also simplifies the verification process.

For BRC20 and RUNES assets, based on cross-chain BTC assets, **SatsChain Bridge** introduces a decentralized indexing mechanism for parsing and processing BRC20/RUNES transactions. This mechanism ensures that cross-chain transfers of complex asset types also have decentralized characteristics, improving the flexibility and applicability of the overall system.

Through these technical innovations, **SatsChain Bridge** achieves seamless connection between Bitcoin assets and SatsChain, provides users with a safe and efficient cross-chain asset transfer solution, and promotes further interoperability and development of the blockchain ecosystem.

## Architecture

### Overview

![SatsChain Bridge](./SatsChainBridge.png)

### Components

#### Taproot

The Taproot upgrade is an important improvement to the Bitcoin network, covering Schnorr signatures (BIP 340), Taproot (BIP 341) and Tapscript (BIP 342), aiming to improve the privacy, efficiency and flexibility of Bitcoin. Schnorr signatures allow multiple signatures to be merged into one, reducing transaction fees and memory burden. Merklized Abstract Syntax Trees (MAST) enhances the anonymity and privacy of transactions by hiding complex Bitcoin scripts in a Merkle tree structure.

MuSig2 is an advanced multi-signature scheme that allows multiple participants to co-sign a single file or transaction and ensures that the final signature appears to be generated by a single entity when observed from the outside. This scheme is specifically designed to enable secure communication between multiple parties in an insecure network environment, providing an efficient and secure multi-signature solution.

Using Taproot technology, we can select m signers from n signers and generate an m-of-m Schnorr aggregate public key through the MuSig2 multi-signature scheme. Then, a MAST tree is constructed with these aggregated public keys as leaf nodes, and finally an n-of-m threshold multi-signature address is generated. This process combines the privacy of Taproot and the multi-signature advantages of MuSig2, providing a more efficient and secure multi-signature solution.

#### Bitcoin SPV

Bitcoin SPV (Simplified Payment Verification) is a lightweight verification method that allows users to verify transactions without downloading the entire blockchain. SPV nodes can confirm the validity of transactions and prevent double payments by downloading block headers and related transaction information, relying only on a small amount of data. Integrating Bitcoin SPV into SatsChain's verification nodes enables SatsChain to synchronize and verify Bitcoin transactions in a decentralized manner. This integration improves the interoperability and efficiency of SatsChain and ensures the security and reliability of cross-chain transactions.

#### Index

Since Bitcoin itself cannot identify specific assets, asset protocols such as BRC20 and RUNES rely on external indexes to parse asset information. These indexes are implemented as off-chain applications based on protocol specifications and exist in multiple versions. Relying on separate index nodes and specific versions for cross-chain asset transfers will bring centralized trust risks.

To achieve the decentralization of indexes, SatsChain has introduced a variety of indexes with different implementation versions, including open source OPI indexes, OKLINK and UNISAT API services, and integrated them into SatsChain nodes. These nodes parse specific Bitcoin transaction information and reach consensus using the Byzantine Fault Tolerance (BFT) mechanism to ensure the security and reliability of index data.

This method significantly improves the flexibility and security of the system by decentralizing the parsing and verification of BRC20 and RUNES asset information, reduces the trust dependence on a single index node, and enhances the credibility and reliability of cross-chain transactions.

#### Bridge Contract

SatsChain uses the Substrate technology stack to implement the EVM virtual machine, and acts as a bridge between the Substrate Wasm virtual machine and the EVM through the Bridge Contract. During the asset recharge process, the system calls the Bridge Contract through the Wasm virtual machine to complete the recharge operation and realize the asset transfer across virtual machines. When withdrawing assets, the system calls the Wasm precompiled contract through the Bridge Contract to initiate an asset withdrawal request to ensure the accuracy and security of the withdrawal operation.

#### User Interface

Detail the components of the user interface and how users interact with the bridge.

#### Backend Services

Explain the backend services supporting the bridge operations.

## Fundamental Principles

### Cross-Chain Asset Transfer

When a user recharges BTC, BRC20 or RUNES assets to a threshold multi-signature address generated by Taproot, SatsChain synchronizes related transactions and verifies their validity through Bitcoin SPV technology.

For BTC assets, the system directly parses the transaction on the chain and calls Bridge Contract to perform the recharge operation.

For BRC20 and RUNES assets, after verifying the validity of the transaction, each node uses a decentralized index node to parse the transaction information, reaches a consensus through the Byzantine Fault Tolerance (BFT) mechanism, and then calls the Bridge Contract to implement the recharge operation.

In the withdrawal operation, the system first initiates a withdrawal request through the Bridge Contract. Subsequently, the SatsChain node verifies the withdrawal information and constructs a withdrawal transaction. When the number of signed nodes reaches a predetermined threshold, the node aggregates the signatures and assembles the transaction, and finally broadcasts the transaction to the Bitcoin network to complete the withdrawal operation.

### Security Mechanisms

Bitcoin SPV (Simplified Payment Verification) and BFT (Byzantine Fault Tolerance) technologies work together to ensure the validity and accuracy of Bitcoin transactions. SPV technology uses lightweight verification to enable nodes to verify the validity of transactions without downloading the entire blockchain, while the BFT mechanism uses a consensus algorithm to prevent malicious nodes from damaging the system, thereby improving the security and reliability of the network.

In order to ensure the decentralization of the index, SatsChain introduces a variety of index mechanisms and BFT consensus. Indexes of different implementation versions (including open source OPI index, OKLINK and UNISAT API services, etc.) parse transaction information between nodes and reach consensus through BFT to ensure the security and accuracy of index data.

In addition, SatsChain uses Sats tokens for staking as an incentive and punishment mechanism for nodes. Nodes need to stake a certain number of Sats tokens to participate in the network consensus. If the node behaves maliciously or attempts to attack the network, its staked Sats tokens will be punished or confiscated. This mechanism not only incentivizes nodes to maintain honest behavior, but also further enhances the overall security of the system.

### Fee Structure

The fee mechanism of SatsChain Bridge reaches a consensus on the fee by regularly updating the fee rate of the Bitcoin network and combining it with the Byzantine Fault Tolerance (BFT) algorithm. The system periodically obtains the fee rate data of the current Bitcoin network and disseminates and verifies it among the SatsChain nodes. Through the BFT mechanism, each node reaches a consensus on the latest fee rate, thereby achieving a dynamic estimate of the fee. This mechanism ensures the rationality and real-time nature of transaction fees, and users can enjoy more accurate and fair fee calculations when performing cross-chain operations.

## User Operations

### Connecting Wallet

Instructions for users to connect their wallets to the SatsChain Bridge.

### Initiating a Transfer

Step-by-step guide for initiating a cross-chain transfer.

### Monitoring Transaction Status

Explain how users can monitor the status of their transactions.

### Withdrawing Assets

Detail the process for withdrawing assets once they are transferred.

## Troubleshooting

Provide solutions for common issues users and developers may encounter.

## FAQ

Answer frequently asked questions about the SatsChain Bridge.
