# Eric Tapia | 35 Mill Interactive: Portfolio Site

A static single-page portfolio (HTML + CSS only, with no build step) that's ready for **GitHub Pages**.

## What's in this folder

```
index.html                      ← the page
style.css                       ← all styling (colors live at the top in :root)
Eric_Tapia_GameDev_Resume.pdf   ← downloadable resume
assets/
  banner.webp / banner.jpg      ← hero banner (1600×900)
  logo.webp / logo.jpg          ← circular shutter logo (512×512)
  favicon.png, apple-touch-icon.png, og-image.jpg
README.md                       ← this file
```

## Publish on GitHub Pages (step by step, for beginners)

Once you're done, your site will be at **https://YOUR-USERNAME.github.io**.

### 1. Create a GitHub account
1. Go to https://github.com/signup and create an account.
2. Choose your username carefully because it becomes part of your web address (for example `35mill` → `https://35mill.github.io`).
3. Verify your email address.

### 2. Create the repository
1. Sign in, then click the **+** in the top-right corner → **New repository**.
2. **Repository name:** type exactly `YOUR-USERNAME.github.io`, using your own GitHub username in lowercase.
   - Example: if your username is `35mill`, the name is `35mill.github.io`.
3. Set it to **Public**. (Free accounts need a public repo for Pages.)
4. Leave "Add a README" **unchecked**, because this folder already has one.
5. Click **Create repository**.

### 3. Upload the files
1. On the new, empty repository page, click the link **"uploading an existing file"**.
   (Or go to **Add file → Upload files**.)
2. Open this folder on your computer, select **everything inside it**
   (`index.html`, `style.css`, `README.md`, the PDF, **and the `assets` folder**), and drag it all into the browser window.
   - Drag the *contents* of the folder, not the folder itself. `index.html` has to sit at the top level of the repo, not inside a subfolder.
   - If your browser won't accept a folder, open `assets/` and drag its files in separately. Afterwards, check that they show up under `assets/`. If they don't, see Troubleshooting below.
3. Wait for every file to finish uploading. At the bottom, type a message such as `Initial site upload` and click **Commit changes**.

### 4. Turn on GitHub Pages
1. In the repo, click **Settings** (the gear tab at the top).
2. In the left sidebar, click **Pages**.
3. Under **Build and deployment → Source**, choose **Deploy from a branch**.
4. Under **Branch**, choose **main** and folder **/ (root)**, then click **Save**.
5. Wait 1–3 minutes, then refresh the page. A box will say **"Your site is live at https://YOUR-USERNAME.github.io"**.
   You can also open the **Actions** tab and watch the "pages build and deployment" run turn green.

### 5. Check it
- Open the link on your computer and on your phone.
- Test the **Download Resume** button, the YouTube video, every Steam Workshop link, Discord, and the email link.

## Updating the site later
- **Change text:** open `index.html` on GitHub, click the ✏️ pencil icon, edit, then **Commit changes**. The live site updates within a minute or two.
- **Replace the resume:** go to **Add file → Upload files** and upload a new PDF with the **same filename** (`Eric_Tapia_GameDev_Resume.pdf`). It will overwrite the old one.
- **Change colors:** edit the variables at the top of `style.css` (`--red`, `--bg`, `--silver`, and so on).

## Troubleshooting
| Problem | Fix |
|---|---|
| 404 page | Check that the repo name is exactly `username.github.io` and that `index.html` is at the top level. Then wait a few more minutes. |
| Images missing | The image files must be at `assets/banner.webp` and so on. File names are case-sensitive. To put a file in a folder through the web UI, choose **Add file → Create new file** and type `assets/` before the name, or re-upload the whole `assets` folder by dragging it. |
| Old version still showing | Hard-refresh with Ctrl+Shift+R (Windows) or Cmd+Shift+R (Mac). |
| Video doesn't play when opened from your computer | YouTube embeds can fail when the file is opened directly (`file://`). They work on the live github.io site. |

## Preview locally (optional)
Double-click `index.html`, or for the most accurate result run `python3 -m http.server` in this folder and open http://localhost:8000.
