# Vault Coin™ Framework

Vault Coin™ (VLT) is the developing ERC-20 network asset of BlackVault Public Network™. SafeVault™ is intended to support VLT as a self-custody wallet interface after the token contract and wallet integration have completed their respective testing, review, and deployment approvals.

Vault Coin and SafeVault are separate but connected systems:

- The Vault Coin smart contract defines VLT supply rules, token behavior, administrative authority, and upgrade controls.
- SafeVault provides a planned user-controlled interface for viewing, receiving, holding, and transferring supported assets.
- SafeVault does not replace, override, or independently modify the Vault Coin contract.
- Publication of this framework does not deploy VLT or authorize a blockchain transaction.

## Canonical technical source

The authoritative source code, tests, deployment scripts, security records, and technical controls for Vault Coin are maintained in the separate [Vault Coin technical repository](https://github.com/blackvault-opps/Vault-Coin-VLT-project).

The [Vault Coin public wiki](https://github.com/blackvault-opps/Vault-Coin-VLT-project/wiki) provides supporting public documentation.

This page is a publication summary for the SafeVault project. If this summary and the canonical technical repository differ, the versioned source and records in the canonical technical repository govern the technical implementation.

## Confirmed token configuration

| Property | Current framework |
|---|---|
| Name | Vault Coin™ |
| Symbol | VLT |
| Decimals | 18 |
| Initial supply | 100,000,000 VLT |
| Lifetime issuance ceiling | 420,000,000 VLT |
| Architecture | ERC-1967 proxy with UUPS upgrades |
| Ownership | Two-step ownership transfer to a deployed contract or Safe |
| Ownership renunciation | Zero-owner renunciation prohibited |
| Deployment status | Not deployed |

The lifetime issuance ceiling tracks cumulative minting. Burning VLT reduces the circulating supply but does not restore minting capacity under the current implementation. Because the contract uses an owner-authorized UUPS upgrade model, a future approved implementation could technically alter contract rules. Upgrade review, governance approval, testing, and public disclosure therefore remain part of the control framework.

## Token-holder functions

The current framework provides standard ERC-20 transfer and approval behavior. Holders may also:

- burn their own VLT; and
- burn VLT from another account when supported by a sufficient allowance.

Ordinary transfers, minting, and holder burns are blocked while the token is paused. Blacklisted accounts cannot participate in ordinary transfers, minting, burning, or approvals.

## Administrative controls

The authorized owner may:

- mint VLT within the remaining lifetime issuance ceiling;
- pause and unpause ordinary token movement;
- blacklist and unblacklist accounts;
- perform an administrative burn without holder allowance, subject to the configured VLT fee;
- transfer VLT from an account to an owner-selected address without holder allowance;
- change the administrative-burn fee and fee recipient;
- recover unrelated ERC-20 tokens or ETH held by the VLT proxy;
- initiate a two-step ownership transfer; and
- authorize implementation upgrades.

Administrative burns and owner-directed transfers require a nonzero reason hash and emit permanent contract events. These functions are designed to remain available while ordinary token movement is paused and when an affected account is blacklisted. They are significant centralized controls and must remain clearly disclosed.

## Treasury and ownership structure

The confirmed initial owner, treasury, fee recipient, and initial-supply recipient is:

`0xc1cC3138699e07B6d7b990DBa8fAE30b332a1eA6`

The address is intended to operate as the Vault Coin multisignature Safe. Signer identities and the approval threshold are managed by the Safe rather than by the VLT contract itself and must be independently verified before a network deployment.

The separate Safe at `0xB06A1DDcb9b31ecBb1a298C68954220FF96E3a03`, and any previously referenced nested Safe, are outside the Vault Coin authorization model.

## SafeVault integration boundary

SafeVault is intended to let an authorized wallet holder interact with VLT through cryptographic wallet signatures. SafeVault is not intended to possess or use a holder's private key, recovery phrase, or VaultKey™.

The Vault Coin owner's contract-level powers remain distinct from custody of a user's wallet credentials. Integrating VLT into SafeVault will not remove or conceal the owner controls defined by the token contract.

Before VLT support is activated in SafeVault, the wallet integration should verify:

- the intended blockchain network;
- the final VLT proxy address;
- the verified contract implementation;
- token name, symbol, decimals, and displayed balance;
- transaction destination, amount, network, and estimated fee before signing; and
- confirmation and failure states using independently verifiable chain data.

## Validation record

The documented local development record includes:

- successful formatting, linting, and compilation checks;
- 53 passing tests with no failures or skipped tests;
- 256-run fuzz testing;
- 256-run stateful invariant testing covering 128,000 calls;
- 96.61% line coverage for `src/VaultCoin.sol`;
- ABI inspection; and
- a successful local deployment-script rehearsal without an RPC endpoint, signature, or transaction broadcast.

These results are implementation evidence. They are not an independent security audit and do not establish that VLT has been deployed.

## Deployment status

Vault Coin remains in pre-deployment review. No VLT proxy address, implementation address, or deployment transaction is identified by the canonical repository as a completed deployment.

A source-code commit, merged pull request, passing CI run, local simulation, read-only network check, or published framework page is not blockchain deployment evidence. Any Sepolia or production transaction requires its own verification record and explicit authorization.

## Publication scope

This document publishes the current relationship between SafeVault and Vault Coin for project review and public reference. It does not copy the active contract source into the SafeVault repository, create a shared deployment, grant SafeVault control over the token, or authorize issuance or transfer of VLT.

For implementation-level details, consult the canonical technical repository and its version history.

