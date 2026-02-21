# Satio Waitlist Page - Icons Reference

This document lists all the custom Satio icons used in the waitlist page (`index-v2.html`).

## Icons Used (Inline SVGs for Performance)

All icons are embedded as inline SVGs for optimal performance (no additional HTTP requests). They use the Satio brand colors.

---

### 1. Logo Icon
**Location:** Header, Footer
**Style:** Gradient background (#5B5FC7 to #4ABBA8), white "S" curve with smile
**Based on:** `logo_satio_icon_only.xml` design language

---

### 2. Intelligence Loop - Center Icon (Brain/Insights)
**Location:** Hero visual center
**Colors:** White on gradient background
**Purpose:** Represents AI-powered insights

---

### 3. Data Node Icons (8 nodes)

| Node | Icon | Color | Original Asset Inspiration |
|------|------|-------|---------------------------|
| **Food** | Plate/Bowl | #5B5FC7 (Primary) | Custom design |
| **Mood** | Smile face | #E8836B (Secondary) | Custom design |
| **Sleep** | Moon with Zzz | #4ABBA8 (Tertiary) | Custom design |
| **Health** | Heart with pulse | #E8836B (Secondary) | Custom design |
| **Triggers** | Lightning bolt | #E4B44C (Warning) | Custom design |
| **Exercise** | Dumbbell | #5AAD7A (Success) | `ic_widget_chart.xml` style |
| **Cycle** | Moon phases | #9B5FC7 (Custom purple) | Custom design |
| **Pantry** | Cabinet/Shelves | #5B5FC7 (Primary) | `illustration_pantry.xml` style |

---

### 4. Problem Section Icons

| Card | Icon | Style |
|------|------|-------|
| **Siloed Data** | Disconnected squares | Outlined, gray (#9B9B9B) |
| **Just Numbers** | Box with "2,100" | Outlined, gray (#9B9B9B) |
| **Satio Connects** | Eye with sparkles | Outlined, white |

---

### 5. Logging Method Icons

| Method | Icon | Source Inspiration |
|--------|------|-------------------|
| **Photo** | Camera | `ic_widget_camera.xml` (adapted) |
| **Voice** | Microphone | `ic_widget_microphone.xml` (adapted) |
| **Receipt** | Receipt with lines | Custom design |
| **Pantry** | Shelves with items | Custom design |

---

### 6. Unique Insights Icons

| Insight | Icon | Style |
|---------|------|-------|
| **Predict Cravings** | Crystal ball with arrows | White, gradient bg |
| **Break Patterns** | Shield with checkmark | White, gradient bg |
| **Optimize Energy** | Lightning bolt | White, gradient bg |
| **Adaptive Targets** | Target/bullseye | White, gradient bg |

---

## Brand Colors Used

| Color | Hex | Usage |
|-------|-----|-------|
| Primary (Warm Indigo) | `#5B5FC7` | Main CTAs, Food, Pantry icons |
| Secondary (Soft Coral) | `#E8836B` | Mood, Health icons |
| Tertiary (Soft Teal) | `#4ABBA8` | Sleep icon, gradients |
| Success (Green) | `#5AAD7A` | Exercise icon |
| Warning (Amber) | `#E4B44C` | Triggers icon |
| Cycle Purple | `#9B5FC7` | Cycle icon |
| Gray | `#9B9B9B` | Inactive/problem icons |

---

## Original Android Assets Referenced

These drawable assets were used as inspiration for the web icons:

1. `ic_widget_camera.xml` - Camera icon design
2. `ic_widget_microphone.xml` - Microphone icon design
3. `ic_widget_chart.xml` - Chart/data visualization style
4. `ic_widget_search.xml` - Search icon style
5. `logo_satio_icon_only.xml` - Logo "S" curve design
6. `illustration_pantry.xml` - Pantry visual style
7. `illustration_visual_data.xml` - Data visualization style

---

## Files to Copy to Web Assets (if needed separately)

If you want to use these icons as separate files, create:
- `waitlist/assets/logo.svg`
- `waitlist/assets/icon-food.svg`
- `waitlist/assets/icon-mood.svg`
- `waitlist/assets/icon-sleep.svg`
- `waitlist/assets/icon-health.svg`
- `waitlist/assets/icon-triggers.svg`
- `waitlist/assets/icon-exercise.svg`
- `waitlist/assets/icon-cycle.svg`
- `waitlist/assets/icon-pantry.svg`
- `waitlist/assets/icon-camera.svg`
- `waitlist/assets/icon-microphone.svg`
- `waitlist/assets/icon-receipt.svg`

Currently all icons are inline in `index-v2.html` for optimal performance.

---

*Last updated: February 2026*
