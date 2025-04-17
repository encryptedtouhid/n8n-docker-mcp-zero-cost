# 🌀 Zero-Cost n8n Setup with Docker & Community Proxy (MCP)

This guide walks through setting up a free, self-hosted instance of [n8n](https://n8n.io) with the **n8n Community Proxy (MCP)**, entirely using Docker.

---

## ✅ Prerequisites

- 🐳 Docker & Docker Compose installed
- ✅ Free domain (optional, for HTTPS)
- ✅ Git + text editor (VSCode, etc.)
- ⛅ Optional: Cloudflare Tunnel for remote access

---

## 📁 Step 1: Create a Project Folder

```bash
mkdir n8n-zerocost && cd n8n-zerocost
```

---

## 🧾 Step 2: Create `.env` File

```ini
# .env

N8N_BASIC_AUTH_USER=admin
N8N_BASIC_AUTH_PASSWORD=strongpassword

N8N_HOST=localhost
N8N_PORT=5678

N8N_EDITOR_BASE_URL=https://n8n.community
N8N_PROTOCOL=http
WEBHOOK_TUNNEL_URL=https://n8n.community

N8N_PERSONALIZATION_ENABLED=false
N8N_DIAGNOSTICS_ENABLED=false
```

---

## ⚙️ Step 3: Create `docker-compose.yml`

```yaml
# docker-compose.yml

version: "3.7"
services:
  n8n:
    image: n8nio/n8n:latest
    restart: always
    ports:
      - "5678:5678"
    env_file:
      - .env
    volumes:
      - ./n8n_data:/home/node/.n8n
    environment:
      - N8N_COMMUNITY_PACKAGES_ALLOWED=true
      - N8N_TUNNEL_SUBDOMAIN=your-subdomain  # Optional
```

---

## 🌍 Step 4: Launch n8n

```bash
docker compose up -d
```

Check logs:

```bash
docker logs -f n8n
```

---

## 🔐 Step 5: Access Your n8n Editor

- Locally: `http://localhost:5678`
- Remotely (if using a tunnel): via `n8n.community` (MCP handles public tunnel)

---

## ☁️ Optional: Use Cloudflare Tunnel (Zero Trust)

```bash
cloudflared tunnel --url http://localhost:5678
```

---

## 🧪 Step 6: First Workflow

1. Go to your n8n instance.
2. Create a simple trigger like HTTP Request ➝ Respond with Message.
3. Test it with the tunnel or MCP URL.

---

## 📦 Step 7: (Optional) Install Community Nodes

You can now install any free community package under `Settings ➝ Community Nodes`.

---

## 📁 Volumes

Your workflows and data will be stored in:

```bash
./n8n_data/
```

---

## ✅ Tips for Zero Cost Hosting

| Platform     | Use                         |
|--------------|------------------------------|
| Railway      | Free Docker hosting          |
| Render       | Free web services            |
| Replit       | For testing                  |
| Cloudflare   | Tunneling + free domain      |
| n8n MCP      | Free tunnel proxy to public  |

---

## 🚨 Security

- Always use strong username/password in `.env`
- For production, use HTTPS (Cloudflare tunnel or NGINX)

---

## ✅ Done!

Your zero-cost n8n is now live and running with Docker and MCP!
