---
name: web-asset-generator
description: Generate professional web assets — favicons, PWA app icons, and social media meta images (Open Graph) — from logos, emojis, or text slogans.
license: MIT
---

# Web Asset Generator

Generate favicons, app icons, and social media meta images for websites and apps.

## Asset Types

- **Favicons**: Browser tab icons (16×16, 32×32, 96×96, favicon.ico)
- **App Icons**: PWA/mobile icons (180×180, 192×192, 512×512)
- **Social Images**: Open Graph images for Facebook (1200×630), Twitter (1200×675), LinkedIn, WhatsApp

## Quick Start

**Before running**, check dependencies:
```bash
python scripts/check_dependencies.py
```

If Pillow is missing:
```bash
pip install Pillow --break-system-packages
```

For emoji support (optional):
```bash
pip install pilmoji 'emoji<2.0.0'
```

## Workflows

### 1. Favicons/App Icons from Logo Image
```bash
python scripts/generate_favicons.py <source_image> <output_dir> [all|favicon|app]
```

### 2. Favicons from Emoji
```bash
# Get emoji suggestions based on project description
python scripts/generate_favicons.py --suggest "your project description" <output_dir>

# Generate from chosen emoji
python scripts/generate_favicons.py --emoji "🚀" <output_dir> all
python scripts/generate_favicons.py --emoji "☕" --emoji-bg "#F5DEB3" <output_dir> favicon
```

### 3. Open Graph Images from Text
```bash
python scripts/generate_og_images.py <output_dir> --text "Your Tagline"
python scripts/generate_og_images.py <output_dir> --text "My App" --logo logo.png
python scripts/generate_og_images.py <output_dir> --text "Hello" --bg-color "#FF5733" --text-color "#FFFFFF"
```

### 4. Open Graph Images from Existing Image
```bash
python scripts/generate_og_images.py <output_dir> --image photo.jpg
```

### 5. Validate Generated Assets
Add `--validate` to any command:
```bash
python scripts/generate_favicons.py logo.png output/ all --validate
python scripts/generate_og_images.py output/ --text "My Site" --validate
```

## Interaction Guidelines

Use interactive questions rather than plain text when clarifying:
- Which asset types are needed (favicons, app icons, social images, or all)
- Source material (upload logo, use emoji, or enter text/slogan)
- Platform selection for social images
- Color preferences for text-based images
- Framework detection for code integration (Next.js, Astro, SvelteKit, Nuxt, etc.)

## Asset Delivery

After generation:
1. Move files to the appropriate output directory
2. Display the generated HTML meta tags and link elements
3. Offer to auto-insert tags into framework config files (with diff preview before committing)
4. Suggest testing tools: Facebook Sharing Debugger, Twitter Card Validator, LinkedIn Post Inspector

## Reference

See `references/specifications.md` for detailed platform specs, aspect ratios, file size limits, and best practices.
