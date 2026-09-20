# Vault Coin — SafeVault Integration Framework

**Updated:** 2026-09-18

Vault Coin (VLT) is the production-token project within BlackVault Public Network. SafeVault is the planned holder-controlled account and asset interface through which users can display and interact with VLT once the production deployment and integration are recorded.

## Token model

| Property | Source-defined value |
| --- | --- |
| Name / symbol / decimals | Vault Coin / VLT / 18 |
| Initial supply | 100,000,000 VLT |
| Lifetime issuance ceiling | 420,000,000 VLT |
| Architecture | ERC-1967 proxy with UUPS implementation |
| Production network | Ethereum mainnet, chain ID `1` |
| Initial administrative-burn fee | 100 basis points (1%) |
| Production addresses | Pending confirmed deployment record |

The [canonical technical repository](https://github.com/blackvault-opps/Vault-Coin-VLT-project) defines supply accounting and token controls. The reviewed baseline is `80e8634ac4d0f1f16b34c94a046c6f1ae4a82527`. Burning reduces live supply while leaving cumulative issuance unchanged.

## Account and token responsibilities

SafeVault Homebase is the primary BlackVault smart-account experience. Existing wallets are optional secondary connections. Either account type may hold VLT on the correct network when supported; token ownership is recorded in the VLT contract ledger.

The VLT contract recognizes one owner address. Application membership, a Vault AI workspace role, or holding VLT does not confer token-owner authority. The intended owner is selected through the project's deployment configuration; the deployed contract's `owner()` result will establish the on-chain role.

Holder functions include transfers, approvals, `burn`, and allowance-based `burnFrom`. Owner functions include cap-bound minting, pause, blacklist, administrative burn, owner-directed transfer (`seize`), fee settings, proxy-held asset recovery, ownership succession, and upgrades.

The current source permits administrative burn and `seize` while paused and against blacklisted accounts. Ordinary transfers, minting, and holder burns follow pause/blacklist checks. These are token-contract behaviors, separate from control of a holder's wallet credentials.

## Three different recovery contexts

| Context | Meaning |
| --- | --- |
| SafeVault account recovery | Restore account access through the selected holder-authorized recovery design |
| Vault AI asset investigation | Identify protocol-specific entitlement or a supported asset-return path |
| VLT `recoverETH` / `recoverERC20` | Owner-only movement of assets held by the VLT proxy to its current owner |

The VLT recovery functions are limited to that proxy. VLT itself held by the proxy uses `seize` with its reason-hash record. These controls do not create a general public claim endpoint for unrelated contracts.

## Activation record

Before enabling VLT actions, record the chain ID, proxy address, implementation address/version, deployment receipt, matching ABI, and actual owner. Resolve amounts in 18-decimal base units and display the intended recipient, value, and estimated fees for holder review. Confirm the receipt and expected result after execution.

The production address remains pending in the reviewed source record. Historical compilation and test reports retain their original dates and commit scope. FUNTOKEN's Sepolia deployments are a separate token history.

See [SafeVault architecture](SAFEVAULT_CURRENT_FRAMEWORK.md) and [VLT controls](https://github.com/blackvault-opps/Vault-Coin-VLT-project/blob/main/CONTROL_MODEL.md).
