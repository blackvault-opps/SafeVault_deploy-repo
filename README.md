Vault Coin (VLT)

Public Project Overview and Pre-Deployment Record

Current status — September 2, 2026: Vault Coin (VLT) is under pre-deployment technical review. It has not been deployed to Sepolia, Ethereum mainnet, or any other blockchain network. No official VLT proxy address, implementation address, or deployment transaction has been recorded.

Vault Coin (VLT) is an owner-managed ERC-20 token project built with an ERC-1967 proxy and the OpenZeppelin UUPS upgrade pattern. This page documents the approved design, control model, validation work, and development journey before deployment.

Repository builds, tests, simulations, commits, pull requests, and GitHub Actions results are development evidence only. None of them proves that a blockchain deployment has occurred.

Documentation boundaries

This public page is a documentation record. It is maintained separately from the Vault Coin source-code repository and its development jobs.

Vault Coin (VLT), the BlackVault Public Network, and SafeVault are separate projects and should be documented on separate pages. A reference between their pages does not establish a shared deployment, contract integration, wallet, treasury, ownership structure, or authorization relationship.

The separate Safe at 0xB06A1DDcb9b31ecBb1a298C68954220FF96E3a03, as well as any nested Safe, is outside the Vault Coin token authorization model.

Approved VLT design

Property

Approved value

Name

Vault Coin

Symbol

VLT

Decimals

18

Initial supply

100,000,000 VLT

Lifetime issuance ceiling

420,000,000 VLT

Intended initial owner

0xc1cC3138699e07B6d7b990DBa8fAE30b332a1eA6

Initial token recipient

0xc1cC3138699e07B6d7b990DBa8fAE30b332a1eA6

Initial administrative-burn fee

100 basis points (1%)

Proxy architecture

ERC-1967 proxy with owner-authorized UUPS upgrades

Ownership transfer

Two-step transfer to a deployed contract or Safe

Ownership renunciation

Prohibited; the contract is not intended to enter a zero-owner state

The intended owner is the existing non-nested Vault Coin Safe at 0xc1cC3138699e07B6d7b990DBa8fAE30b332a1eA6.

Lifetime issuance ceiling

The 420,000,000 VLT limit is a lifetime issuance ceiling in the reviewed implementation. Tokens that are burned remain counted as previously issued, so burning does not restore minting capacity.

The limit is not immutable. Because the owner can authorize a UUPS implementation upgrade, a future owner-approved upgrade could technically modify or remove this rule. Preservation of the ceiling therefore depends on governance, review, and owner authorization.

Privileged owner controls

The reviewed design gives the owner authority to:

mint VLT within the remaining lifetime issuance allowance;

pause and unpause ordinary token movement;

blacklist and unblacklist accounts;

administratively burn VLT from a holder without an allowance and charge a configurable VLT fee;

administratively transfer VLT from an account to an owner-selected address;

change the administrative-burn fee and its recipient;

recover unrelated ERC-20 tokens and ETH held by the proxy;

begin a two-step ownership transfer; and

authorize implementation upgrades.

These controls are unusually powerful and must be clearly disclosed to prospective holders.

Administrative burns and administrative transfers are designed to bypass the ordinary pause and blacklist restrictions. Each operation requires a nonzero reasonHash and emits a permanent on-chain event. The reasonHash records the evidence reference selected by the owner; the smart contract cannot determine whether the referenced reason is legally or factually justified.

At the initial 1% fee, calling adminBurn(account, 100 ether, reasonHash) requires the account to hold at least 101 VLT. The operation transfers 1 VLT to the configured fee recipient and destroys 100 VLT. It cannot burn tokens that the account does not hold or create a negative balance.

Holder controls

Holders retain standard ERC-20 transfer and approval functions, subject to the contract's pause and blacklist rules. They can also:

call burn(amount) to destroy their own VLT; and

call burnFrom(account, amount) to destroy VLT covered by an allowance.

Holder-initiated burns do not pay the administrative-burn fee. When the token is paused, ordinary transfers, minting, and holder-initiated burns are blocked. Blacklisted accounts cannot send or receive VLT, receive newly minted VLT, burn VLT, or participate in approvals.

Ownership safety

Calling the standard zero-argument renounceOwnership() function always reverts. The reviewed successor-based ownership process starts a two-step transfer and leaves the current owner in control until the nominated successor explicitly accepts ownership.

The contract is designed not to enter a zero-owner state intentionally. A proposed successor must be a deployed contract or Safe, rather than an ordinary externally owned wallet.

Repository structure

src/VaultCoin.sol — upgradeable VLT implementation

script/DeployVaultCoin.s.sol — implementation and proxy deployment script

test/VaultCoin.t.sol — unit, fuzz, authorization, and upgrade tests

test/VaultCoin.invariant.t.sol — stateful supply and ownership invariants

test/DeployVaultCoin.t.sol — local deployment-script verification

CONTROL_MODEL.md — authority and trust boundaries

docs/ADMIN_OPERATIONS.md — administrative procedures and warnings

docs/DEPLOYMENT.md — simulation and separately authorized deployment process

docs/UPGRADES.md — upgrade review and execution controls

REVIEW_AUDIT.md — implementation and validation evidence

SECURITY.md — security assumptions and reporting policy

Toolchain and validation commands

Solidity 0.8.24

OpenZeppelin Contracts v5.0.2

OpenZeppelin Contracts Upgradeable v5.0.2

forge-std v1.9.6

Foundry v1.8.1

forge install OpenZeppelin/openzeppelin-contracts@v5.0.2 --no-commit
forge install OpenZeppelin/openzeppelin-contracts-upgradeable@v5.0.2 --no-commit
forge install foundry-rs/forge-std@v1.9.6 --no-commit
forge fmt --check
forge lint --deny warnings
forge build --sizes
forge test -vvv

Deployment evidence standard

Vault Coin must continue to be described as not deployed unless a completed network transaction can be independently verified. A public deployment record should identify, at minimum:

the blockchain network and chain ID;

the official ERC-1967 proxy address;

the implementation address;

the deployment transaction hash;

the deployment block number and timestamp;

the verified source-code record;

the owner address after initialization; and

the initial supply recipient and recorded balance.

Until that evidence exists and is published, no address should be presented as an official VLT token contract.

Review and risk notice

This project repository and public development record are not an independent security audit, legal opinion, financial recommendation, promise of token value, or representation that VLT is available for purchase or transfer.

The owner controls are unusually powerful. Independent technical and legal review should be completed before deployment or before assigning VLT any real economic value.

Project journal

Future entries should clearly identify their status using labels such as Planned, In development, Under review, Approved, Simulated, or Deployed. Only a verified on-chain transaction should receive the Deployed label.

Public journal entries may summarize completed repository work, but private credentials, RPC URLs containing access keys, seed phrases, private keys, signatures, internal security procedures, and unverified wallet claims must never be published.
