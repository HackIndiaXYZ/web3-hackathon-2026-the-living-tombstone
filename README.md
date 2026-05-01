# web3-hackathon-2026-the-living-tombstone
Hackathon team repository for The Living Tombstone - [hackindia-team:web3-hackathon-2026:the-living-tombstone]
## 🚀 Live Prototype

🔗 Prototype: [(https://doc-proof.vercel.app/)]

🎥 Demo Video:[(https://drive.google.com/file/d/1DzOD7tMd-hvG7n-NU0sHSNhZu2QCUpM3/view?usp=sharing)]

# DocProof | The Cryptographic Standard

## 📖 Overview & Architectural Philosophy
DocProof is an immutable verification layer designed for the post-truth era. Its primary directive is to convert standard digital assets (documents, images, audio) into absolute cryptographic facts, ensuring their integrity is secured across time and space. 

The application operates on a strict **Zero-Knowledge, Zero-Trust Architecture**. It never uploads or stores actual files on a server. Instead, all processing—including cryptographic hashing, biometric binding, and byte-level manipulation—happens entirely client-side within the browser's memory buffer. The platform utilizes **Temporal Stamping** and decentralized registry principles to provide undeniable proof of an asset's existence, state, and ownership at a precise moment in history.

---

## 🛠 Detailed Technology Stack

DocProof operates as a pure client-side Single Page Application (SPA) that requires no build steps (Webpack/Vite) or server-side rendering. It leverages native browser APIs and Content Delivery Networks (CDNs) to achieve native-app capabilities.

### 1. Core Frontend & Compilation
* **React 18 (UMD Build):** Utilized via CDN for component-based UI rendering and state management without a Node.js environment.
* **Babel (Standalone):** Runs directly in the browser to transpile JSX and modern ES6+ JavaScript on the fly.
* **Architecture:** "Zero-Build SPA"—the entire application is contained within a single `index.html` file, ensuring maximum portability and execution in air-gapped environments.

### 2. UI, UX, & Styling Engine
* **Tailwind CSS:** Integrated via CDN for utility-first styling.
* **Custom CSS & Animations:** Heavily customized with `@keyframes` for cryptographic processing animations, scanning effects, and UI feedback loops.
* **Visual Effects:** Implements 3D CSS `transform` arrays, `backdrop-filter` glassmorphism (`liquid-glass`), and mathematically generated luxury noise overlays to prevent visual scraping.
* **Typography:** Google Fonts (Anton for bold headers, Condiment for cursive signatures, Space Grotesk for technical data) and system monospace fonts for hex/byte data.
* **Iconography:** Lucide Icons for lightweight, consistent vector graphics.

### 3. Cryptographic & Security Layer (Native APIs)
* **Web Crypto API (`crypto.subtle`):** The backbone of the application. 
  * Uses **SHA-256** for deterministic file fingerprinting.
  * Uses **AES-256-GCM** for military-grade symmetric encryption of file buffers.
* **WebAuthn API:** Interfaces directly with the device's hardware TPM/Secure Enclave (Apple TouchID/FaceID, Windows Hello) to generate cryptographic signatures bound to the user's physical biometrics.

### 4. Hardware & Sensor Integration
* **Geolocation API:** Fetches high-precision GPS coordinates (latitude/longitude) to create spatial anchors for document verification.
* **MediaDevices API (`getUserMedia`):** 
  * **Microphone Access:** Captures audio streams for voice biometric sealing.
  * **Camera Access:** Powers the AR Vault Projection, mapping digital HUD elements over a live rear-facing camera feed.
* **Device Orientation API:** Listens to gyroscope data (`alpha`, `beta`, `gamma`) to generate true physical entropy for cryptographic seeding.

### 5. Media, Canvas & Audio Processing
* **HTML5 Canvas API:** Used extensively for low-level byte manipulation:
  * Renders real-time 2D histograms of byte frequency (Forensic Ghost Images).
  * Calculates and renders 3D topology grids based on file byte arrays.
  * Processes image sanitization by stripping EXIF data and redrawing pixels.
  * Injects steganographic payloads and visual neural noise into image matrices.
* **Web Audio API:** Synthesizes raw binary file data into audible frequencies using custom oscillators (sine/triangle waves) for data sonification.

### 6. Backend & Ledger (Supabase)
* **PostgreSQL / Supabase:** Acts as the public, append-only verification registry.
* **Real-time Syncing:** Uses Supabase's WebSocket connections to instantly broadcast new document hashes to the public ledger feed.
* **Authentication:** Handles anonymous or authenticated sessions via JWTs.

---

## 🔌 Database Connection Protocol

The application connects to a Supabase backend to sync the public ledger. The following credentials are used to establish the client connection:

* **Supabase REST URL:** `[https://rjnolzmhitlcawtsgvwk.supabase.co](https://rjnolzmhitlcawtsgvwk.supabase.co)`
* **Anon Public Key:** `eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJzdXBhYmFzZSIsInJlZiI6InJqbm9sem1oaXRsY2F3dHNndndrIiwicm9sZSI6ImFub24iLCJpYXQiOjE3NzcyMDcxNDEsImV4cCI6MjA5Mjc4MzE0MX0.TMatVjTaxuPRCxUDdfmXJ2xSaxNY32rzNZa91ghKGfI`
* ## 🔌 Database Configuration

To use your own backend, update the following constants in `index.html`:

```javascript
const supabaseUrl = 'https://rjnolzmhitlcawtsgvwk.supabase.co';
const supabaseKey = 'eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJzdXBhYmFzZSIsInJlZiI6InJqbm9sem1oaXRsY2F3dHNndndrIiwicm9sZSI6ImFub24iLCJpYXQiOjE3NzcyMDcxNDEsImV4cCI6MjA5Mjc4MzE0MX0.TMatVjTaxuPRCxUDdfmXJ2xSaxNY32rzNZa91ghKGfI';
```

### Required Database Schema
Create a table named `registry` in your Supabase SQL editor:

```sql
create table registry (
  id uuid default uuid_generate_v4() primary key,
  created_at timestamp with time zone default timezone('utc'::text, now()) not null,
  name text,
  hash text,
  author text,
  metadata jsonb
);
```

> **⚠️ Security Note:** Exposing the `anon` key in client-side code is standard for Supabase, but it requires strict **Row Level Security (RLS)** policies configured on the PostgreSQL database to ensure malicious actors cannot overwrite or delete registry entries.

---

## ⚙️ Core Protocol Modules

These features constitute the standard toolkit for file analysis, sanitization, and cryptographic locking.

* **Shannon Entropy Monitor:** Analyzes the `Uint8Array` buffer of a file to calculate its mathematical randomness. High entropy (approaching 8.0) indicates the file is likely compressed or encrypted, while low entropy reveals plain text or empty space.
* **WebAuthn Bio-Link:** Triggers a platform authenticator prompt (e.g., fingerprint reader), extracting the resulting cryptographic assertion and appending it to the document's verification metadata.
* **GPS Anchor (Geo-Fence):** Binds physical latitude and longitude coordinates to the file's SHA-256 signature, proving *where* the document was sealed.
* **AES-256 Lock (Time Capsule):** Takes the raw file buffer, encrypts it locally using AES-GCM with a user-provided or auto-generated key, and triggers a browser-level download of the ciphered asset.
* **Live Byte Frequency (Forensic Image):** Translates the first 10,000 bytes of a file into visual coordinates, drawing a live 2D plot on a Canvas to detect data anomalies or hidden payloads.
* **Steganography Vault:** Injects encrypted or plaintext hidden messages directly into the least significant bits or EOF space of the raw binary data, exporting the modified asset.
* **Visual Noise (Neural Watermark):** Prevents AI model scraping by injecting mathematically calculated, invisible (or stylized) noise into the pixel data of an image using Canvas manipulation.
* **EXIF Sanitizer:** Defeats metadata tracking by drawing an uploaded image to a temporary off-screen Canvas and re-encoding it natively, entirely stripping camera data, timestamps, and GPS tags.
* **File Sharder (Zero-Trust):** Mathematically slices the file's binary buffer into three unreadable, fragmented chunks (shards) for distributed, secure cold storage.
* **Decoy Maker:** Generates a synthetic file that perfectly matches the exact byte-size of the original asset, but fills it entirely with randomized cryptographic noise.
* **Memory Wipe (Self-Destruct):** A security protocol that holds the file strictly in RAM. Upon a predefined timer expiring (1 to 10 minutes), the JavaScript garbage collector is forced to release the buffer, wiping it from the browser state.
* **IPFS CID Generator:** Computes the simulated Content Identifier (CIDv1 Multihash), projecting exactly what the file's address will be once deployed to the decentralized InterPlanetary File System.

---

## ⚡️ Advanced Arsenal (Experimental Modules)

These features push the boundaries of browser capabilities, exploring multi-sensory data representation and obfuscation.

* **Voice Signature (Biometric Seal):** Captures a 3-second `MediaStream` audio recording, converts the audio buffer to an array, and hashes it into the document's permanent seal.
* **Data Sonification:** Translates a file's raw binary sequence into real-time audio. By mapping byte values (0-255) to pitch and frequency via the Web Audio API, users can literally "listen" to their data.
* **3D Byte Topology Grid:** Maps the cryptographic density of a file onto a 3D HTML Canvas matrix. Byte values dictate the size, height, and offset of rendered nodes, creating a unique physical landscape of the data.
* **Glitch Obfuscation:** Deterministically slices, shifts, and offsets vertical chunks of an image's pixel array, creating visual chaos that renders the image unreadable without the specific decryption algorithm.
* **Optical Transmission (Li-Fi Sim):** Translates the document's SHA-256 hash into a sequence of binary flashes (black/white) on the screen, designed to be read by a high-speed camera receiver in air-gapped environments.
* **Keystroke Dynamics:** A behavioral biometric lock. It tracks the speed, rhythm, and cadence of a user typing a specific passphrase, acting as a secondary layer of authentication before allowing decryption.
* **Redundancy Parity Generator:** Creates an XOR parity buffer using a deterministic random seed against the file's binary array, creating mathematical redundancy for data recovery.
* **Chrono-Lock:** A pseudo-lock feature designed to mathematically tie the decryption algorithm to a specific UNIX timestamp, theoretically preventing access until the timeline matches.
* **AR Vault Projection:** Requests mobile camera access to project a futuristic Heads-Up Display (HUD) and the file's cryptographic hash floating over the user's physical environment.
* **Gyroscope Entropy:** Leverages mobile device sensors (`deviceorientation`) to generate a highly secure, truly random entropy seed based on the physical, unpredictable hand movements of the user.
