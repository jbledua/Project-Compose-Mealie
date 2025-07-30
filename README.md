# Project Compose: Mealie

This project sets up a private Mealie recipe server accessible via [Tailscale](https://tailscale.com), with optional access from the local network or public internet by customizing the exposed port. Designed for testing and production environments with minimal configuration.

Repo: [https://github.com/jbledua/Project-Compose-Mealie](https://github.com/jbledua/Project-Compose-Mealie)

---

## 📦 Included Services

* **Mealie**: A self-hosted recipe manager
* **Tailscale**: A private VPN service to securely access Mealie without exposing ports publicly

---

## 🚀 Quick Start

### 1. Clone the Repository

```bash
git clone https://github.com/jbledua/Project-Compose-Mealie.git
cd Project-Compose-Mealie
```

### 2. Create a `.env` file

You can use this example:

```env
# .env.example
PUBLIC_PORT=9926
TIMEZONE=Canada/Eastern
TAILSCALE_HOSTNAME=mealie-test
TAILSCALE_AUTHKEY=tskey-xxxxxxxxxxxxxxxxx
BASE_URL=http://localhost:9926
```

> 💡 `TAILSCALE_AUTHKEY` can be generated from [https://login.tailscale.com/admin/authkeys](https://login.tailscale.com/admin/authkeys)

### 3. Run the stack

```bash
docker compose up -d
```

---

## 🌐 Access

* **Tailscale**: From any Tailscale-connected device, visit `http://mealie-app:9000` or use MagicDNS/IP.
* **Local/External Network**: Visit `http://<host-ip>:<PUBLIC_PORT>` (e.g., `http://192.168.1.100:9926`)

> 🔒 If you want Mealie to be accessible outside of the host machine (e.g. other devices on your LAN or the internet), ensure the chosen `PUBLIC_PORT` is open in your firewall and router.

---

## 🔧 Configuration Overview

### Environment Variables (from `.env`)

| Variable             | Description                                               |
| -------------------- | --------------------------------------------------------- |
| `PUBLIC_PORT`        | Port on the host for accessing Mealie (default: 9925)     |
| `TIMEZONE`           | Timezone for Mealie container (default: `Canada/Eastern`) |
| `TAILSCALE_HOSTNAME` | Device name in Tailscale network (default: `mealie-test`) |
| `TAILSCALE_AUTHKEY`  | Auth key to connect Tailscale container to your network   |
| `BASE_URL`           | Public or internal base URL for Mealie                    |

---

## 🗑️ To Stop and Remove

```bash
docker compose down
```

---

## 📁 Volumes

| Volume Name              | Purpose                    |
| ------------------------ | -------------------------- |
| `mealie-data`            | Persistent data for Mealie |
| `mealie-tailscale-state` | Tailscale state storage    |

---

## 📎 Notes

* Mealie is bound to `127.0.0.1` by default, meaning it’s only accessible from the host machine unless ports are explicitly exposed to the local or public network.
* To allow other devices to connect, adjust the firewall or host the container using `0.0.0.0:<PUBLIC_PORT>:9000` instead.
* Tailscale allows secure access from remote devices **without** exposing public ports.
* Update `BASE_URL` if you're accessing from a remote device (e.g., `http://mealie-test.tailnet-xyz.ts.net:9000`)

---

## 🛡️ Security Tips

* Use Tailscale ACLs to restrict access
* Avoid exposing Mealie publicly unless behind a reverse proxy with authentication
* Rotate `TAILSCALE_AUTHKEY` periodically

---

## 🧾 License

This project is licensed under the MIT License.
