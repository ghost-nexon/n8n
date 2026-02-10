# n8n on Render Deployment Guide 🚀

Deploy your own self-hosted n8n instance on Render’s free tier and keep it running 24/7.

## 📋 Prerequisites

1. **Render Account**: Sign up at [render.com](https://render.com/).
    * *Recommendation: Use GitHub to log in for easier repository integration.*
2. **n8n Repository**: Have a repository containing the n8n source or a compatible Dockerfile/Node.js setup on your GitHub.

---

## 🛠️ Deployment Steps

### 1. Create a New Web Service
1. Log in to the Render Dashboard.
2. Click **New +** and select **Web Service**.
3. Connect and select your n8n GitHub repository.

### 2. Configure Service Settings
Fill in the following details in the configuration section:

| Field | Value |
| :--- | :--- |
| **Language** | `Node` |
| **Branch** | `main` (or `master`) |
| **Region** | Select your preferred region (e.g., US or Singapore) |
| **Root Directory** | *Leave Empty* |
| **Build Command** | `npm install` |
| **Start Command** | `npm start` |
| **Plan** | `Free` |

### 3. Environment Variables
Navigate to the **Environment** tab and add the following variables:

| Key | Value |
| :--- | :--- |
| `N8N_BASIC_AUTH_ACTIVE` | `true` |
| `N8N_BASIC_AUTH_USER` | *Your chosen username* |
| `N8N_BASIC_AUTH_PASSWORD` | *Your chosen strong password* |
| `N8N_ENCRYPTION_KEY` | *A random 32-character string* (Save this safely!) |
| `TZ` | `Asia/Kolkata` (or your local timezone) |
| `N8N_PROTOCOL` | `https` |
| `N8N_PORT` | `${PORT}` |
| `N8N_HOST` | *Update after deployment (see below)* |
| `WEBHOOK_URL` | *Update after deployment (see below)* |

---

## 🔗 Finalizing Configuration

Once Render completes the deployment, it will provide you with a public URL (e.g., `https://your-n8n-app.onrender.com`).

1. Go back to **Settings** → **Environment**.
2. Update the following two variables:
   - **N8N_HOST**: `your-n8n-app.onrender.com` (Only the host, no `https://`)
   - **WEBHOOK_URL**: `https://your-n8n-app.onrender.com`
3. Save changes. Render will redeploy automatically.

---

## 💤 Keeping it 24/7 (Preventing Sleep)
Render's free tier puts web services to sleep after inactivity. To keep your n8n workflows running 24/7, use a ping service:

1. Go to [Uptime Robot](https://uptimerobot.com/).
2. Create a new account and project.
3. **Add New Monitor**:
   - **Monitor Type**: HTTP(s)
   - **Friendly Name**: n8n-Render
   - **URL**: Your n8n public link.
   - **Monitoring Interval**: Every 5 minutes.
4. Save the monitor.

**Result**: Uptime Robot will ping your n8n instance every 5 minutes, ensuring it never goes into sleep mode. 💸💸

---

## 🔐 Security Note
Keep your `N8N_ENCRYPTION_KEY` in a safe place. If you lose this key and delete your service, you will not be able to decrypt your credentials in future migrations.

---
*Generated for n8n automation enthusiasts.*
