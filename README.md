# 🧱 Solana Token Creation Guide

This guide provides step-by-step instructions for creating a token on the **Solana blockchain** using the **Solana CLI** and **SPL Token CLI** on the **Devnet**.  
It includes setting **mint authority**, **freeze authority**, and initializing **token metadata**.

---

## 📋 Steps

| Step                          | Command |
|-------------------------------|---------|
| **Install Solana CLI**        | `sh -c "$(curl -sSfL https://release.solana.com/v1.18.14/install)"` |
| **Install SPL Token CLI**     | `cargo install spl-token-cli` |
| **Set Devnet**                | `solana config set --url https://api.devnet.solana.com` |
| **Create New Wallet**         | `solana-keygen new --outfile ~/brics-keypair.json` |
| **Set Wallet for CLI**        | `solana config set --keypair ~/brics-keypair.json` |
| **Airdrop SOL on Devnet**     | `solana airdrop 2` |
| **Create Token with Authorities** | `spl-token --program-id TokenzQdBNbLqP5VEhdkAS6EPFLC1PHnBqCXEpPxuEb create-token --enable-metadata --mint-authority ~/brics-keypair.json --freeze-authority ~/brics-keypair.json` |
| → 🧠 *This creates the token mint and sets your wallet as both mint authority and freeze authority.* ||
| **Initialize Token Metadata** | `spl-token --program-id TokenzQdBNbLqP5VEhdkAS6EPFLC1PHnBqCXEpPxuEb initialize-metadata <MINT> "BRICS" "BRICS" "<URI>"` |
| → 🧠 *Metadata includes name, symbol, and a JSON URI (hosted on IPFS or Arweave).* ||
| **Create Associated Token Account** | `spl-token --program-id TokenzQdBNbLqP5VEhdkAS6EPFLC1PHnBqCXEpPxuEb create-account <MINT>` |
| → 🧠 *This is the account that holds the tokens.* ||
| **Mint Tokens to Account** | `spl-token --program-id TokenzQdBNbLqP5VEhdkAS6EPFLC1PHnBqCXEpPxuEb mint <MINT> 10000000 <ACCOUNT>` |
| → 🧠 *This mints tokens to your token account.* ||
| **Check Token Accounts**      | `spl-token --program-id TokenzQdBNbLqP5VEhdkAS6EPFLC1PHnBqCXEpPxuEb accounts` |
| **Check Token Account Info**  | `spl-token --program-id TokenzQdBNbLqP5VEhdkAS6EPFLC1PHnBqCXEpPxuEb account-info <ACCOUNT>` |
| **Freeze Token Account (Optional)** | `spl-token --program-id TokenzQdBNbLqP5VEhdkAS6EPFLC1PHnBqCXEpPxuEb freeze <ACCOUNT>` |
| → 🧠 *Freezing prevents transfers from the token account.* ||
| **Thaw Token Account (Optional)**   | `spl-token --program-id TokenzQdBNbLqP5VEhdkAS6EPFLC1PHnBqCXEpPxuEb thaw <ACCOUNT>` |
| **Transfer Tokens (Optional)**      | `spl-token --program-id TokenzQdBNbLqP5VEhdkAS6EPFLC1PHnBqCXEpPxuEb transfer <MINT> 100 <RECIPIENT_TOKEN_ACCOUNT>` |

---

## 📝 Notes

- Replace `<MINT>` with the mint address returned by the **Create Token** step.
- Replace `<ACCOUNT>` with the address returned by the **Create Account** step.
- Replace `<URI>` with a publicly accessible JSON metadata URL (hosted on IPFS, Arweave, or GitHub Pages).
- The `--mint-authority` allows minting more tokens in the future.
- The `--freeze-authority` allows freezing/unfreezing token accounts.
- You can remove authorities later using:
  - 🔒 Remove Mint Authority:  
    `spl-token authorize <MINT> mint --disable`
  - ❄️ Remove Freeze Authority:  
    `spl-token authorize <MINT> freeze --disable`
- Requires [Rust](https://www.rust-lang.org/tools/install) and Cargo to use `spl-token-cli`.

---

## ✅ Example Token Metadata JSON (`<URI>`)

```json
{
  "name": "BRICS",
  "symbol": "BRICS",
  "decimals": 9,
  "description": "BRICS Token on Solana Devnet",
  "image": "https://example.com/logo.png",
  "attributes": [],
  "properties": {
    "files": [
      {
        "uri": "https://example.com/logo.png",
        "type": "image/png"
      }
    ],
    "category": "image",
    "creators": [
      {
        "address": "<YOUR_WALLET_ADDRESS>",
        "share": 100
      }
    ]
  }
}
