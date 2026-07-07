# Integrations — Connecting Your Data

Longevity OS has **two ways** to get your data in. Start with #1 (works today, zero setup). #2 is for the live self-hosted app.

| # | Method | Works today? | Setup effort |
|---|---|---|---|
| 1 | **File export → Claude** (WHOOP CSV, lab PDF, DNA txt, Viome PDF, supplement photo) | ✅ Yes — this is the [SETUP_GUIDE](SETUP_GUIDE.md) path | 10 min, no coding |
| 2 | **Live API sync** (WHOOP auto-syncs daily; AI Doctor streams from Claude) | ⏳ Requires the full self-host app (see roadmap) | Developer keys + hosting |

> **Honest status:** the public demo and the Claude kit use **method #1 (exports)**. The "WHOOP synced 2m ago" and live AI Doctor you see in the demo are what the **full app** does — that app is on the roadmap, not in this repo yet. Everything below is the setup for when you run that app (or build it with Claude). If you just want your dashboard now, you don't need any of this — use [SETUP_GUIDE](SETUP_GUIDE.md).

---

## 1. WHOOP — create your developer app (for live daily sync)

WHOOP doesn't hand out a personal API key. You create a **free WHOOP developer app**, which gives you a Client ID + Secret your dashboard uses to sync your data automatically.

### Step 1 — Make the app
1. Go to **developer.whoop.com** → sign in with your normal WHOOP login.
2. Open the **Developer Dashboard** → **Create App** (or "New Application").
3. Fill in:
   - **App name:** `Longevity OS`
   - **Redirect URI (Redirect URLs):** the address your dashboard runs at, plus `/api/whoop/callback`.
     - Running locally: `http://localhost:3000/api/whoop/callback`
     - Deployed (Vercel): `https://YOUR-APP.vercel.app/api/whoop/callback`
     - *(You can add both. The redirect URI must match EXACTLY — trailing slash and all.)*
   - **Scopes (check these):** `read:recovery`, `read:sleep`, `read:cycles`, `read:workout`, `read:profile`, `read:body_measurement`, and **`offline`** ← the `offline` scope is required so the app can refresh without you re-logging-in daily.
   - **Contacts / Privacy URL:** your email / any URL (required fields).
4. **Create.** Copy the **Client ID** and **Client Secret** it shows you. Treat the secret like a password.

### Step 2 — Put the keys in your app
Create a file named **`.env.local`** in your app folder (never commit this file — it's gitignored):
```
WHOOP_CLIENT_ID=your_client_id_here
WHOOP_CLIENT_SECRET=your_client_secret_here
WHOOP_REDIRECT_URI=http://localhost:3000/api/whoop/callback
```
On Vercel: **Project → Settings → Environment Variables** → add the same three keys.

### Step 3 — Connect
Open your dashboard → **Settings → Connect WHOOP** → it sends you to WHOOP → **Allow**. You land back on your dashboard, now synced.

### How the sync works (so you're not surprised)
- HRV, resting HR, recovery %, SpO2, and skin temp all live **inside the daily Recovery record** — there's no separate "HRV endpoint."
- WHOOP **refresh tokens rotate and are single-use**, so the app refreshes on a **schedule (a daily cron)**, not lazily. If you self-host, that cron is what keeps it connected.
- Rate limit is **per-app** (100 req/min, 10k/day). Because you self-host with **your own** app keys, you get your own full budget — a real advantage over shared hosted apps.

---

## 2. The AI Doctor — add your Claude API key

The chat coach in the full app streams from Claude. To power it on your own instance:
1. Go to **console.anthropic.com** → **API Keys** → **Create Key** → copy it (starts with `sk-ant-`).
2. Add to `.env.local`:
   ```
   ANTHROPIC_API_KEY=sk-ant-your_key_here
   ```
   (or Vercel → Environment Variables). You pay Anthropic directly for your own usage; nobody else can see or use your key.

> **You can skip this** and use the free Claude-kit path instead ([SETUP_GUIDE](SETUP_GUIDE.md) Path A/B) — that runs the "AI doctor" inside your normal claude.ai chat with no API key at all.

---

## 3. Labs, DNA, Gut — why these stay export-based (on purpose)

These have **no consumer API**, and pulling them unofficially risks getting your account locked. So they're upload-based by design — which is also better for privacy (nothing phones home):

| Source | How it connects | Why not live |
|---|---|---|
| **Labs** (LabCorp/Quest/Rythm) | Upload the PDF or a photo → parsed | No open patient API; portals are login-only |
| **DNA** (23andMe/Ancestry/Sequencing) | Upload the `.txt` / report export once | APIs can't export your genome or reports; one-time import is also more private |
| **Gut** (Viome) | Upload the results PDF | No official API; unofficial endpoints are a terms-of-service / lockout risk |
| **Supplements/peptides** | Snap a label photo → parsed | Photo is faster than any lookup |

Re-upload a new lab or Viome anytime and say **"update my dashboard and tell me what changed."**

---

## 4. Adding another wearable later (Oura, CGM, Apple Health)

The data model is source-agnostic, so the full app leaves a clean adapter seam:
- **Oura:** create an app at cloud.ouraring.com (Personal Access Token is the quickest), same `.env.local` pattern.
- **CGM (Levels/Dexcom/Libre):** OAuth per vendor, or export → upload.
- **Apple Health:** export the Health `.zip` → upload (no live API off-device).

Each maps into the same unified schema, so the dashboard and coach read them the same way as WHOOP.

---

## Security rules (all methods)
- **Never commit `.env.local`** or any key — it's gitignored; use `.env.example` for placeholders only.
- Keys are **per-deploy environment variables**. On a self-host, your keys sit in *your* environment, not in the code and not on anyone's server.
- Rotate a key immediately if it's ever exposed (regenerate in the WHOOP/Anthropic dashboard).

---

*Educational only — not medical advice. See [SETUP_GUIDE](SETUP_GUIDE.md) for the no-code path.*
