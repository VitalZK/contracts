# VitalZK Contracts: On-Chain Verification Layer

> **Decentralized Medical Credentialing with Zero-Knowledge Privacy on Stellar.**


## 📋 Project Description

**VitalZK-Contracts** houses the Soroban smart contracts that power the VitalZK protocol. It serves as the "Source of Truth" for the network, managing a registry of authorized medical issuers and providing a gas-efficient verification gateway for ZK-proofs.

### Key Features

  * **Issuer Registry:** A decentralized list of hospitals and labs authorized to sign medical data.
  * **ZK-Proof Verifier:** High-performance verification logic using the **BN128/BN254** pairing checks.
  * **Atomic Revocation:** Allows issuers to invalidate compromised credentials without revealing patient identity.
  * **Gas Optimization:** Utilizes native Soroban host functions for cryptographic primitives to minimize transaction costs.

### Tech Stack

  * **Language:** Rust
  * **Platform:** Soroban (Stellar Smart Contracts)
  * **SDK:** `soroban-sdk` v20+
  * **Cryptography:** Poseidon Hashing, BN254 Elliptic Curve

-----

## 📂 Folder Structure

```text
vitalzk-contracts/
├── contracts/
│   ├── issuer_registry/      # Manages authorized hospital identities
│   │   └── src/lib.rs
│   └── proof_verifier/       # Entry point for ZK-SNARK validation
│       └── src/lib.rs
├── packages/
│   └── vitalzk-interface/    # Shared types and traits
├── Makefile                  # Build and deployment automation
└── Cargo.toml                # Workspace configuration
```

-----

## ⚙️ Installation

### Prerequisites

1.  **Rust & Cargo:** [Install Rust](https://rustup.rs/)
2.  **Stellar CLI:** \`\`\`bash
    cargo install --locked stellar-cli --features opt
    ```
    ```
3.  **WASM Target:**
    ```bash
    rustup target add wasm32-unknown-unknown
    ```

### Setup

1.  Clone the repository:
    ```bash
    git Clone https://github.com/VitalZK/vitalzk-contracts.git
    cd vitalzk-contracts
    ```
2.  Build the contracts:
    ```bash
    stellar contract build
    ```

-----

## 🚀 Usage

### Deploying to Testnet

```bash
stellar contract deploy \
  --wasm target/wasm32-unknown-unknown/release/vitalzk_registry.wasm \
  --source-account my-identity \
  --network testnet
```

### Verification Snippet (Rust)

To verify a proof on-chain, call the `verify` function with the proof bytes and public inputs:

```rust
let is_valid = client.verify_proof(
    &proof_bytes,
    &vec![&env, hospital_pubkey_hash, current_timestamp]
);
assert!(is_valid);
```

-----

## 🛠️ Configuration

The following environment variables are recommended for deployment and testing:

| Variable | Description | Default |
| :--- | :--- | :--- |
| `STELLAR_NETWORK` | Target network (testnet/futurenet/mainnet) | `testnet` |
| `ADMIN_SECRET` | Secret key for the contract administrator | `None` |
| `SOROBAN_RPC_URL` | Endpoint for the Soroban RPC node | `https://soroban-testnet.stellar.org` |

-----

## 📄 License

This project is licensed under the **MIT License**. See the [LICENSE](./LICENSE) file for details.
