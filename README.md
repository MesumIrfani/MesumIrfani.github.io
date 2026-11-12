# Mesum Ali Irfani, portfolio website

A single-page, multi-tab portfolio. No build step, no framework. Edit one HTML file, drop media into two folders, push to GitHub, done.

## 1. What is in this folder

```
index.html              the whole site (all tabs, styles and scripts)
README.md               this guide
.nojekyll               tells GitHub Pages to serve files as they are
CNAME                   your custom domain (mesumirfani.com); GitHub Pages reads it, keep it
images/                 photos, figures, certificate previews and video poster frames
certs/                  certificate PDFs linked from the Education tab
art/                    artwork images for the Art tab (add new ones here and copy a <figure> block)
videos/                 MP4 clips (short loops and full videos)
cv.pdf                  ADD THIS: your CV, linked from the "Download CV" button
ms-degree.pdf           ADD THESE (optional): degree and transcript PDFs linked
ms-transcript.pdf       from the Education tab. Delete the buttons if you
bs-degree.pdf           would rather not publish them.
bs-transcript.pdf
```

## 2. Editing the site

Open `index.html` in any text editor (VS Code is free and highlights HTML). The file is organised top to bottom:

1. `<style>` block: colours, fonts and layout. The colour and font settings are the `:root` block at the top.
2. `<header class="top">`: the tab bar. Add or remove tabs here.
3. One `<section class="page" data-page="...">` per tab, in this order: home, about, research, projects, uav, publications, experience, education, honors.
4. `<aside class="side">`: the profile sidebar shown on every tab (photo, title, quote, Connect links).
5. `<script>` at the bottom: tab switching and the image lightbox. If you add a tab, add its name to the `pages` list here.

Every spot that still needs your input is marked with an HTML comment, for example `<!-- Fill in start year -->`. Search the file for `<!--` to find them all.

### Adding a photo
1. Resize it to about 1400 px on the long side (any photo editor, or https://squoosh.app) and save as JPG.
2. Put it in `images/`.
3. Find the placeholder, which looks like `<div class="ph" data-label="SOMETHING"></div>`, and replace it with:
   ```html
   <img src="images/your-photo.jpg" alt="What the photo shows" loading="lazy">
   ```
   Inside a `.media` grid use the figure form so it gets a caption and the click-to-enlarge:
   ```html
   <figure><img class="r169 zoom" src="images/your-photo.jpg" alt="..." loading="lazy"><figcaption>Caption</figcaption></figure>
   ```
   `r169`, `r43`, `r916` and `r1` set the crop shape (16:9, 4:3, 9:16 portrait, square).

### Adding a short looping clip (plays like a GIF)
MP4 is far smaller than GIF and looks better. Convert with ffmpeg (free, https://ffmpeg.org):
```
ffmpeg -i input.mp4 -t 15 -vf "fps=24,scale=960:-2" -an -c:v libx264 -crf 27 -pix_fmt yuv420p -movflags +faststart videos/my-clip.mp4
ffmpeg -ss 2 -i videos/my-clip.mp4 -frames:v 1 images/my-clip-poster.jpg
```
Then in the page:
```html
<figure><span class="badge">Animation</span><video class="r169 zoom" src="videos/my-clip.mp4" poster="images/my-clip-poster.jpg" autoplay muted loop playsinline preload="metadata"></video><figcaption>Caption</figcaption></figure>
```

### Adding a full video with controls
Keep each file under about 30 MB (GitHub rejects files over 100 MB). For anything longer, upload to YouTube as Unlisted and embed:
```html
<iframe width="100%" style="aspect-ratio:16/9;border:0" src="https://www.youtube.com/embed/VIDEO_ID" allowfullscreen></iframe>
```

### Adding a project
Copy an existing `<div class="entry">...</div>` block inside the Projects (or UAV) section and edit the label, title, text, tags and media.

### Adding a news item
Copy one `<article>` inside `<div class="news">` on the Home tab. Newest goes first.

### Checking your edits locally
Just double-click `index.html` to open it in a browser. Everything works offline except the Google font (it falls back to Cambria, which you have on Windows).

## 3. Deploying on GitHub Pages (free)

You need a GitHub account (you have one: MesumIrfani).

### One-time setup
1. On GitHub click **New repository**. Name it exactly `MesumIrfani.github.io`, set it to **Public**, do not add a README. Create it.
2. Install GitHub Desktop (https://desktop.github.com) or use git on the command line. The steps below use the command line; GitHub Desktop does the same with buttons (Add local repository, Commit, Push).
3. Open a terminal in this folder and run:
   ```
   git init
   git add .
   git commit -m "Portfolio website"
   git branch -M main
   git remote add origin https://github.com/MesumIrfani/MesumIrfani.github.io.git
   git push -u origin main
   ```
4. On GitHub open the repository, go to **Settings > Pages**. Under **Build and deployment** set Source to **Deploy from a branch**, Branch to **main** and folder to **/ (root)**. Save.
5. Wait one or two minutes, then open **https://mesumirfani.github.io**. That is your live site.

### Every later update
```
git add .
git commit -m "Describe what you changed"
git push
```
The live site updates within a minute or two.

## 4. Your own domain (optional, about USD 10 to 15 per year)

A domain such as `mesumirfani.com` looks better on applications than a github.io address.

1. Buy the domain from any registrar (Namecheap, Porkbun, Cloudflare and GoDaddy all work).
2. In the registrar's DNS settings add:
   - Four **A** records for `@` (the bare domain) pointing to `185.199.108.153`, `185.199.109.153`, `185.199.110.153`, `185.199.111.153`
   - One **CNAME** record for `www` pointing to `mesumirfani.github.io`

   These are GitHub's published addresses at the time of writing; confirm them on the GitHub Pages documentation page for custom domains before you use them.
3. In the repository go to **Settings > Pages > Custom domain**, enter `mesumirfani.com`, save, and tick **Enforce HTTPS** once it becomes available (can take up to a day).
4. The `CNAME` file in this folder already holds `mesumirfani.com`, so GitHub fills the Custom domain box as soon as you push. Keep that file.

## 5. Alternatives to GitHub Pages

- **Netlify** (https://app.netlify.com/drop): drag this whole folder onto the page and it is live in seconds, with a random address you can rename. Good for a quick preview.
- **Cloudflare Pages**: connect the GitHub repository and it deploys on every push, with a free custom domain and fast video delivery worldwide.

## 6. Before you publish, check

- [ ] `cv.pdf` is in the folder and up to date
- [ ] The two `20XX` start years in Experience are filled in
- [ ] The paper's author list matches your submission
- [ ] Google Scholar and ORCID links are added or removed
- [ ] Every photo and video from NaqCoDE is cleared for public use, and no document numbers, drawings, numbers or logos appear in it
- [ ] Colleagues who appear in photos are fine with being on the site
- [ ] Open the site on your phone once; the tab bar scrolls sideways there

## 7. Media already in this folder

| File | Used in | Source |
|---|---|---|
| videos/thesis-summary.mp4 | Research | Your 3-minute thesis video, institution logos removed, closing credits trimmed |
| videos/banner-launch.mp4 | Home banner | 14 s cut of the flight-test video: Mesum at the launcher, then the launch and flight |
| videos/flight-testing.mp4 | UAV tab | Flight test video, full |
| videos/engine-bench-1/2.mp4 | UAV tab | Engine bench clips |
| videos/turbojet-loop.mp4, turbojet-test.mp4 | UAV tab | 20 s loop and full 3 min run |
| videos/slam-mapping/-navigation/-noise.mp4 | Projects | Extracted from the SLAM presentation, cropped to the RViz map and sped up |
| videos/rot3u-pouring.mp4 | Projects | Extracted from the ROT3U presentation, 1.5x speed |
| videos/drone-flying.mp4 | UAV tab, Personal | Trimmed so the building sign is not shown |
| images/slam-gazebo.jpg, slam-map.jpg | Projects | Extracted from the SLAM presentation |
| images/rot3u-arm.jpg | Projects | Extracted from the ROT3U presentation |
| images/electric-aircraft-3view.jpg, -cfd.jpg | UAV tab | Figures from your BS final year report |
| images/pcg-waveforms.png | Projects | Drawn from the sample recordings in your ML project |
| images/*-poster.jpg | everywhere | Still frames shown before each video plays |

From the solid rocket motor presentation and reports only text-free CAD renders and one methodology flowchart were used; the documents are marked confidential, so see the note below.

### MCS-Connect figures (added later)
`images/mcs-*.jpg` are figures taken from the submitted manuscript (Figures 2 to 7 and 10) and `videos/mcs-paths.mp4` is a slideshow of three of them. If the journal's copyright agreement restricts reuse after acceptance, most publishers still allow figures on an author's personal site; check the agreement when the paper is accepted.
