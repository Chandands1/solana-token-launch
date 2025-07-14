# 🧱 Solana Token Creation Guide

This guide provides step-by-step instructions for creating a token on the Solana blockchain using the Solana CLI and SPL Token CLI on the **Devnet**.

---

## 📋 Steps

| Step                 | Command |
|----------------------|---------|
| **Install Solana CLI** | `sh -c "$(curl -sSfL https://release.solana.com/v1.18.14/install)"` |
| **Install SPL Token CLI** | `cargo install spl-token-cli` |
| **Set Devnet** | `solana config set --url https://api.devnet.solana.com` |
| **New Wallet** | `solana-keygen new --outfile ~/brics-keypair.json`<br>`solana config set --keypair ~/brics-keypair.json` |
| **Airdrop** | `solana airdrop 2` |
| **Create Token** | `spl-token --program-id TokenzQdBNbLqP5VEhdkAS6EPFLC1PHnBqCXEpPxuEb create-token --enable-metadata` |
| **Initialize Metadata** | `spl-token --program-id TokenzQdBNbLqP5VEhdkAS6EPFLC1PHnBqCXEpPxuEb initialize-metadata <MINT> "BRICS" "BRICS" "<URI>"` |
| **Create Account** | `spl-token --program-id TokenzQdBNbLqP5VEhdkAS6EPFLC1PHnBqCXEpPxuEb create-account <MINT>` |
| **Mint** | `spl-token --program-id TokenzQdBNbLqP5VEhdkAS6EPFLC1PHnBqCXEpPxuEb mint <MINT> 10000000 <ACCOUNT>` |
| **Check Balance** | `spl-token --program-id TokenzQdBNbLqP5VEhdkAS6EPFLC1PHnBqCXEpPxuEb accounts` |

---

## 📝 Notes

- Replace `<MINT>` with the token mint address generated during the **"Create Token"** step.
- Replace `<URI>` with the metadata URI for your token (e.g., a JSON file hosted on IPFS or Arweave).
- Replace `<ACCOUNT>` with the token account address created in the **"Create Account"** step.
- Ensure you have **Rust** and **Cargo** installed for the SPL Token CLI.
- The **airdrop** provides 2 SOL on Devnet for testing purposes.

---

Happy Building on Solana 🚀
