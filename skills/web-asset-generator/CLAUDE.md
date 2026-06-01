# Web Asset Generator - Developer Guide

This is a Claude Skill that automatically triggers when users request web assets like favicons or social media images. The skill uses Python scripts to generate these assets from either images or emoji inputs.

## Project Structure

```
skills/web-asset-generator/
├── SKILL.md                     # Skill entry point with trigger descriptions
├── CLAUDE.md                    # This file - developer documentation
├── scripts/
│   ├── generate_favicons.py     # Favicon and app icon generation
│   ├── generate_og_images.py    # Open Graph / social media image generation
│   ├── emoji_utils.py           # Emoji suggestion and rendering utilities
│   └── lib/
│       └── validators.py        # File size, dimension, and WCAG validation
└── references/
    └── specifications.md        # Platform specs and best practices
```

## Core Capabilities

### 1. Favicon / App Icon Generation (`generate_favicons.py`)

Supports multiple generation modes:
- **From image**: Resize any image to all standard favicon/icon sizes
- **From emoji**: Render an emoji character at any size with optional background
- **Emoji suggestions**: Auto-suggest relevant emojis from a project description

Sizes generated:
- Favicons: 16x16, 32x32, 96x96 (PNG) + multi-resolution favicon.ico
- App icons: 180x180 (iOS), 192x192 (Android), 512x512 (Android/PWA)

Key behaviors:
- Uses LANCZOS resampling for high-quality resizing
- Transparent backgrounds for favicons, solid backgrounds for app icons (iOS requirement)
- Emoji auto-scales to 75% of minimum dimension

### 2. Open Graph Image Generation (`generate_og_images.py`)

Generates social media preview images:
- **Standard OG**: 1200x630 (Facebook, LinkedIn, WhatsApp)
- **Twitter**: 1200x675 (16:9 ratio)
- **Square**: 1200x1200

Text-based generation features:
- Dynamic font sizing based on text length (144px → 84px as text gets longer)
- Logo overlay support (max 20% of image height, centered at top)
- Word-wrap with configurable max width (85% of image width)

Image resize modes:
- **Cover**: Crops to fill dimensions (default)
- **Contain**: Preserves aspect ratio with borders

### 3. Emoji Utilities (`emoji_utils.py`)

Two main features:

**Emoji Suggestion System:**
- Database of ~80 curated emojis with keywords and categories
- Keyword extraction from project descriptions (removes stop words)
- Scoring: exact match (10pts), partial match (5pts), name match (8pts)
- Category diversity: tries to return emojis from different categories
- Falls back to generic popular emojis if no matches found

**Emoji Rendering:**
- Primary: `generate_emoji_icon()` using Pilmoji library
- Fallback: `generate_emoji_icon_fallback()` using system fonts
  - Tries: Apple Color Emoji (macOS), NotoColorEmoji (Linux), Segoe UI Emoji (Windows)

### 4. Validation (`lib/validators.py`)

Validates generated assets against platform requirements:

Platform limits:
- Facebook: 8MB max, 1200x630 recommended, min 600x315
- Twitter: 5MB max, 1200x675 recommended, min 300x157
- LinkedIn: 5MB max, 1200x627 recommended
- WhatsApp: 8MB max, 1200x630 recommended

Accessibility:
- WCAG 2.0 contrast ratio calculation using relative luminance
- AA standard: 4.5:1 (normal text), 3.0:1 (large text)
- AAA standard: 7.0:1 (normal text), 4.5:1 (large text)

## Dependencies

Required:
- Python 3.6+
- Pillow (`pip install Pillow`)

Optional:
- pilmoji (`pip install pilmoji`) — for emoji rendering via Pilmoji
- emoji (`pip install "emoji<2.0.0"`) — use version <2.0.0 for compatibility

## Development Notes

- All scripts import from `lib/validators.py` using relative imports with fallbacks
- `emoji_utils.py` is imported by `generate_favicons.py` with fallback handling
- Scripts degrade gracefully when optional dependencies are unavailable
- Validation is opt-in via `--validate` flag to keep default output clean
