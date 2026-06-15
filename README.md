# web3-hackathon-2026-the-living-tombstone
Hackathon team repository for The Living Tombstone - [hackindia-team:web3-hackathon-2026:the-living-tombstone]
## 🚀 Live Prototype

🔗 Prototype: [(https://the-living-tombstone-web3-hackathon.vercel.app/)]

# 🪪 DocProof | Skills On-Chain Platform

**DocProof** is a decentralized credentialing verification layer designed for trustless hiring and verifiable digital identity. It directly addresses the need for an on-chain platform that issues, stores, and instantly verifies skills and certifications using the **Polygon Blockchain**.

By converting raw credential files (PDFs, images) into tamper-proof cryptographic fingerprints (SHA-256 hashes) and anchoring them on-chain, DocProof ensures absolute proof of skill existence at a precise moment in history without storing sensitive personal data.

---

## 🎯 Problem Statement Addressed

**Problem Statement 2: Skills On-Chain Platform**

* ✅ **Issue certifications as on-chain records:** Users can upload documents, which are hashed and "minted" using a cryptographic signature tied to their Web3 wallet.
* ✅ **Store and verify via Polygon:** Credentials are tied to a Polygon wallet address (Chain ID `0x13882` / Amoy Testnet) and anchored via signed transactions.
* ✅ **Third-party Integration:** Built on an open, real-time Supabase ledger that allows any platform to query a document's hash to verify authenticity.
* ✅ **Instant & Trustless Verification:** Drag-and-drop a file to instantly recalculate its hash and check the decentralized registry for a match or tamper warning.

---

## ✨ Key Features & Architecture

DocProof goes beyond simple hashing. It includes a complete **"Security Arsenal"** module to process, secure, and obfuscate data locally in the browser before anchoring.

### 🔗 1. Core On-Chain Protocol

* **Zero-Knowledge Architecture:** The actual credential file never leaves the user's device. Only the calculated SHA-256 hash is transmitted and stored on the ledger.
* **Web3 Wallet Integration:** Connects directly to MetaMask/Ethers to switch to the Polygon network and sign credential issuance transactions.
* **Decentralized Ledger:** A real-time, public registry of all minted hashes, tied to author addresses, timestamps, and metadata.

### 🛡️ 2. Local Cryptographic Arsenal

All processing is done **client-side** using standard Web APIs for maximum privacy:

* **AES-256 GCM Encryption:** Lock credentials locally before sharing them.
* **WebAuthn Biometrics:** Tie a credential issuance to physical device biometrics (TouchID/FaceID).
* **File Sharding:** Split documents into 3 unreadable binary chunks for distributed storage.
* **Steganography:** Inject hidden, encrypted text directly into a file's raw binary data.
* **EXIF Sanitization:** Strip tracking metadata and GPS data from certificate images.
* **Neural Watermarking:** Apply mathematical visual noise to deter unauthorized copying.
* **Self-Destruct Memory:** Timers that wipe the file buffer from active memory and update the public ledger.

### 📡 3. Advanced Verification Modules

* **Shannon Entropy Analysis:** Detects if a document is compressed or encrypted based on byte randomness.
* **Live Byte Topology & Sonification:** Visual and audio representation of a document's raw binary buffer.
* **GPS Anchoring:** Embeds verifiable location coordinates into the on-chain metadata at the time of issuance.

---

## 🛠️ Technology Stack

* **Frontend:** React 18 (via CDN), Tailwind CSS.
* **Styling:** Highly custom CSS with 3D hover effects, glassmorphism, hardware-accelerated animations, and custom cursors.
* **Blockchain/Web3:** Ethers.js/MetaMask (`window.ethereum`) for Polygon network interactions and message signing.
* **Backend/Ledger:** Supabase (PostgreSQL) for real-time ledger synchronization and Node authentication.
* **Cryptography:** Web Crypto API (`crypto.subtle`) for SHA-256 hashing and AES-GCM encryption.

---

## 🚀 Quick Start & Installation

Because DocProof was built for rapid deployment and runs primarily client-side, the entire application is bundled into a single file. No `npm install` or complex build steps are required.

### Prerequisites

1. A modern web browser (Chrome, Edge, Brave).
2. **MetaMask** extension installed and configured.
3. A local development server (like VS Code's "Live Server" extension).

### Running the App

1. Clone the repository:
```bash
git clone https://github.com/yourusername/docproof.git
cd docproof

```


2. Serve the `index.html` file. **Note:** Due to browser security policies regarding Web Crypto and WebAuthn APIs, you *must* run this over `localhost` or `127.0.0.1` (do not just double-click the file).
* Using Python: `python -m http.server 8000`
* Using Node/npx: `npx serve .`
* Using VS Code: Right-click `index.html` -> "Open with Live Server"


3. Navigate to `http://localhost:8000` in your browser.

---

## 📖 Usage Guide

### Issuing a Credential

1. Click **"Connect Polygon"** in the top navigation to link your MetaMask wallet.
2. Click **"Initialize Node"** to create a local Supabase session (Optional, falls back to anonymous node).
3. Drag and drop your digital certificate (PDF, PNG, JPEG) into the **Active Terminal**.
4. Wait for the system to scan the signal and generate the SHA-256 identifier.
5. (Optional) Apply any local security layers from the **Security Modules** panel (e.g., GPS Anchor, Biometrics).
6. Click **"Mint to Polygon"**. Sign the transaction in your wallet to anchor the credential.

### Verifying a Credential

1. Anyone can navigate to the DocProof terminal.
2. Drag and drop the credential file they received.
3. The system will hash the file locally and instantly query the real-time Supabase ledger.
4. The terminal will display **"Verified Authentic"** (with Polygon address data) or **"Unregistered Signal/Tamper Detected"** if a single byte has been altered.

---

## 🔌 Third-Party Integration

DocProof is designed to be highly interoperable. Third-party HR platforms, universities, or freelancing websites can integrate DocProof verification by:

1. **Direct Smart Contract Querying (Future Scope):** Verifying the hash directly against the deployed Polygon smart contract.
2. **Ledger Webhooks:** Subscribing to the public Supabase channel (`public:registry`) to get real-time updates when new credentials are submitted.
3. **Local Hash Verification:** Platforms can implement their own standard SHA-256 hashing on file uploads and simply check the output against the DocProof public ledger API.



