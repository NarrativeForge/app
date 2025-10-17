# NarrativeForge Design System

## Overview

NarrativeForge uses a bespoke design system inspired by Tron, Minority Report, and Liminal aesthetics. This document outlines the core principles, components, and usage guidelines.

---

## Design Principles

### 1. Layered Motion & Parallax
- **Layer 1**: Abstract circuitry background with slow drift (30s animation)
- **Layer 2**: Tron grid with pulsing and drifting effects (20s drift, 8s pulse)
- **Layer 3**: Gradient overlays for depth

### 2. Cinematic Easing
- All transitions use `cubic-bezier(.2,.8,.2,1)`
- Duration: 160-220ms for interactions, 400ms for page transitions
- No bouncy or tweeny effects

### 3. Glass Morphism
- Semi-transparent backgrounds with backdrop blur
- Subtle borders with neon glow effects
- Layered depth through shadows and overlays

---

## Design Tokens

Located in `/src/tokens.js`

### Colors

```javascript
colors = {
  bg0: "#070b10",        // Darkest background
  bg1: "#0b1620",        // Dark background
  bg2: "#0f1a28",        // Medium background
  cyan: "#36d2ff",       // Primary accent
  violet: "#a66bff",     // Secondary accent
  mint: "#6fffe3",       // Tertiary accent
  pink: "#ff6bb5",       // Accent variant
  orange: "#ff9f36",     // Accent variant
  textHi: "#ecf7ff",     // High contrast text
  textLo: "#a9bed1",     // Low contrast text
  textMuted: "#6b7f94",  // Muted text
}
```

### Fonts

```javascript
fonts = {
  display: "'Orbitron', sans-serif",  // Headers, titles
  body: "'Inter', sans-serif",        // Body text
}
```

### Motion

```javascript
motion = {
  easing: "cubic-bezier(.2,.8,.2,1)",
  durationFast: "160ms",
  durationMedium: "220ms",
  durationSlow: "400ms",
}
```

### Gradients

```javascript
gradients = {
  primary: "linear-gradient(135deg, cyan, violet)",
  secondary: "linear-gradient(135deg, mint, cyan)",
  accent: "linear-gradient(135deg, pink, orange)",
  background: "linear-gradient(180deg, bg0, bg1)",
}
```

---

## UI Components

All components are located in `/src/ui/`

### GlassButton

Pill-shaped buttons with gradient backgrounds and soft glow.

**Props:**
- `variant`: 'primary' | 'secondary' | 'accent'
- `size`: 'small' | 'medium' | 'large'
- `disabled`: boolean

**Usage:**
```jsx
import { GlassButton } from '../ui';

<GlassButton variant="primary" size="medium" onClick={handleClick}>
  Generate
</GlassButton>
```

### HoloCard

Semi-transparent cards with glass blur and pulsing neon borders.

**Props:**
- `glowColor`: string (hex color for glow effect)
- `className`: string

**Usage:**
```jsx
import { HoloCard } from '../ui';

<HoloCard glowColor={colors.cyan}>
  <p>Content goes here</p>
</HoloCard>
```

### TypeField

Input fields with cyan cursor and animated placeholders.

**Props:**
- `value`: string
- `onChange`: function
- `placeholder`: string
- `multiline`: boolean
- `rows`: number

**Usage:**
```jsx
import { TypeField } from '../ui';

<TypeField
  value={prompt}
  onChange={(e) => setPrompt(e.target.value)}
  placeholder="Describe a scene..."
  multiline={true}
  rows={4}
/>
```

### DockBar

Persistent bottom navigation with glass effect and reflection.

**Usage:**
```jsx
import { DockBar } from '../ui';

<DockBar />
```

### ModalPortal

Pop-up overlays with fade-in from 0.96 scale and glow rim.

**Props:**
- `isOpen`: boolean
- `onClose`: function
- `title`: string
- `children`: React.ReactNode

**Usage:**
```jsx
import { ModalPortal } from '../ui';

<ModalPortal isOpen={isOpen} onClose={handleClose} title="Settings">
  <p>Modal content</p>
</ModalPortal>
```

---

## Background System

### TronGridBackground

Located in `/src/components/TronGridBackground.jsx`

**Layers:**
1. Circuitry background (slow drift)
2. Tron grid (pulsing and drifting)
3. Gradient overlay

**Usage:**
```jsx
import TronGridBackground from './components/TronGridBackground';

<div className="min-h-screen relative">
  <TronGridBackground />
  {/* Your content */}
</div>
```

---

## Typography

### Display Text
- Font: Orbitron
- Use for: Headers, titles, brand elements
- Apply gradient: `linear-gradient(135deg, cyan, violet)`

### Body Text
- Font: Inter
- Use for: Paragraphs, descriptions, UI text
- Color: `textLo` or `textHi`

---

## Animation Guidelines

### Hover States
- Scale: 1.05
- Duration: 160ms
- Add glow effect

### Tap/Click States
- Scale: 0.95
- Duration: 160ms

### Page Transitions
- Fade in/out with scale (0.96 → 1)
- Duration: 220ms

### Background Animations
- Slow, continuous loops (20-30s)
- Subtle opacity changes (0.05 → 0.15)

---

## Best Practices

1. **No Template Components**: Avoid MUI, Bootstrap, or generic UI libraries
2. **Consistent Spacing**: Use 4px grid system (4, 8, 12, 16, 24, 32, 48, 64)
3. **Layered Depth**: Use z-index sparingly (0, 10, 20, 40, 50)
4. **Responsive Design**: Mobile-first approach with breakpoints at 640px, 768px, 1024px
5. **Accessibility**: Maintain WCAG AA contrast ratios, provide keyboard navigation

---

## File Structure

```
/src
  /ui
    GlassButton.jsx
    HoloCard.jsx
    TypeField.jsx
    DockBar.jsx
    ModalPortal.jsx
    index.js
  /components
    TronGridBackground.jsx
  /routes
    Home.jsx
    Clips.jsx
    ...
  tokens.js
  App.css
  App.jsx
```

---

## Future Enhancements

- [ ] Viral Clip Studio integration
- [ ] NightScreening Mode
- [ ] Forge Gallery
- [ ] Offline PWA capabilities
- [ ] Advanced motion effects (particle systems)
- [ ] Sound design integration

---

**Last Updated**: October 16, 2025
**Version**: 1.0.0

