# Satio Waitlist Landing Page

A high-converting waitlist page for the Satio AI nutrition app.

## Quick Start

1. Open `index.html` in a browser to preview locally
2. Deploy to Vercel, Netlify, GitHub Pages, or any static hosting

## Features

- **Single-page design** — Everything in one clean HTML file
- **Mobile-first responsive** — Works on all devices
- **Referral system** — Queue position + shareable referral links with rewards
- **Brand-compliant** — Uses Satio brand colors and typography
- **No dependencies** — Pure HTML/CSS/JS, no frameworks needed
- **Supabase integration** — Real-time waitlist with referral tracking
- **Kit (ConvertKit)** — Email marketing and welcome email automation

## Structure

```
waitlist-github/
├── index.html              # Main landing page (v1)
├── index-v2.html           # Enhanced landing page with illustrations
├── index-v3.html           # Latest version with full feature set
├── privacy.html            # Privacy policy
├── terms.html              # Terms of service
├── README.md               # This file
├── assets/
│   ├── satio_logo.svg      # Logo (SVG)
│   ├── satio_logo.webp     # Logo (WebP)
│   ├── logo.svg            # Alternative logo
│   ├── icon-*.svg          # Feature icons
│   ├── ic_*.svg            # Widget icons
│   ├── ICONS_REFERENCE.md  # Icon documentation
│   ├── OG_IMAGE_SPECS.md   # Open Graph image specs
│   └── illustrations/      # Satio character illustrations
├── emails/
│   └── welcome-email.html  # Welcome email template
├── referral-system/
│   ├── README.md           # Referral system documentation
│   └── EMAIL_SETUP.md      # Email integration setup
└── sunflower-option-*.html # Alternative design options
```

## Deployment

### Vercel (Recommended)
```bash
npx vercel
```

### Netlify
1. Drag & drop this folder to [netlify.com/drop](https://netlify.com/drop)
2. Or connect via Git for automatic deploys

### GitHub Pages
1. Push to a GitHub repo
2. Go to Settings → Pages
3. Select branch and root folder as source

## Configuration

### Supabase (Waitlist Database)
The landing pages use Supabase for waitlist storage. Update these values in the HTML:
```javascript
const SUPABASE_URL = 'your-supabase-url';
const SUPABASE_ANON_KEY = 'your-anon-key';
```

### Kit (ConvertKit) Integration
For welcome emails, update the Kit API credentials:
```javascript
const KIT_API_KEY = 'your-kit-api-key';
const KIT_FORM_ID = 'your-form-id';
```

### Google Analytics
The pages include GA4 tracking. Update the measurement ID:
```javascript
gtag('config', 'G-XXXXXXXXXX');
```

## Assets

### Required: Open Graph Image
Create `og-image.png` (1200x630px) for social media previews. See `assets/OG_IMAGE_SPECS.md` for design guidelines.

### Illustrations
The `assets/illustrations/` folder contains Satio character illustrations:
- Plant mascot in various poses
- Context-aware mood illustrations
- Meal and kitchen visuals

### Icons
SVG icons for features and widgets are in `assets/`:
- `icon-*.svg` — Feature icons (camera, food, mood, sleep, etc.)
- `ic_*.svg` — Widget icons for app mockups

## Colors Reference

| Color | Hex | Usage |
|-------|-----|-------|
| Primary (Indigo) | `#5B5FC7` | CTAs, accents |
| Secondary (Coral) | `#E8836B` | Highlights |
| Tertiary (Teal) | `#4ABBA8` | AI features |
| Background | `#FAFAF8` | Page background |
| Surface | `#F5F5F3` | Cards |
| Text Primary | `#2D2D2D` | Headlines |
| Text Secondary | `#6B6B6B` | Body text |

## Typography

- **Font:** Inter (loaded from Google Fonts)
- **Display:** 32px SemiBold
- **Headline:** 24px SemiBold
- **Body:** 16px Regular

## License

This waitlist page is for the Satio app. All rights reserved.
