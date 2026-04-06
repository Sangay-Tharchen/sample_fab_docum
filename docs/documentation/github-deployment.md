# How to Deploy Your Site on GitHub Pages

This guide walks you through publishing your MkDocs documentation site on the internet using **GitHub** — for free. Follow every step in order.

---

## What You Will Need

| Requirement | Where to get it |
|---|---|
| A GitHub account | [github.com/signup](https://github.com/signup) |
| This repository | You can open this [link](https://github.com/Aesthetics-Centre/sample_fab_docum) |

No Python or software installation is needed if you use **Codespaces**. It is a online IDE to update your code on the browser.

---

## Step 1 — Fork or Copy the Repository

    1. Open the GitHub repo link your teacher shared
    2. Click the **Fork** button (top-right corner)
    3. Keep the default settings or just change the project name and click **Create fork**
    4. You now have your own copy — continue to Step 2

![Description](https://drive.google.com/thumbnail?id=1LyiTpt2ETQX3GGyh4j-RcR0ArvEyOIuR&sz=w800)

Keep the default settings or just change the project name and click **Create fork**

![Description](https://drive.google.com/thumbnail?id=1o6Y9FG9IQ-Htm3m-aEOTIs4-jfKJRhUL&sz=w800)

---

## Step 2 — Enable GitHub Pages and Workflow.

!!! warning "Do this ONCE before your first deployment"

### Workflow:

1. On the top of the repo click on **Actions**

![Description](https://drive.google.com/thumbnail?id=153JcEieMOgWBJHlMUOnvzs-s4Bj1w50l&sz=w800)

2. Make sure you click on the green button so that github can build your MkDocs website.

### Deploy Pages 

1. Open your repository on GitHub

![Description](https://drive.google.com/thumbnail?id=1ekwpKD70lWEFpXVccTBHOd85wknKQCY1&sz=w800)

2. Click **Settings** (the cog icon in the top menu)
3. In the left sidebar, click **Pages**
4. Under **Source**, choose:
   - **Deploy from a branch**
   - Branch: `gh-pages`
   - Folder: `/ (root)`
5. Click **Save**

refresh the page in few minutes to see the published link.

!!! note
    The `gh-pages` branch is created automatically when the first deployment runs.  
    If you don't see it yet, complete Step 4 first, then come back and set this.

---

## Step 3 — Edit Your Site

You have two ways to edit your site. **Codespaces is strongly recommended.**

=== "🌐 Codespaces (No installation — works in your browser)"

    1. Open your repository on GitHub
    2. Click the green **Code** button
    3. Click the **Codespaces** tab
    4. Click **New codespace**

![Description](https://drive.google.com/thumbnail?id=1lnkuF-QzkFdXr8q1INQE0irPZQVGknJ3&sz=w800)

    5. Wait **1–2 minutes** for the environment to build
    6. A **live preview** of your site opens automatically in the browser panel


![Description](https://drive.google.com/thumbnail?id=1Jn3W1cEy9krticXtw2EnexbqDhcfEvN6&sz=w800)



    **To edit a page:**

    1. In the file explorer on the left, to navigate with the repo files
    2. Source Control: Git to stage, commit and push to update your website or update the code.
    3. Bavigation panel to find your files.
    4. Editing panel to open your file and edit the code.
    5. Terminal to send commands
    6. AI agent for assistance.


## Step 4 — Save and Publish Your Changes

Every time you save and push your changes to GitHub, the site rebuilds automatically.

for now we will edit the deploy.yml file to make sure we can deploy our github pages on gh-pages branch. 

Copy this code :

```
name: Deploy MkDocs to GitHub Pages

on:
  push:
    branches:
      - main

permissions:
  contents: write

jobs:
  deploy:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout code
        uses: actions/checkout@v4

      - name: Set up Python
        uses: actions/setup-python@v5
        with:
          python-version: 3.x

      - name: Install MkDocs
        run: pip install mkdocs mkdocs-material

      - name: Deploy to GitHub Pages
        run: mkdocs gh-deploy --force
```

=== "In Codespaces"

![Description](https://drive.google.com/thumbnail?id=1-cS4ArzwnVciyTFE9oA2gRRxOhs8rHHd&sz=w800)

Press `Ctrl+S` (or `Cmd+S` on Mac) to save your file
    
    1. Click the **Source Control** icon in the left sidebar (it looks like a branch)
    2. In the **Message** box, type a short description of your change  
       Example: `Update my About Me page`
    3. make sure those files you want to update on your website is added from chnages tab to staged changes

![Description](https://drive.google.com/thumbnail?id=1QcgkKp5AFyykePvM3KEKrDK0C4tOCieb&sz=w800)  

    4. Then once the files you want to update to your site is in the staged changes then:
        1. you can click on the arrow.
        2. Then click on commit and push.

OR you can also push the update using the terminal.

    !!! tip
        You can also use the terminal inside Codespaces:
        ```bash
        git add .
        git commit -m "Your message here"
        git push
        ```
---

## Step 5 — Watch the Deployment Run

1. Go to your repository on GitHub
2. Click the **Actions** tab
3. You will see a workflow called **Deploy MkDocs to GitHub Pages** running
4. Click on it to watch the progress
5. When it shows a **green tick ✅**, your site is live!

![Description](https://drive.google.com/thumbnail?id=1KySZrgKW3oe6maOd466TyzbNHe0LF_fs&sz=w800) 



!!! note "How long does it take?"
    Usually **1–3 minutes** from when you push your changes.

---

## Note

Now you can go to setting --> Pages and select "gh-pages" from select branch and then save. After sometime you will find your site link.

## Step 6 — Visit Your Live Website

Your site URL follows this pattern:

```
https://YOUR-USERNAME.github.io/YOUR-REPO-NAME/
```

**Example:** if your GitHub username is `ahmed` and the repo is `my-docs`:
```
https://ahmed.github.io/my-docs/
```

You can find the exact URL in **Settings → Pages** (it appears at the top once the site is live).

---

## 📝 What to Edit

| File | What it controls |
|------|-----------------|
| `mkdocs.yml` | Site name, your GitHub URL, social links |
| `docs/index.md` | Home page welcome message |
| `docs/about/index.md` | Your name, bio, skills, photo |
| `docs/documentation/` | Your notes and guides |
| `docs/projects/` | Your project writeups |

### Changing Your Site Name

Open `mkdocs.yml` and update the top lines:

```yaml
site_name: Ahmed's Documentation    # ← Your name/project
site_url: https://ahmed.github.io/my-docs/
site_author: Ahmed Al-Rashid

repo_url: https://github.com/ahmed/my-docs
repo_name: ahmed/my-docs
```

### Adding a New Page

1. Create a new `.md` file inside `docs/documentation/`
2. Add it to `mkdocs.yml` under the `nav:` section:

```yaml
nav:
  - Documentation:
      - Overview: documentation/index.md
      - My New Topic: documentation/my-new-topic.md   # ← add this
```

---

## ❓ Troubleshooting

| Problem | Solution |
|---------|----------|
| Actions tab shows a red ❌ | Click the failed run → read the error log → check your `mkdocs.yml` for typos |
| Site URL shows 404 | Go to **Settings → Pages** and confirm source is set to `gh-pages` branch |
| Changes not showing | Wait 2–3 minutes and refresh. If still not updated, check the Actions tab |
| Codespace preview not opening | In the terminal, run `mkdocs serve --dev-addr=0.0.0.0:8000` manually |

---

!!! success "You're done!"
    Your site is now live on the internet and updates automatically every time you push a change. 🎉
