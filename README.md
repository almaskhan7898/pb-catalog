# PicBeast Style Catalog

Static asset repository for [PicBeast](https://github.com/almaskhan7898/pb-catalog) — an AI portrait app. This repo contains style reference images and the master catalog file (`data.json`) that the app fetches at runtime. There is no application code here — only folders, images, and JSON.

## Folder Structure

```
pb-catalog/
├── data.json              # Master catalog (categories, styles, tiers)
├── styles/                # Full-size style reference images by category
│   ├── professional/
│   ├── rishta/
│   ├── casual/
│   ├── outdoor/
│   ├── dating/
│   └── social/
├── backgrounds/           # Background reference assets
│   ├── studio/
│   ├── outdoor/
│   └── abstract/
├── poses/                 # Pose reference assets
│   ├── standing/
│   ├── sitting/
│   └── candid/
└── thumbnails/            # 300px preview images for the catalog UI
```

## How the App Fetches Assets

The PicBeast app reads `data.json` from:

```
https://raw.githubusercontent.com/almaskhan7898/pb-catalog/main/data.json
```

Image paths in `data.json` are relative. The app prepends `base_url` to build full URLs, for example:

```
https://raw.githubusercontent.com/almaskhan7898/pb-catalog/main/styles/professional/suit_office_01.jpg
https://raw.githubusercontent.com/almaskhan7898/pb-catalog/main/thumbnails/suit_office_01_thumb.jpg
```

## Tier System

Each style has a `tier` that controls access in the app:

| Tier       | Description                                      |
|------------|--------------------------------------------------|
| `free`     | Available to all users                           |
| `creator`  | Requires Creator subscription                    |
| `pro`      | Requires Pro subscription                        |

## Image Naming Convention

- Use **lowercase** letters and **underscores** only
- End style IDs and filenames with a version suffix: `_01`, `_02`, etc.
- Style image: `styles/{category}/{id}.jpg` — e.g. `styles/casual/casual_tshirt_01.jpg`
- Thumbnail: `thumbnails/{id}_thumb.jpg` — e.g. `thumbnails/casual_tshirt_01_thumb.jpg`
- The `id` in `data.json` must match the filename (without extension) and be unique across the entire catalog

## How to Add a New Style

1. **Add the full-size image** — Place the reference image in the correct `styles/{category}/` folder using the naming convention above.
2. **Add the thumbnail** — Create a ~300px preview and save it in `thumbnails/` as `{id}_thumb.jpg`.
3. **Update `data.json`** — Add a new style entry under the appropriate category with `id`, `label`, `thumb`, `image`, `prompt_hint`, `tier`, `tags`, and `sort_order`. Bump `updated_at` to today's date.
4. **Git push** — Commit and push to `main` so the app can fetch the new assets via raw.githubusercontent.com.

## Important

**Never commit the following to this repo:**

- User photos or personal data
- API keys, secrets, or credentials
- AI-generated output images (only curated reference assets belong here)

This repository is public and served directly to client apps. Treat every file as production-facing.
