# SafeVault™

**Your account. Your assets. Your authority.**  
BlackVault Public Network · Public architecture and product documentation

SafeVault brings a primary BlackVault smart account and optional connections to existing wallets into one asset workspace. Its planned experience combines balances, activity, receive/send review, account settings, and assistance from Vault AI.

## The two-layer experience

SafeVault has two wallet layers:

1. **Homebase — the primary BlackVault smart account.** A user signs in to the BlackVault application to reach their Homebase workspace, assets, activity, and account controls. The approved product direction starts with a holder-controlled smart account. Application login, account initialization, and blockchain authorization are separate operations.
2. **Connected external wallets — an optional second layer.** Existing compatible wallets retain their own addresses, networks, balances, and permissions. Connecting one enables supported visibility and interaction; moving assets into Homebase is a separately authorized transfer.

The primary design uses an ERC-4337-style account model. Optional EIP-7702 support for compatible external EOAs is a separate integration proposal. A connected wallet is not evidence of an active delegation. Account deployment timing, gas arrangements, authentication/recovery, and infrastructure providers remain implementation selections.

Assets remain recorded on their respective blockchains. Homebase brings those records into a coordinated interface; signing in does not merge accounts or transfer balances.

## What belongs in SafeVault

| Area | Intended experience |
| --- | --- |
| Homebase | The user's primary BlackVault smart account and account overview |
| Assets | ETH, supported tokens, VLT after production deployment, and the separate FUN testnet experience |
| Connected assets | Optional external-wallet views with clear address and network labels |
| Activity and transfers | Transaction details, recipient and fee review, and confirmed results |
| Vault AI | Project guidance, asset discovery, evidence review, and wallet handoffs |
| Permissions and settings | Account controls and separately enabled delegation where implemented |
| Vault Coin Rewards | Planned, separate token/product surface with eligibility and distribution details to be defined |

## Network and token roles

| Context | Network | Configuration status |
| --- | --- | --- |
| Vault Coin (VLT) | Ethereum mainnet, `1` | Production proxy and deployment receipt pending |
| FUNTOKEN (FUN) | Sepolia, `11155111` | Three recorded deployments; shared canonical address pending owner selection |
| Initial Vault AI recovery workflow | Ethereum mainnet, `1` | First supported claim contract and live connection pending validation |
| FUN discovery and development | Sepolia, `11155111` | Separate, explicitly selected testnet context |

Identify every asset by chain ID and full contract address. A token symbol alone is insufficient. Additional networks require their own supported provider and contract configuration.

## Development position

The smart-account product direction is confirmed. The private application repository currently contains a React/Vite presentation shell and runtime configuration; smart-account creation, signing, and recovery are implementation work ahead. This public repository contains product documentation and an architecture illustration.

Vault AI agent configuration, live provider connectivity, a deployed scan service, and tested claim support are tracked as separate milestones. Creating a Botpress playbook establishes its conversation structure.

## Explore the documentation

- [Current SafeVault framework](docs/SAFEVAULT_CURRENT_FRAMEWORK.md)
- [Vault Coin integration](docs/VAULT_COIN_FRAMEWORK.md)
- [BlackVault ecosystem](https://github.com/blackvault-opps/Blackvault-Public-Network-repo)
- [FUNTOKEN records](https://github.com/blackvault-opps/FUN-TOKEN-ERC-20-Report-Repo)
- [Vault AI workspace project](https://github.com/blackvault-opps/Vault-AI-Extension-Public-Deployment-Repo)

Updated 2026-09-18. Powered By Intelligent Design™.  
Copyright © 2026 BlackVault Public Network™. All rights reserved. No additional licence is granted by this documentation update.
