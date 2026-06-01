# Web Asset Specifications and Best Practices

## Favicon Specifications

### Standard Sizes

| Size | Use Case |
|------|----------|
| 16x16 | Browser tabs |
| 32x32 | Standard browsers and taskbars |
| 96x96 | Google TV |
| favicon.ico | Multi-resolution (16x16, 32x32) |

### Best Practices
- Use simple, recognizable designs that work at small sizes
- Ensure good contrast for visibility against both light and dark browser UI
- Test icons against both light and dark backgrounds
- Avoid excessive detail that becomes invisible at minimal dimensions
- Keep file size under 100KB per PNG file

## App Icons (PWA/Mobile)

### Sizes

| Size | Platform |
|------|----------|
| 180x180 | iOS Safari (apple-touch-icon) |
| 192x192 | Android Chrome |
| 512x512 | Android Chrome high-res and PWA splash screens |

### Best Practices
- Use square images with no transparency (or solid background)
- iOS rounds corners automatically — keep important content away from edges
- Android may apply masks — design for a circular crop safe zone
- Account for platform-specific treatments when designing

## Open Graph (Social Media Meta Images)

### Primary Sizes

| Size | Ratio | Platforms |
|------|-------|-----------|
| 1200x630 | 1.91:1 | Facebook, LinkedIn, WhatsApp |
| 1200x675 | 16:9 | Twitter |
| 1200x1200 | 1:1 | Square variants |

### Platform-Specific Guidelines

**Facebook**
- Recommended: 1200x630
- Minimum: 600x315
- Max file size: 8MB
- Formats: PNG, JPG

**Twitter**
- Large image card: 1200x675
- Standard card: 1200x1200
- Max file size: 5MB
- Formats: PNG, JPG, WEBP

**LinkedIn**
- Recommended: 1200x627
- Max file size: 5MB
- Formats: PNG, JPG

**WhatsApp**
- Uses Open Graph tags (same as Facebook)
- Recommended: 1200x630
- Max file size: 8MB

### Content Best Practices
- Keep important content in the "safe zone" (center 80% of image)
- Use font sizes of 80-120px for 1200px width images
- Text should remain large and readable
- Maximum ~40 characters per line
- Use high-contrast text (check WCAG guidelines)

## HTML Implementation

### Favicon Tags
```html
<link rel="icon" type="image/png" sizes="16x16" href="/favicon-16x16.png">
<link rel="icon" type="image/png" sizes="32x32" href="/favicon-32x32.png">
<link rel="icon" type="image/png" sizes="96x96" href="/favicon-96x96.png">
<link rel="apple-touch-icon" sizes="180x180" href="/apple-touch-icon.png">
<link rel="icon" type="image/png" sizes="192x192" href="/android-chrome-192x192.png">
<link rel="icon" type="image/png" sizes="512x512" href="/android-chrome-512x512.png">
```

### Open Graph Tags
```html
<!-- Primary OG tags -->
<meta property="og:image" content="https://example.com/og-image.png">
<meta property="og:image:width" content="1200">
<meta property="og:image:height" content="630">
<meta property="og:image:alt" content="Description of image">

<!-- Twitter Card -->
<meta name="twitter:card" content="summary_large_image">
<meta name="twitter:image" content="https://example.com/twitter-image.png">
<meta name="twitter:image:alt" content="Description of image">
```

## File Format Guidelines

| Format | Best For |
|--------|----------|
| PNG | Icons with transparency, graphic-based OG images |
| JPEG | Photographic OG images |
| ICO | favicon.ico (multi-resolution) |

- Use RGB color mode (not CMYK)
- Keep files under 1MB for fast loading
- Optimize PNG files with lossless compression

## Accessibility (WCAG 2.0)

### Contrast Ratios
- AA Normal text: 4.5:1 minimum
- AA Large text (18pt+ or 14pt+ bold): 3.0:1 minimum
- AAA Normal text: 7.0:1 minimum
- AAA Large text: 4.5:1 minimum

### Common Color Combinations

| Background | Text | Ratio | Standard |
|------------|------|-------|----------|
| #000000 | #FFFFFF | 21:1 | AAA |
| #4F46E5 | #FFFFFF | ~5.7:1 | AA |
| #FFFFFF | #000000 | 21:1 | AAA |
| #808080 | #FFFFFF | ~3.9:1 | AA Large only |

## Testing and Validation

### Official Validation Tools
1. [Facebook Sharing Debugger](https://developers.facebook.com/tools/debug/)
2. [Twitter Card Validator](https://cards-dev.twitter.com/validator)
3. [LinkedIn Post Inspector](https://www.linkedin.com/post-inspector/)

### Pre-Launch Checklist
- [ ] Test at all zoom levels (100%, 200%)
- [ ] Check favicon on both light and dark browser themes
- [ ] Preview social images on each target platform
- [ ] Test mobile rendering on iOS and Android
- [ ] Verify load times (all images under 1MB)
- [ ] Confirm text legibility across all sizes
- [ ] Use absolute URLs in meta tags (not relative)
- [ ] Validate HTML tags are in `<head>` section

## Common Pitfalls

1. **Too much detail in small icons** — simplify for 16x16 and 32x32
2. **Text too small** — minimum 80px font size for social images
3. **Forgetting safe zones** — keep content in center 80% of social images
4. **Wrong aspect ratio** — causes unwanted cropping on platforms
5. **Oversized files** — hurts performance; optimize before deploying
6. **Relative URLs** — use absolute URLs in `og:image` meta tags
7. **Missing alt text** — always add `og:image:alt` for accessibility
8. **No platform testing** — verify on each target platform before launch
