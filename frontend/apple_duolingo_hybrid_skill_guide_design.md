# SKILL SPECIFICATION: Apple-Duolingo Hybrid Design System

## Overview & Visual Philosophy
This design system pairs **Apple-like minimalism, whitespace, and typographic discipline** with **Duolingo’s signature tactile interactivity and vibrant green branding**.

- **Atmosphere**: Clean, premium, accessible, and energetic. Professional enough for modern digital products and SaaS, friendly enough for gamified consumer experiences.
- **Core Contrast Rule**: Never use pure green text directly on white backgrounds (insufficient contrast ratio). Green is reserved for interactive accents, indicators, active states, and tactile buttons.
- **Strict Button Constraint**: All primary buttons must strictly use the Duolingo brand green with a tactile 3D bottom border lip. No competing button colors (e.g. blue/orange) for primary actions.

---

## 1. Design Tokens & Variables

```css
:root {
  /* Brand & Primary Actions */
  --primary: #58CC02;
  --primary-hover: #61E002;
  --primary-dark: #4FBB02;       /* Tactile 3D bottom border */
  --primary-active: #46A301;
  --primary-soft: #E8F8DE;       /* Active pill / highlight tint */

  /* Neutral Backgrounds & Surfaces (Apple-inspired) */
  --background: #FFFFFF;
  --background-secondary: #F5F5F7;
  --surface: #FFFFFF;
  --surface-muted: #F7F7F7;
  --dark-surface: #161617;       /* Apple-style deep obsidian container */

  /* Typography & Text */
  --text-primary: #1D1D1F;       /* Headings & key copy */
  --text-secondary: #3C3C3C;     /* Body & descriptions */
  --text-muted: #777777;         /* Metadata & captions */
  --text-inverse: #FFFFFF;       /* Copy on dark surface or primary green */

  /* Borders & Dividers */
  --border: #D2D2D7;
  --border-light: #E8E8EA;

  /* Semantic Feedback */
  --success: #2E9D50;
  --warning: #FF9600;
  --error: #DE4545;

  /* Typography Scale (Inter Font Family) */
  --font-family: 'Inter', -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, sans-serif;
  --font-display: 56px;
  --font-h1: 44px;
  --font-h2: 32px;
  --font-h3: 24px;
  --font-h4: 20px;
  --font-body: 16px;
  --font-small: 14px;
  --font-caption: 12px;

  /* 4px Spacing System */
  --space-xs: 4px;
  --space-sm: 8px;
  --space-md: 12px;
  --space-base: 16px;
  --space-lg: 24px;
  --space-xl: 32px;
  --space-2xl: 48px;
  --space-3xl: 64px;
  --space-4xl: 80px;

  /* Border Radii */
  --radius-xs: 6px;
  --radius-sm: 8px;
  --radius-md: 12px;
  --radius-lg: 16px;
  --radius-xl: 20px;
  --radius-pill: 9999px;

  /* Shadows & Elevation */
  --shadow-flat: none;
  --shadow-card: 0 2px 8px rgba(0, 0, 0, 0.05);
  --shadow-card-hover: 0 8px 20px rgba(0, 0, 0, 0.08);
  --shadow-floating-dock: 0 12px 36px rgba(0, 0, 0, 0.12), 0 4px 12px rgba(0, 0, 0, 0.05);

  /* Motion Timing */
  --transition-fast: 150ms cubic-bezier(0.25, 1, 0.5, 1);
  --transition-base: 240ms cubic-bezier(0.25, 1, 0.5, 1);
}
```

---

## 2. Core UI Components

### 2.1 Tactile Duolingo-Inspired Buttons

The signature button features bold uppercase typography, a 12px border radius, and a 4px darker green bottom border that compresses into a 2px offset when pressed.

```css
/* Tactile Primary Button */
.btn-duo-primary {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  gap: 8px;
  background-color: var(--primary);
  color: #FFFFFF;
  font-family: var(--font-family);
  font-size: 15px;
  font-weight: 700;
  text-transform: uppercase;
  letter-spacing: 0.02em;
  padding: 12px 24px;
  border-radius: var(--radius-md);
  border: none;
  border-bottom: 4px solid var(--primary-dark);
  cursor: pointer;
  transition: filter var(--transition-fast), transform var(--transition-fast);
}

.btn-duo-primary:hover {
  filter: brightness(1.06);
}

.btn-duo-primary:active {
  transform: translateY(2px);
  border-bottom-width: 2px;
  background-color: var(--primary-active);
}

/* Secondary Button (Ghost Outline with Tint) */
.btn-duo-secondary {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  gap: 8px;
  background-color: transparent;
  color: var(--primary-dark);
  font-family: var(--font-family);
  font-size: 15px;
  font-weight: 700;
  text-transform: uppercase;
  letter-spacing: 0.02em;
  padding: 12px 24px;
  border-radius: var(--radius-md);
  border: 2px solid var(--primary-dark);
  cursor: pointer;
  transition: background-color var(--transition-fast), color var(--transition-fast);
}

.btn-duo-secondary:hover {
  background-color: rgba(88, 204, 2, 0.08);
}
```

---

### 2.2 Floating Pill Bottom Navigation Dock

Floating dock anchored to the bottom center of the viewport, providing a clean Apple-style blur with Duolingo-styled active indicators.

```html
<nav class="floating-nav-dock" aria-label="Main Navigation">
  <a href="#home" class="nav-item active">
    <svg class="nav-icon" ...></svg>
    <span class="nav-label">Home</span>
  </a>
  <a href="#explore" class="nav-item">
    <svg class="nav-icon" ...></svg>
    <span class="nav-label">Explore</span>
  </a>
  <a href="#activity" class="nav-item">
    <svg class="nav-icon" ...></svg>
    <span class="nav-label">Activity</span>
  </a>
  <a href="#profile" class="nav-item">
    <svg class="nav-icon" ...></svg>
    <span class="nav-label">Profile</span>
  </a>
</nav>
```

```css
.floating-nav-dock {
  position: fixed;
  bottom: 24px;
  left: 50%;
  transform: translateX(-50%);
  z-index: 50;
  display: flex;
  align-items: center;
  gap: 8px;
  padding: 6px 12px;
  background-color: rgba(255, 255, 255, 0.95);
  backdrop-filter: blur(16px);
  -webkit-backdrop-filter: blur(16px);
  border: 1px solid var(--border-light);
  border-radius: var(--radius-pill);
  box-shadow: var(--shadow-floating-dock);
}

.floating-nav-dock .nav-item {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  min-width: 72px;
  padding: 8px 16px;
  border-radius: var(--radius-pill);
  color: var(--text-muted);
  text-decoration: none;
  font-size: 13px;
  font-weight: 600;
  transition: all var(--transition-fast);
}

.floating-nav-dock .nav-item.active {
  background-color: var(--primary-soft);
  color: #2F7502;
}

.floating-nav-dock .nav-item:hover:not(.active) {
  color: var(--text-primary);
  background-color: rgba(0, 0, 0, 0.03);
}
```

---

### 2.3 Apple-Inspired Clean Cards

Cards prioritize clean lines, generous padding, subtle elevation, and light hover feedback.

```css
.card {
  background-color: var(--surface);
  border: 1px solid var(--border-light);
  border-radius: var(--radius-md);
  padding: 24px;
  box-shadow: var(--shadow-card);
  transition: transform var(--transition-base), box-shadow var(--transition-base);
}

.card:hover {
  transform: translateY(-2px);
  box-shadow: var(--shadow-card-hover);
}
```

---

### 2.4 Dark Contrast Surface Container (VIP / Vault Section)

Used for contrast sections or premium rewards (e.g. VIP Vault).

```css
.dark-vault-section {
  background-color: var(--dark-surface);
  border-radius: var(--radius-xl);
  color: #FFFFFF;
  padding: 48px;
  border: 1px solid rgba(255, 255, 255, 0.08);
}
```

---

## 3. Implementation Rules for Skill Prompting

1. **Button Uniformity**:
   - Always use `.btn-duo-primary` for action buttons.
   - Do NOT use alternative colored buttons (e.g., blue, red, gold) for primary actions. Everything resolves to Duolingo green.
2. **Bottom Offset**:
   - When using the floating bottom dock, ensure pages contain `padding-bottom: 96px` (or `pb-24`) to ensure content is never obscured.
3. **No Low-Contrast Green Text**:
   - Never render `#58CC02` as body copy on pure white backgrounds. Use `#1D1D1F` or `#2F7502` for text-on-tint elements.
4. **Elevation**:
   - Keep surfaces flat and crisp, relying on 1px subtle borders (`#E8E8EA`) and gentle shadows rather than heavy drop shadows.
