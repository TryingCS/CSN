---
{"dg-publish":true,"permalink":"/curl/","created":"2026-10-31T14:16:03.079+01:00","updated":"2026-10-31T14:37:04.013+01:00","dg-note-properties":{}}
---

#misc 
***
# Can you `curl` any URL?

You can *attempt*  but whether you get something useful back depends  on **what protocol the server speaks** and **what kind of data it returns**.

Here's the nuance:

## ✅ What `curl` can handle well

`curl` supports a long list of URL schemes out of the box:

| Scheme | Example | What you get |
| :--- | :--- | :--- |
| `http://` / `https://` | `curl https://example.com` | HTML source, JSON, images, etc. |
| `ftp://` / `sftp://` | `curl ftp://ftp.gnu.org/` | Directory listing or file |
| `file://` | `curl file:///etc/hosts` | Local file contents |
| `dict://` | `curl dict://dict.org/d:curl` | Dictionary lookup |
| `telnet://` | `curl telnet://mapscii.me` | Raw TCP stream (non-interactive) |
| `ldap://`, `smtp://`, `imap://`, `pop3://` | — | Protocol-specific responses |

So for any URL whose scheme `curl` understands, **yes — it will connect and speak that protocol**.

## ⚠️ What "works" actually means

The catch is that `curl` is a **non-interactive pipe**. It sends a request and dumps whatever comes back to your terminal. That produces very different results depending on the target:



## 🔑 The real distinction

The question isn't "can `curl` hit any URL?" — it's **"does the server speak a protocol `curl` can drive, and does the response make sense in a terminal?"**

| Target type | `curl` result |
| :--- | :--- |
| REST API / static file / plain HTML | ✅ Perfect |
| SPA / JS-rendered page | ⚠️ Empty shell |
| Image / PDF / binary | ⚠️ Garbage (redirect to file) |
| Interactive TCP service (MapSCII, BBS, MUD) | ❌ Not designed for this |
| Streaming animation (ascii.live) | ✅ Works (one-way stream) |
| SSH, WebSocket interactive apps | ❌ Wrong tool |

## 💡 Rule of thumb

- **`curl` is for:** "give me the bytes this URL returns, in a predictable format, and I'll handle them."
- **It is not for:** interactive sessions, rendered pages, or running JavaScript.

So you *can* point `curl` at nearly anything — but the useful question is always: **what does that server expect to receive, and what will it send back?** If both sides agree on HTTP (or FTP, etc.), you're fine. If the server expects a live human typing keystrokes over a raw socket, `curl` will connect but won't give you the experience you're hoping for.
***

| Command | Origin | Meaning |
| :--- | :--- | :--- |
| `apropos` | French/English word | "relevant to" |
| `grep` | acronym | "global / regular expression / print" |
| `awk` | initials | Aho, Weinberger, Kernighan (authors) |
| `sed` | acronym | "stream editor" |
| `cat` | English word | "concatenate" |

