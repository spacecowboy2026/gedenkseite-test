# Olaf Margraf Memorial Page

A single-page memorial website. Plain static HTML, CSS and a little vanilla JavaScript.
No framework, no build step, no dependencies, no server code.

> **For humans:** a simple step-by-step guide is in [HOW-TO-PUBLISH.md](HOW-TO-PUBLISH.md).
> **For AI assistants:** this README is written so that it can be given to an AI coding assistant as the full task description. Everything the assistant needs is below.

---

## Task for the AI assistant

**Goal:** Publish this folder as a website with GitHub Pages, using an existing GitHub repository. The contents of this folder must **replace** the website files that are currently in that repository.

**Ask the repository owner first, do not guess:**
1. The repository name or URL.
2. Whether the site should use a custom domain, and if yes, which one.

### Hard rules
- Do **not** change any text, names, dates, images, colours or layout. The image order may only be changed if the owner asks for it. This is a memorial page and the content is final.
- Do **not** add a framework, bundler, package.json, build step, analytics, cookies or tracking.
- Do **not** delete the repository's `.git` folder or its history.
- If the repository already contains a file named `CNAME`, **keep it unchanged**. It holds the custom domain. Deleting it takes the domain offline.
- Do **not** force-push. Make a normal commit on top of the existing history.
- Do not add any other photos. Only the `.jpg` files in this folder are meant to be public.

### Steps
1. Clone the existing repository.
2. Find out which branch and folder GitHub Pages currently serves. Check the repository under *Settings, Pages*, or run `gh api repos/OWNER/REPO/pages`. It is usually branch `main`, folder `/ (root)`. Less often it is the `/docs` folder or a `gh-pages` branch.
3. In that served location, delete all old website files. Keep `.git`, and keep `CNAME` if it exists.
4. Copy the **contents** of this folder into that location, so that `index.html` sits directly at the top level of the served location. Do not nest it inside a subfolder, otherwise the site shows a 404 page.
5. Commit with a message such as `Replace site with new memorial page` and push.
6. Make sure GitHub Pages is enabled: *Settings, Pages, Build and deployment, Source: Deploy from a branch*, then the branch and folder from step 2.
7. Wait for the Pages deployment to finish. It normally takes one to two minutes. The status is visible in the repository's *Actions* tab.
8. Open the live URL and run the checks below.

### Custom domain, only if the owner wants one
- Enter the domain under *Settings, Pages, Custom domain*. GitHub then creates or updates the `CNAME` file itself.
- DNS records at the domain provider, for an apex domain such as `example.com`, four `A` records:
  ```
  185.199.108.153
  185.199.109.153
  185.199.110.153
  185.199.111.153
  ```
- For `www.example.com`, one `CNAME` record pointing to `OWNER.github.io`.
- After DNS has propagated, tick *Enforce HTTPS* on the Pages settings screen.

### Checks after publishing
- [ ] The page loads without a 404.
- [ ] The slideshow on the left shows a photo, and after about five seconds it crossfades to the next one.
- [ ] The portrait photo next to the quote is visible.
- [ ] The round button at the bottom right switches between the dark and the light colour scheme.
- [ ] Clicking or tapping the pill "Naline, Rena und Ole mit Familien" releases small floating hearts.
- [ ] The button "Olaf’s Song" at the bottom left plays and pauses the song.
- [ ] The small line "In Liebe, dein Sohn" with a kite icon is at the very bottom.
- [ ] The browser console shows no missing files.
- [ ] On a phone, the slideshow sits on top and the text below it, with no sideways scrolling.

---

## Project structure

```
index.html          The whole page: markup, texts and small inline scripts
style.css           All styles. Colour schemes are defined at the very top
01.jpg … 29.jpg     Slideshow photos, shown in numerical order
NN-ganz.jpg         Same, but this photo is shown completely instead of cropped (see below)
segeln.jpg          Sailing boat at sunset, always the last slide
olaf.jpg            Portrait shown next to the quote
olafs-song.mp3      The song, sung by Olaf himself. Played by the button at the bottom left
.nojekyll           Tells GitHub Pages to serve the files as they are
.gitignore          Keeps the large original photos out of the repository
README.md           This file
HOW-TO-PUBLISH.md   Simple guide for humans
```

**All files live in one flat folder on purpose.** There are no subfolders, so nothing can get lost when files are uploaded by drag and drop. Every file must sit at the top level of the published site, next to `index.html`.

All paths in the code are **relative**. The site therefore works at a domain root, for example `https://example.com/`, and equally in a project subpath, for example `https://owner.github.io/repo/`. No base URL needs to be configured.

## Hosting note
The instructions above describe GitHub Pages. The site also works unchanged on Vercel, Netlify or any other static host connected to the repository. In that case skip the GitHub Pages settings. No build command and no output directory are needed.

## How the page works
- **Layout.** Two equal panels side by side with an 8px gap. Below 992px width they stack, slideshow first.
- **Slideshow.** There is no list of images in the code. The page simply loads `01.jpg`, `02.jpg`, `03.jpg` and so on, five seconds each with a soft crossfade. For every number it first tries `NN.jpg` and then `NN-ganz.jpg`. The first number for which neither file exists ends the series. Then `segeln.jpg` is shown and the slideshow starts again at `01`. Two missing-file requests (404) at the end of the first round are therefore expected and harmless.
  - **Change the order:** renumber the files. **Add a photo:** give it the next free number. **Remove a photo:** delete it and renumber so that no gap remains.
  - Numbers must be two digits, continuous, without gaps, and the extension must be lowercase `.jpg`.
  - `NN-ganz.jpg` ("ganz" is German for "whole") shows a photo completely over a blurred copy of itself. Use it for landscape group photos that would lose people when cropped. All other photos fill the panel and are cropped around the upper middle.
  - When photos are renamed, delete the old files on the server. Do not leave old numbers lying around.
- **Colour scheme.** Dark is the default, with background `#060810`. The light scheme is set through `data-theme="light"` on the `<html>` element. The visitor's choice is stored in `localStorage` under the key `theme`.
- **Hearts.** A click on the `.badge` button creates sixteen small SVG hearts that are animated with the Web Animations API and then removed. Visitors who prefer reduced motion only get a short pulse.
- **Song.** `olafs-song.mp3` starts by itself where the browser allows it. Most browsers, especially on phones, block sound until the visitor touches the page. In that case the song starts with the first tap, click or key press anywhere on the page. The pill button at the bottom left pauses and resumes it. If the visitor pauses, nothing restarts it automatically.
- **Cache busting.** `index.html` loads the stylesheet as `style.css?v=…`. Whenever `style.css` changes, change that value as well, otherwise returning visitors keep seeing the old styles from their browser cache.
- **Font.** "Host Grotesk" is loaded from Google Fonts. There are no other external requests.

## Search engines
The page is meant to be found through Google and other search engines. It contains no `noindex` tag and no `robots.txt` that blocks crawlers. Do not add either.

## Language
The page content is in German and must stay in German.
