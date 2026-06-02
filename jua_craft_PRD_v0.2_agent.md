# JUA Craft — Product Requirements Document
**Version:** 0.2  
**Status:** In Progress  
**Brand:** JUA Craft · Nairobi, Kenya  
**Contact:** jua.nairobi@gmail.com  
**Last Updated:** June 2026

---

## Overview

JUA Craft is a Kenyan handcraft brand's online showcase platform. The creator photographs products at markets or studios; after processing, items appear on a timeline canvas. Users browse like flipping through a book or wandering a market stall.

**Tagline:** *在非洲淘到的漂亮东西* ("Beautiful things found in Africa")  
**Core philosophy:** Less is more. The product is the protagonist. Whitespace is design.

---

## Tech Stack

### Current (Prototype)
- Single-file HTML + CSS + Vanilla JS
- No framework, no dependencies
- Deliverable: `.html` file openable directly in browser

### Phase 1 (Planned, not yet implemented)
- **Airtable** — product database (no, material, price, stock, image URL)
- **Framer or raw HTML** — frontend display
- **Make (Integromat)** — automation pipeline
- **Photoroom** — background removal (mobile app)
- **GitHub** — version control (`jua-craft` repository)

---

## Users

### Creator (Admin)
- Shoots products on mobile at markets or studio
- Mobile-first workflow; no desktop required
- High aesthetic standards — no AI-generated-looking output
- Product categories: earrings, camel bone carvings, illustrations, banana fiber, porcupine quill, peacock feather, wood carving, Maasai beads, cow horn

### Viewers (End Users)
- Private community users from Xiaohongshu (RED)
- Access via shared link — **zero download, zero login required**
- Browse, heart items, comment after liking
- Purchase intent handled externally via Xiaohongshu DM

---

## Design System

### Color Palette
```
Canvas background:  #A86E38  (terracotta orange)
Card surface:       rgba(244, 232, 208, 0.93)  (cream paper)
Dark overlay:       #1a1208
Text primary:       rgba(255, 255, 255, 0.88)
Text secondary:     rgba(255, 255, 255, 0.48)
Text dim:           rgba(255, 255, 255, 0.22)
Gold accent:        rgba(255, 210, 105, 0.88)
Heart red:          #b82828
```

### Typography
```
Serif (product names, brand):  Crimson Text, italic
System UI (labels, metadata):  -apple-system, Helvetica Neue
```

### Card Styling
```css
background: rgba(244, 232, 208, 0.93);
border-radius: 3px;
box-shadow:
  1px 2px 0px rgba(255,255,255,0.18) inset,
  2px 3px 6px rgba(20,8,0,0.18),
  4px 7px 18px rgba(20,8,0,0.22),
  8px 14px 32px rgba(20,8,0,0.14);
```

### Background Texture
```css
background:
  radial-gradient(ellipse at 12% 15%, rgba(200,140,60,0.35) 0%, transparent 45%),
  radial-gradient(ellipse at 88% 80%, rgba(55,25,5,0.3) 0%, transparent 42%),
  repeating-linear-gradient(0deg, transparent, transparent 2px, rgba(0,0,0,0.018) 2px, rgba(0,0,0,0.018) 3px),
  repeating-linear-gradient(90deg, transparent, transparent 6px, rgba(0,0,0,0.01) 6px, rgba(0,0,0,0.01) 7px);
```

---

## Layout & Responsiveness

The timeline is **always centered** on all screen sizes. No sidebar layout.

```
Mobile   (< 600px):  max-width: 480px  | card size: ~86px  | detail: bottom sheet
Tablet   (600-900px): max-width: 600px  | card size: ~110px | detail: bottom sheet centered
Desktop  (≥ 900px):  max-width: 780px  | card size: ~140px | detail: centered modal
```

Topbar is always horizontal at the top. Never split into a sidebar — doing so breaks the centered timeline composition.

---

## Core Features (Confirmed)

### 1. Scatter Canvas (CONFIRMED ✅)
Product cards are scattered directly on the canvas on both sides of the timeline.

**Rules:**
- Each card is visible immediately — no grouping, no folding
- Card dimensions vary per product (not uniform squares)
- Position has random vertical offset: `rand(-18px, 18px)`
- Horizontal gap from timeline center: `rand(14px, 48px)`
- Each card has a unique rotation angle (stored per item, not regenerated)
- Thin connector line from card to timeline center dot

**Rejected alternative:** Folded pile mode (required 3 taps to see a product — too many steps) ❌

### 2. One-Tap User Flow (CONFIRMED ✅)
```
See card → tap → detail sheet opens
```
No intermediate screens. Maximum 2 taps for sold items (flip → detail).

### 3. Timeline Structure (CONFIRMED ✅)
- Vertical center line, 0.5px, gradient fade at top and bottom
- Month markers: small dot + label pill, centered on the line
- Items alternate left/right per month group
- Timeline dot + connector line for each card

```
Month marker:
  dot: 7px circle, rgba(255,255,255,0.55)
  label: 7.5px, letter-spacing 0.22em, pill background rgba(120,72,24,0.52)
```

### 4. Sold Item Behavior (CONFIRMED ✅)
- Sold cards are flipped to back face by default
- Back face shows: brand name "JUA" + archive number "#001" + "archived"
- Filter: `saturate(0.1) brightness(0.65)` (greyed out)
- On tap: flip to front face (weighted flip animation) → open detail sheet
- Sold items are NOT removed — they preserve the sense of history

**Flip animation:**
```css
transition: transform 0.78s cubic-bezier(0.38, 0, 0.12, 1);
/* Fast start, resistance at mid-point, slow finish — feels like a thick card */
```

### 5. Hover Interaction (CONFIRMED ✅)
```css
/* On mouseenter */
transform: rotate({reduced_angle}deg) translateY(-12px) scale(1.1);
filter: drop-shadow(0 12px 28px rgba(10,4,0,0.55));
z-index: 30;
transition: 0.45s cubic-bezier(.22,1,.36,1);

/* On mouseleave */
transform: rotate({original_angle}deg);
/* Restore filter and z-index */
```

### 6. Entrance Animation (CONFIRMED ✅)
- Cards slide in from their respective side (left items from left, right items from right)
- Stagger delay: 100ms between each card
- Month markers fade in first
- Uses `IntersectionObserver` — elements animate only when scrolled into view

```css
/* Initial state */
opacity: 0;
transform: rotate({angle}deg) translateX(±24px);

/* Animated state */
transition: transform 0.58s cubic-bezier(.22,1,.36,1) {delay}ms,
            opacity 0.5s ease {delay}ms;
opacity: 1;
transform: rotate({angle}deg); /* translateX removed */
```

### 7. Heart / Like (CONFIRMED ✅)
- ♡ → ♥ on tap, count increments by 1
- Stored in local JS object (not persisted to server in Phase 0)
- Liked state: `color: #b82828`
- No "dislike" button — users simply scroll past

---

## Detail Sheet

Slides up from bottom on mobile/tablet. Centered modal on desktop.

```
Content:
  - Product image (SVG or PNG with drop-shadow)
  - Item number + material (uppercase, dim)
  - Product name (Crimson Text, 22px)
  - Material detail (10px, dim)
  - Price (Crimson Text, 22px, gold)
  - Stock status (8px, dim)
  - Heart button + count

Close: tap backdrop
```

---

## Data Model

Each product item:
```typescript
interface Item {
  id: string;          // e.g. 'i1'
  no: string;          // e.g. '001'
  name: string;        // e.g. '大象 · 骆驼骨项链'
  mat: string;         // e.g. '骆驼骨 · 木珠'
  price: string;       // e.g. '¥220'
  stock: string;       // e.g. '剩 1 件' or '已售'
  likes: number;       // base like count
  sold: boolean;       // flips card to back if true
  svg: string;         // inline SVG string (replace with img src in production)
  side: 'left' | 'right';
  w: number;           // card width in px
  h: number;           // card height in px
  rot: number;         // rotation in degrees (fixed per item, e.g. -8)
}
```

Monthly group:
```typescript
interface MonthGroup {
  month: string;   // e.g. 'Nov 2025'
  items: Item[];
}
```

---

## Reserved Fields (Phase 1, not shown in UI yet)
```
contact_url    string   // Xiaohongshu profile link
is_purchasable boolean  // toggle to enable buy flow
purchase_url   string   // external link
comments       array    // enabled after user likes
```

---

## Creator Workflow

```
1. Shoot product photo on mobile
2. Remove background in Photoroom app (preserve real texture + clean outline)
3. Review cutout — approve or reshoot
4. Fill in: material, price, stock (number auto-assigned)
5. Publish → card appears on timeline canvas
```

Edge cases for background removal:
- Earrings with cutouts → high complexity
- Woven/braided edges → use Photoroom's refine edge tool
- Illustrated paper → watch for edge blur

---

## Out of Scope (Phase 1)

The following will NOT be built:
- [ ] Purchase / payment flow
- [ ] User registration / login
- [ ] Search or filter UI
- [ ] Folded pile card grouping (rejected)
- [ ] Timeline diary feed layout (paused)
- [ ] Ads or recommendation algorithm
- [ ] App download / native app

---

## Next Actions

- [ ] Remove background from first 3–5 real product photos using Photoroom
- [ ] Send PNG cutouts → replace SVG placeholders in HTML
- [ ] Create GitHub repo `jua-craft`, commit current HTML version
- [ ] Share link with 3–5 Xiaohongshu community users for feedback
- [ ] Based on feedback: decide whether to proceed to Phase 1 (Airtable + Framer)

---

## Version History

| Version | Date | Summary |
|---------|------|---------|
| v0.1 | 2026-06 | Initial PRD. Product direction, users, MVP roadmap. |
| v0.2 | 2026-06 | Confirmed visual prototype, all interaction patterns, responsive layout, design system. |

---

*This document is maintained collaboratively between the creator and Claude. Update on every significant design or scope decision.*
