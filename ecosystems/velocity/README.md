---
description: >-
  Intro to Velocity Network
---
# Velocity Network Foundation

Velocity Network<sup>TM</sup> is a public permissioned distributed network, based on a permissioned version of the Ethereum Blockchain utilizing Hyperledger Besu. Operating a node and writing to the Velocity Ledger requires permission from the Velocity Network Foundation<sup>R</sup>.

The following data is stored on chain:
* organization metadata - DID, profile, endpoint
* credential metadata (encrypted) - ID, type, public key, revocation status
* verification voucher transactions
* credential types and schemas

# Network participants

## High level

* Holder - a person that holds the credential on behalf of the subject (themselves or another person)
* Issuer - an organization that creates and issues credentials
    * first party issuer - an entity that can directly attest to the claims within the credential
    * notary issuer - an entity that can evaluate evidence to attest to the claims within the credential
* Relying Party - an entity that requests and verifies credentials from a Holder

## Low level

* Wallet Provider (Holder App Provider) - an organization offering digital wallets to be used by Holders
* Credential Agent Operator - an organization operating a credential agent
    * Agent - an interface to the network used by organizations (Issuer, Relying Party, Holder) - call contracts, retrieve account states - form the 'layer-2' network
        * Tenant - an organization’s delegate on which behalf the agent is acting
* Node Operator - an organization operating a node
    * Node - a participant on the network holding copies of the underlying ledger
        * Members (Stewards) - read-only nodes with limited data access that forward write operations to Validators
        * Validators - full-write permission nodes that participate in consensus
* Velocity Network Registrar - a set of centralized services that are used for administering the accredited organizations and credential types on the Network 
* Credits hub - a module where Velocity credits are administered and credit reward transactions can be executed
* Voucher hub - a module where Velocity vouchers are administered and top up transactions can be executed
* The ledger - the distributed blockchain-based, continuously-replicated, global cryptographic database maintained by Stewards operating nodes communicating with the Velocity consensus protocol

# Workflows

* Issuing - the process of asserting claims about a Holder who receives the verifiable credential
    * by writing a transaction to the Velocity Ledger which includes the credential ID, its type, the Issuer ID, and the public key matching the private key that signed it
* Revocation - the act of an Issuer revoking the validity of a credential
    * by writing a transaction to the Velocity Ledger marking the credential as revoked
* Verification - the process of confirming that a verifiable credential is not modified, revoked or expired and is issued by a trusted authority
    * by accessing the Velocity Ledger to retrieve the unique public key associated with credential and verify its signature

# Verifiable Credentials

Velocity currently uses the JWT format for encoding credentials with JWS signatures using SECP256K1 as proofs.

Verifiable credentials are divided into the following categories:
* Layer-1 credential types - network’s core set of credential types (e.g. Email, IdDocument, OpenBadgeCredential)
    * for each issued credential, the Issuer receives a reward in the form of Velocity Credits
* Layer-2 credential types - any custom credential type
    * should be mapped to a Layer-1 type in order for the Issuer to be eligible for a reward

More about credential types here https://docs.velocitynetwork.foundation/docs/developers/basics-credential-types.

# Decentralized identifiers

* did:ion - used to identify organizations or individuals
    * received when registering with the Registrar
* did:velocity - used to identify credentials
    * is immutable
    * stores only a single key and credential type
    * resolving it will burn an NFT to permit DID resolution