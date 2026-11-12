# 🕵️ Hidden Chat

**Hidden Chat** is a privacy-first, real-time steganography messenger, pixel-level LSB image steganography studio, and standalone emoji encoder/decoder web application created by [**@mrabr381**](https://github.com/mrabr381). It lets users hide password-encrypted messages, original-quality photos, voice notes, and secret documents inside ordinary emojis and casual everyday phrases (`\u200D` / `\u200C` zero-width carriers) or inside image pixels, and chat in real time inside zero-metadata hashed rooms.

- 🌐 **Live Site Demo:** [https://hidden-chaat.netlify.app/](https://hidden-chaat.netlify.app/)
- 👨‍💻 **Author GitHub:** [https://github.com/mrabr381](https://github.com/mrabr381)

---

## ✨ Key Features

### 1. 💬 Real-Time Encrypted Stego Chat & UX
- **🕵️ Dual Chat Modes (Stego Mode & Simple Chat):**
  - **Stego Mode:** Hides your encrypted message inside an innocent cover phrase (e.g., `[🤖] Aaj mausam kafi acha hai!`) or an **Emoji-Only** carrier (`[🤖]`).
  - **Simple Chat Mode:** Works like a clean, direct real-time chat room while keeping every message encrypted in the background.
- **🟢 Live Online Presence & Typing Indicator:** Displays real-time active room member count (`🟢 X Online`) and an encrypted typing indicator without exposing user identities in the database.
- **↩️ Encrypted Reply Quotes & Single-Message Delete:** Quote-reply to any message (with the quote encrypted inside the payload) or delete individual messages for everyone (available to the message sender and the Room Admin).
- **🔗 Zero-Knowledge Invite Link & Visual Matrix:** Generate shareable `#room=...` invite links (where the room name stays in the URL hash fragment and is never sent to any web server) along with a custom visual room matrix.
- **👑 Portable Room Creator (Admin) Protection:** Only the original room creator can clear the entire room history for everyone. Supports **Portable Admin Login** (`Nickname + Room Password` or `Nickname#pin` like `Ali#786`) so the creator retains Admin rights across any device, browser, or Incognito session.
- **👥 Same-Nickname Disambiguation:** Every user receives a unique cryptographic ID tag (e.g., `Ali #A9F2`), preventing collisions even if multiple users pick the same nickname.

### 2. 🔥 Advanced Privacy & Self-Destruct Suite
- **🔥 Burn-on-Read (1-Time View Messages):** Optional self-destruct mode that starts a live 10-second countdown only after a receiver unlocks and reads the message, then permanently deletes it from Firebase and local storage.
- **🎭 Decoy / Dual Password (Duress Mode):** Attach a secondary *Fake Password* and *Fake Message* to any chat message or encoded emoji. If forced to reveal your password, entering the decoy password unlocks the harmless cover message while keeping the real secret text and media completely hidden.
- **🛡️ Auto Tab-Blur & Panic Stealth Mode (`Esc` Key & 15-Min Auto-Lock):**
  - **Auto-Blur Shield:** Automatically blurs the entire chat feed and decoded outputs the instant you switch tabs, minimize the browser, or click outside the window.
  - **Panic Key (`Esc`):** Pressing `Esc` (or 15 minutes of inactivity) immediately switches all bubbles back to innocent cover text.
- **🛡️ App-Exclusive Decoder Lock:** Uses bit-stream scrambling + dual-layer key derivation (`PBKDF2` 210,000 SHA-256 iterations + `AES-256-GCM`) so external zero-width decoders and AI tools cannot extract or read hidden payloads.

### 3. 🖼️ Multimedia Vault & Image-in-Image LSB Steganography
- **🖼️ Original-Quality Secret Photo Injection:** Attach PNG, JPG, WEBP, or GIF images—delivered in 100% original quality via an encrypted media vault with **Full-Screen Lightbox Preview** and **One-Click Original Quality Download**.
- **🎙️ Encrypted Voice Notes in Emoji:** Record up to 15-second voice notes directly from your browser microphone (`MediaRecorder` API), automatically encrypted with `AES-256-GCM` and playable inside the decrypted chat bubble or Decoder tab.
- **📄 Encrypted Secret Document / File Attachment:** Hide `.pdf`, `.txt`, `.zip`, `.doc/.docx`, `.csv`, or `.json` files (up to 2.5 MB) inside an emoji carrier and download them with their original filename upon decryption.
- **🖼️ Image-in-Image Pixel Steganography (LSB Engine):** A dedicated 4th tab that hides password-encrypted secret messages inside the actual RGB pixel Least Significant Bits (LSB) of any PNG/JPG image, exports a lossless Stego PNG, and lets you send it directly to Live Chat or decode it anytime.
- **📲 Installable Mobile & Desktop App (PWA):** Includes a Web App Manifest (`manifest.json`) and offline Service Worker (`sw.js`) so users can install **Hidden Chat** on Android, iOS, Windows, or macOS directly from the browser.

---

## 📋 Requirements

To run or deploy **Hidden Chat**, you only need:

1. **A Modern Web Browser:** Chrome, Edge, Brave, Firefox, or Safari (supports the native Web Crypto API `window.crypto.subtle` and `MediaRecorder`).
2. **A Free Firebase Account (Optional for Live Multi-Device Cloud Sync):** [Firebase Spark Plan (Free Tier)](https://console.firebase.google.com/) for Realtime Database. Without Firebase configured, the app automatically runs in **Instant Local / Multi-Tab Demo Mode**.
3. **Node.js (v18+ Optional):** Only needed if you want to deploy from your terminal using `firebase-tools` or `netlify-cli`. (No Node.js is required if you use **Netlify Drag & Drop** or **GitHub Pages**).

---

## ⚡ Quick Clone & Run Locally

```bash
git clone https://github.com/mrabr381/hidden-chat.git
cd hidden-chat
# Open index.html directly in your browser or serve locally:
npx serve .
```

---

## 🗄️ Free Firebase Realtime Database Setup Guide

Follow these steps to create your own free real-time database and connect it to **Hidden Chat**:

### Step 1: Create a Firebase Project & Realtime Database
1. Open the [Firebase Console](https://console.firebase.google.com/) and click **Create a project** (you can disable Google Analytics for faster setup).
2. In the left sidebar, go to **Build > Realtime Database** and click **Create Database**.
3. Select your preferred server region (e.g., `United States` or `Europe`) and choose **Start in test mode**, then click **Enable**.

### Step 2: Copy Your Database URL
1. Inside the **Realtime Database** view, copy your database URL at the top of the data tree (for example: `https://your-project-default-rtdb.firebaseio.com`).
2. Connect it to **Hidden Chat** using **either** of these two methods:
   - **Method A (No Code Edit — Via UI):** Open the live app, click **🌐 Custom Server** in the top bar, paste your `https://...firebaseio.com` URL, and click **Connect Custom DB**.
   - **Method B (Self-Hosted Code Config):** Open `index.html`, find `DEFAULT_FIREBASE_CONFIG`, and paste your project credentials:
     ```javascript
     const DEFAULT_FIREBASE_CONFIG = window.__HIDDEN_CHAT_FIREBASE_CONFIG__ || {
       apiKey: "YOUR_FIREBASE_API_KEY",
       authDomain: "YOUR_PROJECT_ID.firebaseapp.com",
       databaseURL: "https://YOUR_PROJECT_ID-default-rtdb.firebaseio.com",
       projectId: "YOUR_PROJECT_ID",
       storageBucket: "YOUR_PROJECT_ID.firebasestorage.app",
       messagingSenderId: "YOUR_SENDER_ID",
       appId: "YOUR_APP_ID"
     };
     ```
     *(Tip: Never commit your private API keys to a public GitHub repository—use environment injection during build or connect via the `🌐 Custom Server` modal).*

### Step 3: Apply Security Rules (`database.rules.json`)
In the Firebase Console, open **Realtime Database > Rules**, paste the contents of `database.rules.json` from this repository, and click **Publish**:

```json
{
  "rules": {
    ".read": false,
    ".write": false,
    "rooms": {
      "$roomHash": {
        ".read": "$roomHash.matches(/^r_[0-9a-f]{24}$/)",
        "meta": {
          ".write": "!data.exists() && newData.hasChildren(['ownerUid', 'adminTokenHash', 'createdAt']) && newData.child('ownerUid').isString() && newData.child('adminTokenHash').isString()"
        },
        "presence": {
          "$uidKey": {
            ".write": "$roomHash.matches(/^r_[0-9a-f]{24}$/) && newData.hasChildren(['lastSeen', 'typing'])"
          }
        },
        "messages": {
          ".write": "$roomHash.matches(/^r_[0-9a-f]{24}$/)",
          "$msgId": {
            ".validate": "newData.hasChildren(['sender', 'uid', 'stegoText', 'timestamp']) && newData.child('stegoText').isString() && newData.child('stegoText').val().length < 50000"
          }
        }
      }
    },
    "media_vault": {
      "$mediaId": {
        ".read": true,
        ".write": "!data.exists() && newData.hasChildren(['payload', 'timestamp']) && newData.child('payload').isString() && newData.child('payload').val().length < 4500000"
      }
    }
  }
}
```

---

## 🚀 Deployment Guide (3 Easy Ways)

### Option 1: Deploy on Netlify (Recommended — Like Our Live Demo)
Live Demo Reference: [https://hidden-chaat.netlify.app/](https://hidden-chaat.netlify.app/)

1. **Via GitHub Integration:**
   - Push this repository (`https://github.com/mrabr381/hidden-chat`) to your GitHub account.
   - Log in to [Netlify](https://app.netlify.com/), click **Add new site > Import an existing project**, and select your GitHub repository.
   - Leave the build command blank, set the publish directory to `.` (root), and click **Deploy site**. (`netlify.toml` automatically configures all production security headers!).
2. **Via Netlify Drop (10 Seconds, No CLI):**
   - Drag and drop this repository folder directly onto [Netlify Drop](https://app.netlify.com/drop).

### Option 2: Deploy on Firebase Hosting
1. Install the Firebase CLI:
   ```bash
   npm install -g firebase-tools
   firebase login
   ```
2. Link your Firebase project and deploy:
   ```bash
   firebase use --add
   firebase deploy
   ```

### Option 3: Deploy on GitHub Pages
1. Push these files to your GitHub repository (`https://github.com/mrabr381/hidden-chat`).
2. Go to **Settings > Pages** in your GitHub repo.
3. Under **Build and deployment**, select **Deploy from a branch**, choose `main` (and `/ (root)`), and click **Save**.
4. Your site will be live at `https://mrabr381.github.io/hidden-chat/`.

---

## 🔒 Security Highlights (27-Point Security Checklist Audited)

- **Zero Hardcoded Secrets in Repo:** Clean template configuration with `.gitignore` and `.env.example` so credentials never leak in Git history.
- **Strict File Upload Verification:** Validates binary magic bytes (`PNG`, `JPEG`, `GIF`, `WEBP`) and strict MIME allowlists for voice notes and documents while blocking SVG/HTML/script uploads disguised with fake extensions.
- **XSS & Injection Defense:** All dynamic values are HTML-escaped, input lengths are strictly bounded, and media previews only render verified base64 data URIs.
- **SSRF Protection:** Custom database connections strictly validate HTTPS protocol and allow only official `*.firebaseio.com` and `*.firebasedatabase.app` domains.
- **Production Security Headers:** Pre-configured `Content-Security-Policy`, `Strict-Transport-Security` (HSTS), `X-Frame-Options`, `X-Content-Type-Options`, `Permissions-Policy`, and `Referrer-Policy` in `netlify.toml` and `firebase.json`.

---

## 📜 License & Copyright

Copyright © 2026 [**mrabr381**](https://github.com/mrabr381). All rights reserved.  
Licensed under the **Non-Commercial Personal & Educational Use License** — commercial use, monetization, or sale of this software is strictly prohibited. See [`LICENSE`](./LICENSE) for full details.

---

## ⚖️ Disclaimer

This project is developed for personal privacy, cryptographic research, and educational purposes. Users are solely responsible for complying with local laws and regulations.
