# Clouduck 🦆

**A free, open-source Cyberduck-like cloud file manager — runs in your browser.**

No installation. No server. No cost. Just open the HTML file.

---

## ✨ What it does (like Cyberduck)

| Feature | Clouduck |
|---------|----------|
| Browse cloud files | ✅ |
| Upload files (drag & drop) | ✅ |
| Download files | ✅ |
| Create folders | ✅ |
| Delete files | ✅ |
| Rename files | ✅ |
| Multiple accounts/bookmarks | ✅ |
| Transfer queue | ✅ |
| Keyboard shortcuts | ✅ |
| Right-click context menu | ✅ |
| Sort & filter files | ✅ |

---

## ☁ Supported Storage Services

| Service | Cost | Auth Method |
|---------|------|-------------|
| **Google Drive** | Free 15GB | OAuth (Client ID) |
| **OneDrive** | Free 5GB | OAuth (Azure App) |
| **Dropbox** | Free 2GB | Bearer Token |
| **S3 / Backblaze B2** | Pay-per-use / Free tier | Access Key + Secret |

---

## 🚀 Quick Start

### Option 1 — Just open the file
```
Open index.html in Chrome, Firefox, or Edge
```

### Option 2 — Local server (recommended for OAuth)
```bash
python -m http.server 8080
# then open http://localhost:8080
```

### Option 3 — GitHub Pages (free hosting)
1. Push to GitHub
2. Settings → Pages → Deploy from main
3. Done — accessible from anywhere

---

## 🔧 Setup by Service

---

### 🟡 Google Drive

**One-time setup (~5 min):**

1. Go to [console.cloud.google.com](https://console.cloud.google.com) → New Project
2. APIs & Services → Library → Enable **Google Drive API**
3. APIs & Services → Credentials → Create **OAuth 2.0 Client ID**
   - Application type: **Web application**
   - Authorized JavaScript Origins:
     - `http://localhost:8080` (for local use)
     - `https://yourusername.github.io` (for GitHub Pages)
4. OAuth Consent Screen → External → Add your accounts as **Test Users**
5. Copy the Client ID → paste in Clouduck when connecting

**Capabilities:** Browse, upload, download, create folders, delete, rename

---

### 🔵 OneDrive

**One-time setup (~5 min):**

1. Go to [portal.azure.com](https://portal.azure.com) → **App Registrations** → New Registration
2. Name it anything → Accounts in any org + personal → Register
3. Authentication → Add Platform → **Single-page Application**
   - Redirect URI: `http://localhost:8080` (or your GitHub Pages URL)
4. API Permissions → Add → Microsoft Graph → **Files.ReadWrite**, **User.Read**
5. Copy the **Application (client) ID** → paste in Clouduck

**Capabilities:** Browse, upload (small files), download, create folders, delete, rename

---

### 📦 Dropbox

**One-time setup (~3 min):**

1. Go to [dropbox.com/developers/apps](https://www.dropbox.com/developers/apps)
2. Create App → Scoped access → **Full Dropbox**
3. Go to **Settings** tab → OAuth 2 → Generated Access Token → **Generate**
4. Copy the token → paste in Clouduck

> ⚠️ Access tokens expire after a few hours. For long-lived tokens, enable "offline access" in your app's permissions.

**Capabilities:** Browse, upload, download, create folders, delete, rename

---

### 🪣 S3 / Backblaze B2 / MinIO

**Requirements:**
- Endpoint URL (e.g. `https://s3.amazonaws.com` or `https://s3.us-west-004.backblazeb2.com`)
- Bucket name
- Access Key ID + Secret Access Key

**Important — CORS setup:**
S3 buckets need CORS enabled to allow browser access. Add this to your bucket's CORS config:

```xml
<CORSConfiguration>
  <CORSRule>
    <AllowedOrigin>*</AllowedOrigin>
    <AllowedMethod>GET</AllowedMethod>
    <AllowedMethod>PUT</AllowedMethod>
    <AllowedMethod>DELETE</AllowedMethod>
    <AllowedHeader>*</AllowedHeader>
  </CORSRule>
</CORSConfiguration>
```

**Backblaze B2 free tier:** 10GB storage + 1GB/day download — completely free.

---

## ⌨️ Keyboard Shortcuts

| Shortcut | Action |
|---------|--------|
| `Double-click` | Open folder / Download file |
| `Ctrl+A` | Select all |
| `Delete` | Delete selected |
| `Backspace` | Go back |
| `/` | Focus search |
| `Escape` | Clear search |
| `Ctrl+R` or `F5` | Reload |
| `Right-click` | Context menu |

---

## 📁 Project Structure

```
clouduck/
├── index.html    ← The entire app (one self-contained file)
└── README.md     ← This file
```

---

## 🔒 Privacy & Security

- **Zero backend** — everything runs in your browser
- **No data collection** — your files never touch any server we control
- **OAuth tokens** — stored in memory, cleared on tab close
- **Bookmarks** — saved to your browser's `localStorage` only
- **Credentials** — never transmitted anywhere except the cloud provider directly

---

## 💡 Why browser-based instead of native?

| | Clouduck (Browser) | Cyberduck (Native) |
|--|--|--|
| Cost | Free | Free (donation) |
| FTP/SFTP | ❌ (browser limitation) | ✅ |
| Google Drive | ✅ | ✅ |
| OneDrive | ✅ | ✅ |
| Dropbox | ✅ | ✅ |
| S3 | ✅ | ✅ |
| Cross-platform | ✅ | ✅ |
| No install | ✅ | ❌ |
| GitHub hosting | ✅ | ❌ |

> **FTP/SFTP note:** Browsers cannot make raw TCP connections, so FTP and SFTP are not supported. For FTP/SFTP, use Cyberduck (free), FileZilla (free), or WinSCP (free, Windows).

---

## ❓ Troubleshooting

**Google auth popup not opening:**
Use a local server (`python -m http.server 8080`) instead of opening the file directly.

**"redirect_uri_mismatch" error:**
The URL you're accessing must exactly match what you put in Authorized Origins in Google Cloud Console.

**Dropbox token not working:**
Make sure you selected "Full Dropbox" access when creating the app, and generated a fresh token.

**S3 CORS error:**
Enable CORS on your bucket. See the CORS config above.

**OneDrive login popup blocked:**
Allow popups for localhost in your browser settings.

---

## 📝 License

MIT — free to use, modify, and host.
