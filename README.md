# 🤖 RAG Bot Checker — Bookmarklet

A one-click browser bookmarklet that audits any website's `robots.txt` to show which **AI and RAG (Retrieval-Augmented Generation) crawlers** are allowed or blocked.

Built for SEO professionals, content creators, and developers who want to know whether their site is **discoverable by AI assistants** like ChatGPT, Claude, Perplexity, Gemini, and Copilot.

![Status](https://img.shields.io/badge/status-stable-brightgreen) ![License](https://img.shields.io/badge/license-MIT-blue) ![Dependencies](https://img.shields.io/badge/dependencies-none-success)

---

## ✨ Features

- ✅ Checks **9 major AI/RAG crawlers** in one click
- 🎨 Clean modal overlay with allowed/blocked breakdown
- ℹ️ Hover tooltips explaining what each bot does
- 📄 Raw `robots.txt` viewer included
- ⚡ Runs instantly — no install, no servers, no accounts
- 🔒 100% client-side — your data never leaves your browser

## 🤖 Bots Checked

| Bot | Purpose |
|---|---|
| `OAI-SearchBot` | OpenAI SearchGPT indexing |
| `ChatGPT-User` | ChatGPT on-demand link fetch |
| `PerplexityBot` | Perplexity AI live search |
| `ClaudeBot` | Anthropic Claude web access |
| `Google-Extended` | Gemini & Vertex AI opt-out token |
| `Applebot-Extended` | Apple Intelligence opt-out token |
| `YouBot` | You.com AI search |
| `Bingbot` | Bing + Microsoft Copilot RAG |
| `Googlebot` | Google Search + AI Overviews |

---

## 🚀 Installation (30 seconds)

1. **Open** [`bookmarklet.js`](./bookmarklet.js) in this repo and **copy the entire contents** (it's a single line starting with `javascript:`)
2. **Show your bookmarks bar** in your browser: `Ctrl/Cmd + Shift + B`
3. **Right-click the bookmarks bar** → **Add page** (or **New bookmark**)
4. Fill in the fields:
   - **Name:** `🤖 RAG Bot Checker`
   - **URL:** paste the code you copied
5. **Save** ✅

> ⚠️ Make sure the pasted URL still starts with `javascript:` — some browsers strip this prefix for security. If yours does, just type `javascript:` back in front of the code before saving.

---

## 🧭 Usage

1. Visit any website (e.g., `https://example.com`)
2. Click the **🤖 RAG Bot Checker** bookmark
3. A modal appears showing which AI bots are allowed/blocked
4. Hover the ℹ️ icons for details about each bot
5. Click ✕ or outside the modal to close

> The tool always checks `<current-domain>/robots.txt` — so navigate to the site you want to audit first.

---

## 🔒 Is It Safe? (Security Overview)

**Yes — this bookmarklet is safe to use.** Here's exactly why, in plain terms:

### ✅ What it does
- Fetches **only** `/robots.txt` from the current site you're visiting (a public file anyway)
- Parses it locally in your browser using standard JavaScript
- Displays the results in an overlay on the current page
- Removes itself when you close the modal

### 🚫 What it does NOT do
| ❌ Does NOT | Why it's safe |
|---|---|
| Send any data to external servers | Zero `fetch()` calls outside the current domain |
| Use cookies or localStorage | No persistence — nothing is saved |
| Track you or use analytics | No third-party scripts, no telemetry |
| Read passwords, forms, or page content | Only touches `/robots.txt` |
| Modify the page permanently | The overlay is removed on close |
| Require any permissions | Just runs as a normal `<script>` in the page context |
| Load external code | All logic is self-contained in the bookmarklet |

### 🛡️ Built-in Safeguards
The code includes several **defensive checks**:

- **HTML escaping** of all output (`esc()` function) → prevents XSS from malicious robots.txt content
- **Size limit** → rejects `robots.txt` files larger than 500 KB
- **Content-type validation** → rejects responses that look like HTML (catches misconfigured servers returning 404 pages as 200)
- **Path-length cap** → ignores rule paths over 2000 chars (prevents ReDoS)
- **Regex sanitization** → special characters in patterns are escaped before regex compilation
- **`cache: 'no-store'`** → always fetches fresh content, no stale results
- **Sandboxed scope** → wrapped in an IIFE so it doesn't pollute the page's global namespace

### 🔍 Verify It Yourself
The entire bookmarklet is **~5 KB of readable JavaScript** in `bookmarklet.js`. You can:
1. Open it in any text editor
2. Search for `fetch(` — you'll find exactly **one call**, to `/robots.txt` on the current origin
3. Search for `XMLHttpRequest`, `WebSocket`, `sendBeacon`, `eval`, `Function(` — **none exist**

> Unlike browser extensions, bookmarklets cannot run in the background, cannot access other tabs, and cannot persist between sessions. They only execute when you explicitly click them.

---

## 🧰 Browser Compatibility

| Browser | Support |
|---|---|
| Chrome / Edge / Brave | ✅ Full |
| Firefox | ✅ Full |
| Safari | ✅ Full |
| Mobile browsers | ⚠️ Limited (bookmarklets are harder to trigger on mobile) |

> Some sites with strict **Content Security Policy (CSP)** headers may block the bookmarklet from running. This is a browser security feature, not a bug.

---

## 📂 Repository Structure

```
.
├── bookmarklet.js      # The bookmarklet source code (copy this into a bookmark)
├── README.md           # This file
└── LICENSE             # MIT
```

---

## 🛠️ Development

The bookmarklet is a single self-contained IIFE. To modify:

1. Edit `bookmarklet.js`
2. Test by pasting into your browser's DevTools console (without the `javascript:` prefix)
3. Once happy, ensure it starts with `javascript:` and save as a bookmark URL
4. Optionally minify with [bookmarkleter](https://chriszarate.github.io/bookmarkleter/)

---

## 📜 License

MIT — see [`LICENSE`](LICENSE). Free to use, modify, and share.

---

## 🙋 FAQ

**Q: Why check AI bots specifically?**
A: With the rise of AI-generated answers (ChatGPT, Gemini AI Overviews, Perplexity), your site's visibility in AI tools now depends on whether you allow these specific crawlers — separate from regular SEO.

**Q: Does blocking `Google-Extended` hurt my Google ranking?**
A: No. `Google-Extended` only controls Gemini/Vertex AI training. Regular Google Search uses `Googlebot`.

**Q: Why didn't it find a robots.txt?**
A: The site may not have one (which means everything is allowed by default), or the server returned an HTML error page instead of a 404. The tool warns you in both cases.

**Q: My browser stripped the `javascript:` prefix when I pasted!**
A: This is a common security feature in Chrome and Firefox. Just type `javascript:` back in front of the pasted code before saving the bookmark.

**Q: Can I add more bots?**
A: Yes — edit the `UAS` array in `bookmarklet.js` and add `{ua, label, info}` objects.

---

⭐ If this helped you, consider starring the repo!
