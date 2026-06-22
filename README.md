# web3-hackathon-2026-the-living-tombstone
Hackathon team repository for The Living Tombstone - [hackindia-team:web3-hackathon-2026:the-living-tombstone]


# 🪪 DocProof | On-Chain Skills & Credential Vault

**DocProof** is a decentralized, zero-knowledge verification layer that converts raw credentials (degrees, certifications, skills) into tamper-proof cryptographic facts anchored to the **Polygon** blockchain.

By executing all cryptographic operations strictly client-side, DocProof ensures that sensitive personal data never leaves the user's device. Only mathematical proofs (SHA-256 hashes) and verifiable metadata are transmitted to the decentralized ledger.

---

## ⛓️ Deep Dive: Polygon Blockchain Integration

The core value proposition of DocProof relies on **Polygon** (specifically targeting the Amoy Testnet, Chain ID: `0x13882`). Polygon was chosen as the Layer-2 scaling solution due to its EVM compatibility, near-zero gas fees, and lightning-fast block times, making it ideal for micro-transactions like credential anchoring.

**How the Polygon Integration Works Under the Hood:**

1. **Provider Connection:** DocProof interfaces directly with the browser's injected Web3 provider (MetaMask via `window.ethereum`).
2. **Network Enforcement:** Upon connection, the application automatically requests the wallet to switch to the specific Polygon network configuration (`eth_requestAccounts` and `wallet_switchEthereumChain`).
3. **Zero-Knowledge Hashing:** When a user uploads a credential, DocProof converts the file into an `ArrayBuffer` and uses the `crypto.subtle.digest` API to generate a strict **SHA-256 hash**. The actual file is *never* uploaded.
4. **Cryptographic Signing (Minting):** To issue the credential, DocProof requests a `personal_sign` transaction from the user's Polygon wallet. The user signs a deterministic message containing the file's hash and a precise timestamp.
5. **Ledger Anchoring:** The resulting cryptographic signature, the document's hash, and the user's public Polygon address (`0x...`) are committed to the public Supabase registry.
6. **Trustless Verification:** Any third party can independently verify the credential by recalculating the hash of the file and querying the ledger to confirm it was signed by the authorized Polygon address at the stated time.

---

## 🛠️ Technology Stack Breakdown

* **Frontend Architecture:** **React 18** (implemented directly via CDN for a zero-build-step prototype). State management handles complex asynchronous tasks like file buffering, Web3 wallet states, and real-time ledger updates.
* **Styling Engine:** **Tailwind CSS** heavily customized with raw CSS for hardware-accelerated 3D transforms (`transform-style: preserve-3d`), glassmorphism (`backdrop-filter: blur`), and dynamic CSS variables mapping mouse coordinates for lighting effects.
* **Decentralized Ledger:** **Supabase (PostgreSQL)**. Utilizes the Supabase real-time client to listen for `INSERT` events on the `registry` table, ensuring the UI updates instantly across all active nodes when a new credential is minted globally.
* **Web Cryptography API:** Utilizes native browser APIs (`window.crypto.subtle`) for military-grade AES-256-GCM encryption and SHA-256 hashing without external dependencies.
* **HTML5 Canvas & Web Audio API:** Used extensively for local file manipulation, image processing, byte visualization, and data sonification.

---

## ⚙️ Feature Breakdown: Core Protocol

The Core Protocol handles the primary ingestion, analysis, and fundamental security of the uploaded credential.

* **Shannon Entropy Analysis:** Reads the file's `Uint8Array` buffer to calculate mathematical randomness (entropy score out of 8.0). High scores indicate a file is compressed or properly encrypted, preventing the anchoring of corrupted data.
* **WebAuthn Bio-Link:** Triggers the device's native platform authenticator (TouchID, Windows Hello) via `navigator.credentials.create` to structurally bind a physical biometric approval to the digital issuance session.
* **GPS Anchoring:** Utilizes the HTML5 Geolocation API to fetch latitude and longitude, embedding the exact physical location of issuance into the credential's metadata.
* **AES-256 Lock:** Generates a dynamic 256-bit symmetric key and a 12-byte Initialization Vector (IV) to encrypt the raw file buffer locally before prompting a secure download.
* **Live Byte Frequency:** Maps the first 10,000 bytes of the file into a live 2D Canvas histogram, giving a visual footprint of the credential's binary structure.
* **Steganography Vault:** Encodes a secret user-defined text string and concatenates it directly to the end of the file's binary buffer (`Uint8Array.set()`), allowing hidden messages to pass undetected in standard file viewers.
* **Visual Noise (Watermarking):** Draws an image credential to a hidden canvas, injects calculated mathematical noise into the RGBA pixel array (`getImageData`), and re-exports the image to deter unauthorized scraping.
* **EXIF Sanitizer:** Strips hidden tracking data (camera models, GPS tags) by painting the image to a blank canvas and re-encoding it as a pure PNG file.
* **File Sharder:** Divides the `ArrayBuffer` into three equal-sized, unreadable binary chunks (`fileBuffer.slice`) for distributed physical or cloud storage.
* **Memory Wipe Sequence:** A configurable JavaScript timeout that permanently nullifies the active file buffer (`setFileBuffer(null)`) and purges it from the session state to prevent memory scraping.
* **IPFS CIDv1 Generation:** Simulates the creation of a Content Identifier base58 string, preparing the file for future decentralized storage on the InterPlanetary File System.

---

## ⚡ Feature Breakdown: Advanced Arsenal

The Advanced Arsenal utilizes experimental web APIs for extreme obfuscation and multi-factor verification techniques.

* **Voice Signature:** Accesses the microphone via `navigator.mediaDevices.getUserMedia`, records a short vocal cadence, and functionally links the issuance to the user's audio print.
* **Data Sonification:** Translates the raw binary buffer of the credential into audible frequencies using the `AudioContext` API. Bytes dictate the Hz of generated sine/triangle oscillator waves, allowing users to "hear" their data.
* **3D Byte Topology:** Generates a real-time, hardware-accelerated 3D canvas mapping of byte distribution using trigonometric offsets (`Math.sin`), visually representing cryptographic depth.
* **Glitch Obfuscation:** Deterministically slices horizontal segments of an image's pixel data and offsets them by random X-coordinates to visually scramble the asset prior to encryption.
* **Optical Transmission:** Manipulates DOM background colors rapidly using `requestAnimationFrame` to visually broadcast the file's hash via high-frequency screen flashes (intended for machine-camera reception).
* **Rhythm Lock:** Tracks the precise keydown/keyup timestamps as a user types a passphrase. The system validates the *cadence* and *dwell time* of the keystrokes rather than just the characters themselves.
* **Parity Generator:** Creates a secondary redundancy file by iterating through the original buffer and applying an XOR bitwise operation (`^`) against a seeded integer.
* **Chrono-Lock:** Applies a pseudo-time-lock to the UI state, blocking further cryptographic operations or anchoring until a specified physical world time is reached.
* **AR HUD Overlay:** Accesses the device's rear-facing camera to render a real-time video feed underneath the UI components using the `mix-blend-mode: screen` CSS property, creating an augmented reality terminal environment.

---

## 📐 System Architecture & Data Flow

1. **Local Ingestion:** User drops `certificate.pdf` -> `FileReader` API converts to `ArrayBuffer`.
2. **Processing:** `ArrayBuffer` is passed to various modules (Hashing, Canvas API, Crypto API) strictly in local memory.
3. **Web3 Handshake:** User clicks "Mint" -> App requests `personal_sign` from Polygon Wallet.
4. **Ledger Commit:** Signed payload + SHA-256 Hash -> Sent via Supabase REST API -> Inserted into PostgreSQL `registry`.
5. **Global Sync:** Supabase Realtime pushes the new `registry` row back to all connected clients instantly.


