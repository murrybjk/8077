# ⚡ Flask IPTV Redirector

A lightweight Flask-based service that dynamically generates and redirects to IPTV stream links using `server`, `channel`, and `MAC address` parameters.

---

## 🔗 Example Usage

```url
http://localhost:8077/<server>/<channel>/<mac>
```

📺 Example:

```url
http://localhost:8077/hd-max.org:8080/201/00:1A:79:12:14:01
```

This sends a request to the IPTV portal to generate a tokenized stream and redirects the user directly to the stream.

---

## 🚀 Quick Start

### 1. Install dependencies

```bash
pip install flask requests
```

### 2. Run the app

```bash
python app.py
```

By default, it runs on:

```url
http://0.0.0.0:8077
```

---

## 📦 API Details

### GET `/\<server>/\<channel>/\<mac>`

- **server** – e.g. `hd-max.org:8080`
- **channel** – channel ID from the IPTV provider
- **mac** – MAC address in STB format (e.g. `00:1A:79:12:14:01`)

🔁 The route:
- Builds a URL to generate a streaming link using IPTV middleware
- Parses JSON to extract the final stream URL
- Redirects the user to the playable stream (`.ts` or `.m3u8`)

---

## ✅ JSON Response Format Expected

```json
{
  "js": {
    "cmd": "ffmpeg http://example.com/stream/abc123.ts"
  }
}
```

---

## 🛡️ Notes

- No caching — each request fetches a new token
- Uses `ffmpeg` syntax internally to extract the stream link
- Make sure the IPTV server allows `User-Agent` spoofing (Googlebot)

---

## 🔧 Deployment Tips

- Use **Nginx** or **Apache** as a reverse proxy
- Set up a **systemd** service for auto-start on boot
- Optional: add rate limiting or password protection if exposed publicly

---

## 👨‍💻 Author

**murrybjk**  
[GitHub Profile](https://github.com/murrybjk)

---

## 📄 License

[MIT](https://choosealicense.com/licenses/mit/)
