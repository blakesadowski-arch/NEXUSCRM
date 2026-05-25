# NexusCRM — Live Deploy

AI-native CRM demo. `index.html` is the marketing site; `app.html` is the full app.
Both call `/api/chat` (a serverless function) which proxies to the Anthropic API.
If the API is unreachable, the pages fall back to built-in simulated AI — no errors.

## File structure (IMPORTANT)

These files must be at the ROOT of your GitHub repo — NOT inside a wrapper folder:

```
index.html      ← homepage (must be at root)
app.html        ← the CRM app
api/chat.js     ← AI backend (serverless function)
vercel.json
package.json
.gitignore
```

If your repo looks like `nexcrm-deploy/index.html`, that extra folder is what
causes a 404. Move the files up so index.html sits at the top level.

## Deploy steps

### 1. GitHub
- Create a repo at github.com/new (name it `nexcrm`, no README)
- Click "uploading an existing file"
- Drag in the CONTENTS of this folder (index.html, app.html, the api folder, etc.)
  — NOT the folder itself
- Commit

### 2. Vercel
- vercel.com → sign in with GitHub
- Add New → Project → import `nexcrm` → keep defaults

### 3. API key
- Settings → Environment Variables
- Name: `ANTHROPIC_API_KEY`   Value: your sk-ant-... key (from console.anthropic.com)

### 4. Deploy
- Click Deploy → live in ~30s at https://nexcrm.vercel.app

## Fixing a 404

A 404 on the homepage means index.html is not at the repo root. Check your repo
on GitHub — you should see index.html in the file list immediately, not inside
another folder. If it's nested, delete the repo files and re-upload the CONTENTS
(not the wrapping folder).

## Updating
Push to GitHub → auto-redeploys on Vercel.
