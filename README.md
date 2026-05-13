# 🎯 YouTube Downloader (GitHub Actions)

Automatically download YouTube videos using GitHub Actions – no local tools needed, Free and without International Internet  .
Videos are stored directly in your repository, with optional subtitles, quality selection and password protection.

## ✨ Features

- 📥 Download one or multiple videos at once
- 🎬 Choose quality: best, 4K, 2K, 1080p, 720p, 480p, or audio only
- 📝 Download Persian and/or English subtitles (manual + auto‑generated)
- 🔒 Optional zip password protection for your files
- 📦 Large videos automatically split into 45MB parts for easier handling
- 🖼️ Thumbnails included in each video folder
- 📄 Detailed `README.md` per video with download links, file info, and extraction guide
- 🌐 Uses Cloudflare WARP proxy inside the runner for better connectivity

## 🚀 How to Use

### 1. Create your own copy

Fork this repository, or create a new repository and copy the workflow file into `.github/workflows/`.

> The workflow file is named: `01 - 🎯 دانلود یوتیوب.yml`

### 2. Enable GitHub Actions

Make sure Actions are enabled in your repository settings (they usually are by default).

### 3. Run the workflow

1. Go to the **Actions** tab of your repository.
2. Select the **01 - 🎯 دانلود یوتیوب** workflow.
3. Click **Run workflow**.
4. Fill in the parameters:

| Parameter              | Description |
|------------------------|-------------|
| `video_urls`           | **Required.** YouTube link(s). Separate multiple links with a space. |
| `download_subtitles`   | Check to download Persian and English subtitles. |
| `quality`              | Quality & type: `best`, `2160`, `1440`, `1080`, `720`, `480`, or `audio`. |
| `password`             | Optional password to protect the zip archive. |

5. Click **Run workflow**.

### 4. Find your downloaded files

After the workflow finishes:

- Browse to the `videos/` folder in your repository.
- Each video is stored in its own subfolder.
- Inside you'll find the video file (or split parts), a `thumbnail.jpg`, and a `README.md` with download links and extraction instructions.

## 📖 Video README Example

Every video folder contains a `README.md` that looks like this:

```markdown
# My Video Title
<div align="center">
  <picture>
    <img src="thumbnail.jpg" width="250" />
  </picture>
</div>

---
## Video Information
| Property | Value |
|----------|-------|
| **Video Name** | `My-Video-Title` |
| **Original Link** | [YouTube Video](https://youtube.com/...) |
| **Total Size** | **3 parts** - **134.50 MB** |
| **Quality** | **1080** |
| **Status** | **Complete (100%)** |
| **Password Protected** | **NO** |

---
## Download Links
> ⬇️ Download **all parts**, then open `My-Video-Title.zip` — the other parts are found automatically.

| # | File | Link |
|---|------|------|
| 1 | `My-Video-Title.zip` | [Download](raw-link) |
| 2 | `My-Video-Title.z01` | [Download](raw-link) |
| 3 | `My-Video-Title.z02` | [Download](raw-link) |

---
## How to Extract
Download all parts into the **same folder**, then:
...
```

## 📦 Working with Split Archives

If the file is larger than 45 MB, it's automatically split into parts:
- `.zip` – the main archive
- `.z01`, `.z02`, … – subsequent parts

**To extract:**
- **Windows**: Right‑click the `.zip` file → *Extract Here* (7‑Zip or WinRAR)
- **Mac**: Double‑click the `.zip` (Keka or The Unarchiver)
- **Linux**: `unzip My-Video-Title.zip`
- **Android**: Use ZArchiver

If a password was set, you'll be prompted for it during extraction.

## 🔤 Subtitles

When the subtitle option is enabled, a `subtitle.zip` file is added to the video folder. It contains `.vtt` files for Persian (`fa`) and English (`en`), both manual and auto‑generated (if available).

## 🛠️ Technical Details

- The workflow runs on **Ubuntu** with **180 minutes** timeout.
- It uses [`yt-dlp`](https://github.com/yt-dlp/yt-dlp) to download videos.
- A **Cloudflare WARP** proxy is started inside the runner to avoid regional blocks or rate‑limiting.
- Multiple download methods are tried (different player clients) to ensure success.
- Files are committed directly to the repository using GitHub Actions bot.
- The master list in `videos/README.md` is automatically updated with links to each video folder.

## ❓ Troubleshooting

- **Workflow fails with no video files**: Check that the YouTube link is valid and the video is not private/age‑restricted.
- **Push fails**: The workflow will retry up to 10 times. Large files may take a while. Ensure your repository has no size limits that could cause issues (GitHub has a soft limit around 1 GB per repo, but large binary files are not recommended).
- **WARP proxy not starting**: The workflow continues anyway; it just might be slower or blocked in some regions.

## 🤝 Contributing

Feel free to open issues or pull requests. This project is meant to be a simple, free YouTube download helper powered by GitHub Actions.

**Made with ❤️ and [yt-dlp](https://github.com/yt-dlp/yt-dlp)**
