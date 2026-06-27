# Team Setup Guide — Savera Handicrafts Project

Complete step-by-step guide for new team members to set up GitHub access and get the project running.

**Requirements:** Windows PC · GitHub account · ~10 minutes

---

## Step 1: Install GitHub CLI

Open **PowerShell** and run:

```powershell
winget install GitHub.cli --source winget
```

Close and reopen PowerShell after the install completes.

---

## Step 2: Generate a GitHub Personal Access Token (PAT)

1. Log in to [github.com](https://github.com)
2. Go to: **Settings → Developer settings → Personal access tokens → Tokens (classic)**
3. Click **"Generate new token (classic)"**
4. Fill in:
   - **Note:** give it a name like `my-laptop`
   - **Expiration:** 90 days (recommended)
   - **Scopes:** check **`repo`** — that's all you need
5. Click **"Generate token"**
6. **Copy the token immediately** — GitHub will never show it again

Your token will look like: `ghp_xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx`

---

## Step 3: Store Your Token in a .env File

Create a folder for your credentials (e.g. `D:\my-credentials\`) and inside it create a file named `.env` with this content:

```
GITHUB_TOKEN=ghp_your_token_here
```

Replace `ghp_your_token_here` with the actual token you copied.

> Keep this file private. Never share it or commit it to any repository.

---

## Step 4: Authenticate GitHub CLI

Open **PowerShell** and run these commands:

```powershell
$env:Path = [System.Environment]::GetEnvironmentVariable("Path","Machine") + ";" + [System.Environment]::GetEnvironmentVariable("Path","User")

$token = ((Get-Content "D:\my-credentials\.env") | Where-Object { $_ -match "^GITHUB_TOKEN=" }) -replace "^GITHUB_TOKEN=","" -replace "\r","" -replace "\n",""

$env:GH_TOKEN = $token

gh auth status
```

You should see:
```
github.com
  ✓ Logged in to github.com account <your-username> (GH_TOKEN)
```

---

## Step 5: Clone the Repository

```powershell
gh repo clone cocodigitalwave-wq/savera-handicrafts
```

Or using git directly:

```powershell
git clone https://github.com/cocodigitalwave-wq/savera-handicrafts.git
```

---

## Step 6: Run the App

1. Open the cloned `savera-handicrafts` folder
2. Double-click **`index.html`**
3. It opens in your browser — fully offline, no install needed

---

## Troubleshooting

| Problem | Fix |
|---------|-----|
| `gh: command not found` | Close and reopen PowerShell after installing gh CLI |
| `401 Bad credentials` | Token was copied wrong or expired — generate a new one (Step 2) |
| `Repository not found` | Confirm you're cloning `cocodigitalwave-wq/savera-handicrafts` exactly |
| App doesn't load | Make sure you're opening `index.html` directly in a browser |

---

## Repository
`https://github.com/cocodigitalwave-wq/savera-handicrafts`
