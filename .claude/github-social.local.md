---
# Image generation provider
provider: svg

# SVG-specific settings
svg_style: geometric

# Dark mode support
# false = light only, true = dark only, both = generate both variants
dark_mode: both

# Output settings
output_path: .github/social-preview.svg
dimensions: 1280x640
include_text: true
colors: auto

# README infographic settings
infographic_output: .github/readme-infographic.svg
infographic_style: hybrid

# Upload to repository (requires gh CLI or GITHUB_TOKEN)
upload_to_repo: false
---

# GitHub Social Plugin Configuration

This configuration was created by `/github-social:setup`.

## Provider: SVG (Default)

Claude generates clean, editable SVG graphics directly. No API key required.
- **Pros**: Free, instant, editable, small file size (10-50KB)
- **Style**: Geometric — complex arrangements with 8-15 shapes representing domain metaphors

## Dark Mode: Both

Generates light and dark variants automatically:
- `.github/social-preview.svg` (light)
- `.github/social-preview-dark.svg` (dark)

## Command Overrides

Override any setting via command flags:
```bash
/social-preview --provider=dalle-3 --dark-mode
/readme-enhance --provider=gemini
```
