# Set Up Your Own Longevity OS (10 minutes, no coding)

You'll use **Claude** (the AI) as the engine. You upload your health files, Claude reads them and builds **your** dashboard with your real numbers. Your data stays in **your own Claude account** — nobody else ever sees it.

**Just want to look first?** The live demo (sample data, not a real person) is here: **https://colby-source.github.io/longevity-os/** — click around, then come back and build your own.

---

## What you need
- A free account at **claude.ai** (Claude Pro is better but not required).
- Any health data you have. **You don't need all of it** — even one lab PDF works. More data = better dashboard.

---

## Step 1 — Get your health files (do only the ones you have)

Save each of these to your computer or phone. A **photo** of any document works if you can't find a download.

| Data | Where to get it |
|---|---|
| **WHOOP** | WHOOP app → **More** → **App Settings** → **Data Export** → **Request Export**. They email you a ZIP of CSV files — download it. |
| **DNA / genetics** | **23andMe:** 23andme.com → **Settings** → **23andMe Data** → **Download** → **Raw data** (a `.txt` file). **Ancestry:** Settings → **Download DNA Data**. **Sequencing.com:** log in → **Files** → download your report exports. |
| **Gut (Viome)** | Viome app → **Results** → **Share / Download** → **Save as PDF**. |
| **Bloodwork / labs** | **LabCorp:** patient.labcorp.com → Results → **Download PDF**. **Quest:** MyQuest → Results → **Download**. **Any other lab:** open the result → **Print → Save as PDF**, or just take a clear **photo of each page**. |
| **Supplements / peptides** | Just **snap a photo** of each label (front + supplement-facts side). |

> **Too-big-file tip:** For DNA, upload the **23andMe/Ancestry `.txt`** or your **report exports** — NOT a full raw genome file (those are gigabytes and won't upload). Lab PDFs and WHOOP CSVs are small and fine.

---

## Step 2 — Set up Claude (pick ONE path)

### Path A — You have Claude Pro (recommended: it remembers you)
1. Go to **claude.ai** → left sidebar → **Projects** → **＋ New Project**.
2. Name it **`Longevity OS`** → **Create**.
3. Click **Set custom instructions** (or the ⚙/edit icon on the project). Open the file **`PROJECT_INSTRUCTIONS.md`** from this repo, **copy everything in it**, and **paste it** into the instructions box → **Save**.
4. In the project, click **Add content / files** and upload the file **`dashboard-template.html`** from this repo. *(Optional: also add `knowledge-starter.md`.)*
5. Done. Go to Step 3.

### Path B — Free Claude (no Project)
1. Go to **claude.ai** → **＋ New chat**.
2. Open the file **`MASTER_PROMPT.md`** from this repo → **copy the whole prompt** in it → **paste it** into the chat box. *(Don't press send yet.)*
3. Go to Step 3.

> **Where do I get `PROJECT_INSTRUCTIONS.md` / `MASTER_PROMPT.md` / `dashboard-template.html`?** They're in the **`setup/`** folder of this repo (github.com/colby-source/longevity-os). Click the file → **Raw** → select-all → copy. Or download the repo as a ZIP: green **Code** button → **Download ZIP**.

---

## Step 3 — Upload your files and build it
1. In the Claude chat, click the **📎 attach** (paperclip) button and **attach the files from Step 1**. You can add them in batches.
2. Type exactly:
   > **Build my dashboard.**
3. Press send.

Claude will tell you what it received, then build your **dashboard as an Artifact** (it opens in a panel on the right — you can view, download, or share it) and write your analysis: your **biological age**, top flags, genetics→what-to-monitor, supplement/peptide overlaps, and your top 3–5 moves.

---

## Step 4 — Use it as your coach (ongoing)
- **Ask it anything:** "Why is my HRV low?" · "What should I fix first?" · "Any overlaps in my stack?" · "Is my bio-age real?"
- **Keep it current:** upload a new lab panel anytime and say:
  > **Update my dashboard and tell me what changed.**
- **Save your dashboard:** on the Artifact, click **⋯ → Download** to keep the HTML file, or **Share** to get a link.

---

## Troubleshooting
- **"It didn't read my file."** Make sure it fully uploaded (you see the file chip in the chat) before sending. Re-attach and try again.
- **A file won't upload (too big).** It's probably a raw genome — use the 23andMe/Ancestry `.txt` or your report exports instead.
- **The dashboard looks empty in places.** That's normal — Claude labels anything you didn't upload as "no data yet." Add that source later.
- **I only have one thing.** Fine. Upload it and build — the dashboard grows as you add more.

---

*Educational only — not medical advice. Longevity OS does not diagnose, treat, or prescribe, and creates no doctor–patient relationship. Peptide references are research-use-only and not FDA-approved. Supplement statements are not evaluated by the FDA. Consult a licensed clinician for medical decisions; call your doctor or emergency services for anything urgent.*
