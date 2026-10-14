# King of Tarts — extracted design rules

Source: computed styles on `https://kingoftarts.net/` (home page), measured at 1512px, 760px and 390px viewport widths.
Extracted 14 October 2026. These are the authority for the recipe archive and recipe single pages.

---

## 0. Critical findings

1. **No responsive type scaling.** h1 is 64px at 1512px, at 760px and at 390px. Same for every other text
   style. Only section padding changes. Any `clamp()` on type breaks the rule.
2. **Playball ships weight 400 only.** The site declares `font-weight: 700`, so every Playball heading is
   rendered with a browser-synthesised faux bold. To match, declare `700`.
3. **Body copy is Roboto 18px/25px — not Lora.** Lora is used only for navigation, footer menus,
   the header tagline and the search field.
4. Three buttons ("Discover the Story", "Join me", footer "Get the Recipes") have no per-element hover rule,
   so only the global `.elementor-button:hover{color:#fff}` applies — white text on a white button.
   Live-site bug; do not replicate.

---

## 1. Fonts

| Role | Family | Loaded weights |
|---|---|---|
| Display | `Playball, sans-serif` | 400 only (700 = synthetic) |
| Body / UI | `Roboto, sans-serif` | 400, 500, 600, 700 |
| Nav / chrome | `Lora, serif` | 400, 500, 700 |

---

## 2. Type scale (fixed at all breakpoints)

### Display — Playball
| Token | Size / line-height | Weight | Notes |
|---|---|---|---|
| `h1` hero | 64px / 75px | 700 | `text-transform: capitalize`, centred, `#FFFFFF` over image |
| `h2` section A | 50px / 50px | 700 | `#000000`, `text-align: start` |
| `h2` section B | 50px / 60px | 700 | `#000000`, centred |
| `h3` section | 45px / 45px | 700 | `#000000` |
| `h2` modal | 25px / 27.5px | 500 | `#1A1A1A`, margin `0 0 15px` |

### Headings — Roboto
| Token | Size / line-height | Weight | Notes |
|---|---|---|---|
| Card title | 22px / 32px | 600 | `#000000`, start-aligned |
| Icon-box title | 22px / 24.2px | 500 | centred, margin `0 0 15px` |

### Body — Roboto
| Token | Size / line-height | Weight | Notes |
|---|---|---|---|
| Paragraph (default) | 18px / 25px | 400 | `#000000`, margin `0 0 10px` |
| Paragraph (centred card) | 18px / 28px | 400 | centred, margin `0 0 10px` |
| Eyebrow / kicker | 18px / 18px | 700 | `letter-spacing: 1px`, `#9ECCBC`, centred |
| Inline link in body | 18px / 25px | 400 | `#EC9F2E`, no underline |

### Chrome — Lora
| Token | Size / line-height | Weight | Notes |
|---|---|---|---|
| Utility-nav link | 12px / 17.14px | 700 | `letter-spacing: 1px`, uppercase, `#000000` |
| Main-nav link | 14px / 20px | 700 | uppercase, `#000000`; `padding: 35px 40px` gives a 90px link box |
| Sub-menu item | 12px / 17.14px | 700 | `letter-spacing: 0.5px`, uppercase |
| Footer menu link | 14px / 25px | 400 | `padding-bottom: 4px` |
| Footer widget title | 16px / 19.2px | 500 | `#FFFFFF` |
| Header tagline | 16px / 25px | 400 | `#000000` — **Lora, not Playball** |
| Search field | 12px, italic | 400 | `#000000` |
| Footer copyright | 12px / 25px | 400 | `#FFFFFF` |

---

## 3. Buttons

All pill-shaped: `border-radius: 30px`, `transition: 0.3s`, `text-transform: none`, `letter-spacing: normal`.

### A. Primary filled — "Get the Recipes"
```
font: 500 20px/20px Roboto;
background:#9ECCBC; color:#FFFFFF; border:2px solid #9ECCBC;
padding:16px 30px; border-radius:30px;
:hover { background:#FFFFFF; color:#333333; }
```

### B. Ghost / outline — "Start Baking"
```
font: 500 20px/20px Roboto;
background:#FFFFFF; color:#333333; border:2px solid #9ECCBC;
padding:16px 30px; border-radius:30px;
:hover { background:#9ECCBC; color:#FFFFFF; }
```

### C. Card action — "View Recipes" (the 6 category cards)
```
font: 600 17px/17px Roboto;
background:#9ECCBC; color:#FFFFFF; border:1px solid #9ECCBC;
padding:15px 30px; border-radius:30px;
:hover { background:#FFFFFF; color:#333333; border-color:#9ECCBC; }
```

### D. Plain white — "Discover the Story", "Join me"
```
font: 500 20px/20px Roboto;
background:#FFFFFF; color:#333333; border:none;
padding:14px 28px; border-radius:30px;
:hover { /* broken on live site — use variant B's hover: background:#9ECCBC; color:#FFFFFF; */ }
```

### E. Form submit — "Subscribe" (Fluent Forms)
```
font: 500 16px/24px Lora;
background:#9ECCBC; color:#FFFFFF; border:1px solid #9ECCBC;
padding:8px 20px; border-radius:7px;
transition: background-color .15s ease-in-out, border-color .15s, box-shadow .15s;
:hover { background:#FFFFFF; border-color:#9ECCBC; color:#333333; }
```

**Note:** the only non-pill radius on the site is `7px`, on form submits only.

---

## 4. Colour

| Token | Value | Use |
|---|---|---|
| Mint | `#9ECCBC` | section backgrounds, button fills, eyebrow text, borders |
| Amber | `#EC9F2E` | inline links, accents |
| Cream | `#FFFDD0` | section backgrounds |
| Black | `#000000` | all body + heading text |
| Button text dark | `#333333` | button labels and hover text only |
| Dark surface | `#262626` | footer |
| White | `#FFFFFF` | page background, reversed text |

---

## 4b. Header band — the white fade

The logo band is **not a flat fill**. It is a white-to-transparent gradient laid over the doodle,
both sized `cover`. The doodle is washed out at the top and fully visible at the bottom.

```css
/* <header> */
background-color: transparent;
background-image:
  linear-gradient(rgb(255,255,255), rgba(219,219,219,0)),
  url("bg-logo-img-scaled.png");
background-size: cover, cover;
background-position: 50% 50%, 50% 50%;
background-repeat: repeat, repeat;
```

Doodle source image is **2560 × 909px**.

**The background sits on the whole `<header>`**, not on the logo strip alone. The menu strip inside it
paints solid white over the lower part, so the gradient never fully clears within the visible band.
Applying it to the logo strip alone makes the doodle read noticeably stronger — wrong.

| Strip | Height | Background |
|---|---|---|
| Utility bar (above `<header>`) | 43px | `#FFFFFF`, `border-bottom: .8px solid #EEEEEE` |
| `<header>` total (carries the background) | **294px** @1900 · 258px @760 · 245px @390 | gradient + doodle above |
| └ Logo + tagline | 200px @1900 · 206px @760 · 192px @390 | transparent |
| └ Main menu | 90px @1900 · 53px @760 | solid `#FFFFFF` |

**Logo:** rendered at **415 × 86px**, fixed from 760px up; `max-width: 100%` below that (350px @390).
Source `KOT-logo-landscape-RGB.png` is 970 × 200. Logo top offset inside the header: 40px @1900, 20px @760.

Page background is `#FFFFFF`.

## 4c. Archive page title band (live `/category/recipes/`)

| | Value |
|---|---|
| Band | `.container-fluid.container-page-item-title`, full-bleed, **156px**, background `#EEEEEE` |
| Eyebrow "CATEGORY" | Lora **12px / 25px**, 400, `letter-spacing: 3px`, uppercase, `#8F9294` |
| Title "RECIPES" | Playball **35px / 38.5px**, **500**, `letter-spacing: 4px`, **uppercase**, `#000000` |

Note this differs from the home page h1 (Playball 64/75, 700, capitalize). The archive has its own
title treatment. Which one the redesign uses is a decision, not a measurement.

## 5. Spacing

| Context | Desktop (>1024px) | Tablet / mobile (≤1024px) |
|---|---|---|
| Section outer | `padding: 90px 60px` | `padding: 64px 16px` |
| Section with bg colour | `padding: 0 60px` | `padding: 0 16px` |
| Inner container | `padding: 10px`, `gap: 20px` | same |

### Width (measured @1900 viewport / 1885 document)

| | Value |
|---|---|
| **Content measure** | **1140px**, centred |
| Theme chrome container | 1170px = 1140 + `padding: 0 15px` |
| Full-bleed section | full document width, `padding: 90px 60px` |
| Wide-section variant | 1250px inner (a few sections only) |
| Inner gap | 20px (30px on two-column rows) |
| Content left edge @1885 | 373px |

Backgrounds run edge to edge; the type and cards sit in the 1140px column with the 60px gutter outside it.
That is how "full width sections" and a readable measure coexist on this site, so the new pages follow it:

```css
:root { --content: 1140px; --gutter: 60px }   /* --gutter: 16px ≤1024px */
.band {
  width: 100%;
  max-width: calc(var(--content) + var(--gutter) * 2);
  margin-inline: auto;
  padding-inline: var(--gutter);
}
```

To go genuinely edge-to-edge instead, drop `max-width` and `margin-inline` from `.band` — one change.

---

## 6. Carried-over mistakes to fix in `recipe-archive.html`

- [ ] Body copy set in Lora 15px → must be **Roboto 18px/25px**
- [ ] Playball headings at weight 400 → must be **700**
- [ ] `clamp()` on h1/h2/h3 → must be **fixed px**
- [ ] Header tagline in Playball 21px → must be **Lora 16px/25px**
- [ ] Buttons: custom sizes/weights → must use variants A–E above
- [ ] Card titles in Playball → home page card titles are **Roboto 22px/32px, 600**
- [ ] Eyebrow colour/size → **Roboto 18px/18px, 700, 1px tracking, `#9ECCBC`**
