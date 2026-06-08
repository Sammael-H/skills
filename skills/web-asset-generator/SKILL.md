---
name: web-asset-generator
description: Generate web assets including favicons, app icons (PWA), and social media meta images (Open Graph) for Facebook, Twitter, WhatsApp, and LinkedIn. Use when users need icons, favicons, social sharing images, or Open Graph images from logos or text slogans. Handles image resizing, text-to-image generation, and provides proper HTML meta tags.
---

# Web Asset Generator

Generate professional web assets from logos or text slogans, including favicons, app icons, and social media meta images.

## Quick Start

When a user requests web assets:

1. **Use AskUserQuestion tool to clarify needs** if not specified:
   - What type of assets they need (favicons, app icons, social images, or everything)
   - Whether they have source material (logo image vs text/slogan)
   - For text-based images: color preferences

2. **Check for source material**:
   - If user uploaded an image: use it as the source
   - If user provides text/slogan: generate text-based images

3. **Run the appropriate script(s)**:
   - Favicons/icons: `scripts/generate_favicons.py`
   - Social media images: `scripts/generate_og_images.py`

4. **Provide the generated assets and HTML tags** to the user

## Using Interactive Questions

**IMPORTANT**: Always use the AskUserQuestion tool to gather requirements instead of plain text questions. This provides a better user experience with visual selection UI.

### Why Use AskUserQuestion?

✅ **Visual UI**: Users see options as clickable chips/tags instead of typing responses
✅ **Faster**: Click to select instead of typing out answers
✅ **Clearer**: Descriptions explain what each option means
✅ **Fewer errors**: No typos or misunderstandings from free-form text
✅ **Professional**: Consistent with modern Claude Code experience

### Example Flow

**User request**: "I need web assets"

**Claude uses AskUserQuestion** (not plain text):
```
What type of web assets do you need?                          [Asset type]
☑ Favicons only - Browser tab icons (16x16, 32x32, 96x96) and favicon.ico
☑ App icons only - PWA icons for iOS/Android (180x180, 192x192, 512x512)
☑ Social images only - Open Graph images for Facebook, Twitter, WhatsApp, LinkedIn
☑ Everything - Complete package: favicons + app icons + social images
```
User clicks → Claude immediately knows what to generate

### Question Patterns

Below are the standard question patterns to use in various scenarios. Copy the structure and adapt as needed.

### Question Pattern 1: Asset Type Selection

When the user's request is vague (e.g., "create web assets", "I need icons"), use AskUserQuestion:

**Question**: "What type of web assets do you need?"
**Header**: "Asset type"
**Options**:
- **"Favicons only"** - Description: "Browser tab icons (16x16, 32x32, 96x96) and favicon.ico"
- **"App icons only"** - Description: "PWA icons for iOS/Android (180x180, 192x192, 512x512)"
- **"Social images only"** - Description: "Open Graph images for Facebook, Twitter, WhatsApp, LinkedIn"
- **"Everything"** - Description: "Complete package: favicons + app icons + social images"

### Question Pattern 2: Source Material

When you need to know what to generate from:

**Question**: "What source material do you have?"
**Header**: "Source"
**Options**:
- **"Logo image"** - Description: "I have an image file to use as the base"
- **"Emoji"** - Description: "Use an emoji character as the icon"
- **"Text/Slogan"** - Description: "Generate from text with custom colors"
- **"Logo + Text"** - Description: "Combine a logo image with text overlay"

### Question Pattern 3: Platform Selection

When generating social images and need to know which platforms:

**Question**: "Which platforms do you need social images for?"
**Header**: "Platforms"
**Options**:
- **"All platforms"** - Description: "Facebook, Twitter, WhatsApp, and LinkedIn"
- **"Facebook/LinkedIn"** - Description: "Standard 1200x630 Open Graph image"
- **"Twitter only"** - Description: "Twitter card image (1200x675)"
- **"Square variant"** - Description: "Square 1200x1200 for Instagram-style feeds"

### Question Pattern 4: Color Preferences

When creating text-based images:

**Question**: "What colors do you prefer for the images?"
**Header**: "Colors"
**Options**:
- **"Brand colors"** - Description: "I'll specify the hex codes for background and text"
- **"Default (Indigo)"** - Description: "Use the default indigo (#4F46E5) background with white text"
- **"Extract from logo"** - Description: "Sample colors from the uploaded logo"
- **"Gradient"** - Description: "Use a gradient background (specify colors)"

### Question Pattern 5: Icon Type Clarification

When user asks for "icons" without specifying favicon vs app icons:

**Question**: "What kind of icons do you need?"
**Header**: "Icon type"
**Options**:
- **"Website favicon"** - Description: "Small browser tab icon (16x16 to 96x96)"
- **"App icons"** - Description: "PWA/mobile icons (180x180, 192x192, 512x512)"
- **"Both"** - Description: "Complete set: favicons + app icons"

### Question Pattern 6: Emoji Selection

After running `--suggest` to get emoji options, present them using AskUserQuestion:

**Question**: "Which emoji best represents your project?"
**Header**: "Emoji"
**Options**: (dynamically generated from suggest_emojis output — show up to 4)
- **"{emoji} {Name}"** - Description: "{keywords from emoji data}"

### Question Pattern 7: Code Integration

After generating assets, offer to add the HTML tags:

**Question**: "Would you like me to add the HTML tags to your project?"
**Header**: "Integration"
**Options**:
- **"Auto-detect setup"** - Description: "I'll find your HTML/framework files and add the tags"
- **"Tell me the file"** - Description: "Specify which file to update"
- **"Just show me the tags"** - Description: "Display the HTML tags for me to add manually"
- **"Skip for now"** - Description: "I'll handle it later"

### Question Pattern 8: Testing Links

After integration, offer validation options:

**Question**: "Would you like to test how your social images look?"
**Header**: "Testing"
**Options**:
- **"Open Graph debugger"** - Description: "Test Facebook/LinkedIn preview with Meta's debugger"
- **"Twitter card validator"** - Description: "Validate Twitter card appearance"
- **"Both"** - Description: "Check both Facebook and Twitter previews"
- **"Skip testing"** - Description: "I'll test later"

## Asset Generation Workflow

### Favicons from Image

```bash
python scripts/generate_favicons.py logo.png output/ all
```

This generates:
- `favicon.ico` (16x16, 32x32 multi-resolution)
- `favicon-16x16.png`
- `favicon-32x32.png`
- `favicon-96x96.png`
- `apple-touch-icon.png` (180x180)
- `android-chrome-192x192.png`
- `android-chrome-512x512.png`

### Favicons from Emoji

```bash
# Get emoji suggestions first
python scripts/generate_favicons.py --suggest "coffee shop" output/ all

# Then generate with chosen emoji
python scripts/generate_favicons.py --emoji "☕" --emoji-bg "#F5DEB3" output/ favicon
```

### Social Media Images from Text

```bash
python scripts/generate_og_images.py output/ --text "Welcome to My App" --bg-color "#4F46E5" --text-color white
```

### Social Media Images from Logo

```bash
python scripts/generate_og_images.py output/ --image logo.png
```

### With Validation

```bash
python scripts/generate_favicons.py logo.png output/ all --validate
python scripts/generate_og_images.py output/ --text "My App" --validate
```

## Delivery Workflow

After generating assets:

1. **Move files** to the project's output directory
2. **Display HTML meta tags** for the generated assets
3. **Offer code integration** using framework detection
4. **Provide testing links** for validation across platforms

### HTML Tags for Favicons

```html
<link rel="icon" type="image/png" sizes="32x32" href="/favicon-32x32.png">
<link rel="icon" type="image/png" sizes="16x16" href="/favicon-16x16.png">
<link rel="icon" type="image/png" sizes="96x96" href="/favicon-96x96.png">
<link rel="apple-touch-icon" sizes="180x180" href="/apple-touch-icon.png">
<link rel="icon" type="image/png" sizes="192x192" href="/android-chrome-192x192.png">
<link rel="icon" type="image/png" sizes="512x512" href="/android-chrome-512x512.png">
```

### HTML Tags for Social Images

```html
<!-- Open Graph / Facebook -->
<meta property="og:image" content="/og-image.png">
<meta property="og:image:width" content="1200">
<meta property="og:image:height" content="630">
<meta property="og:image:alt" content="Your description here">

<!-- Twitter -->
<meta name="twitter:card" content="summary_large_image">
<meta name="twitter:image" content="/twitter-image.png">
<meta name="twitter:image:alt" content="Your description here">
```

## Framework Detection

Auto-detect and integrate with:
- **Next.js** (App Router): `app/layout.tsx` metadata API
- **Next.js** (Pages Router): `pages/_document.tsx` or `_app.tsx`
- **Astro**: `src/layouts/Layout.astro`
- **SvelteKit**: `src/app.html`
- **Vue/Nuxt**: `nuxt.config.ts` or `index.html`
- **Plain HTML**: `index.html` or `<head>` section
- **Gatsby**: `gatsby-config.js` or `src/html.js`

## Quality Assurance

Optional validation checks (use `--validate` flag):
- File sizes within platform limits (Facebook: 8MB, Twitter: 5MB)
- Dimensions matching platform specifications
- Format compatibility
- Accessibility contrast ratios (WCAG 2.0 AA/AAA standards)

## Technical Requirements

- Python 3.6+
- `pip install Pillow` (required)
- `pip install pilmoji` (optional, for emoji rendering)
- `pip install "emoji<2.0.0"` (optional, for emoji library support)
