---
name: create-pixel-art
description: Use this skill when the user asks to "create a pixel icon", "make a pixel art SVG", "design a pixel canvas", "create a flow chart in pixel art style", "add a pixel art diagram", "make an architecture diagram", "create an animated SVG", or anything related to building pixel art visuals, icons, or animated canvases for OmniQuery. Produces SVG files that match OmniQuery's dark pixel art brand identity.
---

# Create OmniQuery Pixel Art

Produce SVG pixel art icons, canvases, flow diagrams, and animated visuals that match OmniQuery's dark, terminal-aesthetic brand identity.

## Brand Guidelines

### Color Palette

| Role | Hex | Usage |
|------|-----|-------|
| **Primary (Cyan)** | `#06b6d4` | Borders, outlines, data flow lines, active states, connector paths |
| **Secondary (Purple)** | `#8b5cf6` | AI/LLM layer, query headers, accent elements, inner details |
| **Accent (Amber)** | `#f59e0b` | Cursors, live indicators, blinking dots, highlighted cells |
| **Success (Green)** | `#4ade80` | Active/connected status, success states, MongoDB icon |
| **Warning (Orange)** | `#f97316` | MySQL icon, caution states |
| **Info (Blue)** | `#60a5fa` | PostgreSQL icon, informational |
| **Violet (Indigo)** | `#818cf8` | Teams/UI icons, dashboard elements |
| **Sky Blue** | `#38bdf8` | Jira, secondary connectors |
| **Pink** | `#e879f9` | Slack, notifications |
| **Background Dark** | `#030712` | Page/canvas background |
| **Card Dark** | `#060c18` | Icon backgrounds, card fills |
| **Card Mid** | `#080f1e` | Hover card fills |
| **Border** | `rgba(255,255,255,0.08)` | Subtle card borders |

### Design Principles
- **Pixel-crisp**: Always use `shape-rendering="crispEdges"` on all rects
- **Dark-first**: Dark backgrounds (`#060c18`), light pixel elements
- **Monospace terminal aesthetic**: Icons look like they belong in a terminal
- **Pixel corners**: Use small corner accent squares (2–4px) instead of rounded borders
- **No gradients inside icons**: Solid pixel fills only; gradients only for glow effects

---

## Part 1 — Pixel Icons (8×8 Grid)

An 8×8 pixel icon is a 64-element array where `1` = filled pixel, `0` = empty.

### SVG Structure for an 8×8 Icon

```svg
<svg width="32" height="32" viewBox="0 0 32 32" xmlns="http://www.w3.org/2000/svg">
  <!-- Optional: dark background -->
  <rect width="32" height="32" fill="#060c18"/>
  <!-- Pixel grid: each cell is 3px with 1px gap -->
  <g>
    <!-- Row 0 -->
    <rect x="1"  y="1"  width="3" height="3" fill="#06b6d4" shape-rendering="crispEdges"/>
    <!-- ... more rects ... -->
  </g>
</svg>
```

### Cell Size Formula

For an N×N icon in a W×W canvas:
```
padding  = W * 0.03   (e.g. 32px canvas → ~1px padding)
cell     = (W - 2*padding) / N
gap      = 1px
x_i      = padding + i * (cell + gap)
y_j      = padding + j * (cell + gap)
```

Standard sizes:
| Canvas | Grid | Cell | Gap | Padding |
|--------|------|------|-----|---------|
| 32×32  | 8×8  | 3px  | 1px | 1px     |
| 48×48  | 8×8  | 5px  | 1px | 1.5px   |
| 180×180| 8×8  | 13.83px | gap implicit | 25px |
| 512×512| 8×8  | 40.43px | gap implicit | 66px |

### Existing Icon Pixel Maps

Use these as references or combine/modify for new icons.

**Database (cylinder top view) — generic DB:**
```
0,0,1,1,1,1,0,0
0,1,1,1,1,1,1,0
1,1,0,0,0,0,1,1
1,1,1,1,1,1,1,1
1,1,1,1,1,1,1,1
1,1,0,0,0,0,1,1
0,1,1,1,1,1,1,0
0,0,1,1,1,1,0,0
```
Color: `#60a5fa` (PostgreSQL blue)

**T-shape (Trino / query engine):**
```
1,1,1,1,1,1,1,1
0,0,0,1,1,0,0,0
0,0,0,1,1,0,0,0
0,0,0,1,1,0,0,0
0,0,0,1,1,0,0,0  (mid row adds horizontal bar)
0,0,1,1,1,1,0,0
0,1,1,0,0,1,1,0
1,1,0,0,0,0,1,1
```
Color: `#06b6d4`

**Leaf (MongoDB):**
```
0,0,0,1,1,0,0,0
0,0,1,1,1,1,0,0
0,1,1,1,1,1,1,0
0,1,1,1,1,1,1,0
0,0,1,1,1,1,0,0
0,0,0,1,1,0,0,0
0,0,0,1,1,0,0,0
0,0,0,0,1,0,0,0
```
Color: `#4ade80`

**S-curve (S3/storage):**
```
0,1,1,1,1,1,1,0
1,1,0,0,0,0,1,1
1,1,1,1,1,1,1,0
0,1,1,1,1,1,1,1
0,0,0,0,0,0,1,1
1,0,0,0,0,0,1,1
1,1,0,0,0,1,1,0
0,1,1,1,1,1,0,0
```
Color: `#fbbf24`

**Terminal cursor (OmniQuery logo inner):**
```
0,1,1,1,1,1,0,0   ← purple header bar
0,1,0,0,0,0,0,0
0,1,1,1,0,0,0,0   ← cyan data row 1
0,1,1,0,0,0,0,0   ← cyan data row 2
0,1,0,1,0,0,0,0   ← amber cursor pixel
0,0,0,0,0,0,0,0
0,0,0,0,0,0,0,0
0,0,0,0,0,0,0,0
```
Colors: header=`#8b5cf6`, rows=`#06b6d4`, cursor=`#f59e0b`

**Bar chart (analytics):**
```
0,0,0,0,0,0,1,0
0,0,0,0,0,1,1,0
0,0,0,1,0,1,1,0
0,0,0,1,0,1,1,0
0,1,0,1,0,1,1,0
0,1,0,1,1,1,1,0
0,1,1,1,1,1,1,0
1,1,1,1,1,1,1,1
```
Color: `#06b6d4`

**Window/iFrame (two nested frames):**
```
1,1,1,1,1,1,1,1
1,0,0,0,0,0,0,1
1,0,1,1,1,1,0,1
1,0,1,0,0,1,0,1
1,0,1,0,0,1,0,1
1,0,1,1,1,1,0,1
1,0,0,0,0,0,0,1
1,1,1,1,1,1,1,1
```
Color: `#22d3ee`

**Brain/neural (LLM):**
```
0,1,1,0,0,1,1,0
1,1,1,1,1,1,1,1
1,0,1,1,1,1,0,1
1,1,1,1,1,1,1,1
0,1,1,1,1,1,1,0
0,1,0,1,1,0,1,0
0,0,1,0,0,1,0,0
0,0,0,1,1,0,0,0
```
Color: `#8b5cf6`

### How to Render a Pixel Map in SVG

Given a flat 64-element array and canvas size W:
```
for j in 0..7:
  for i in 0..7:
    if pixels[j*8 + i] == 1:
      emit <rect x="{padding + i*(cell+gap)}" y="{padding + j*(cell+gap)}"
                width="{cell}" height="{cell}" fill="{color}"
                shape-rendering="crispEdges"/>
```

---

## Part 2 — Pixel Canvas (Larger Diagrams)

A pixel canvas is a full SVG scene: cards, connectors, hubs, and animations.

### Canvas Template

```svg
<svg width="960" height="540" viewBox="0 0 960 540"
     xmlns="http://www.w3.org/2000/svg">

  <!-- Optional glow filter -->
  <defs>
    <filter id="glow" x="-20%" y="-20%" width="140%" height="140%">
      <feGaussianBlur in="SourceGraphic" stdDeviation="4" result="blur"/>
      <feMerge><feMergeNode in="blur"/><feMergeNode in="SourceGraphic"/></feMerge>
    </filter>
  </defs>

  <!-- Background -->
  <rect width="960" height="540" fill="#030712"/>

  <!-- Pixel grid texture (optional) -->
  <defs>
    <pattern id="grid" width="24" height="24" patternUnits="userSpaceOnUse">
      <path d="M 24 0 L 0 0 0 24" fill="none"
            stroke="rgba(6,182,212,0.04)" stroke-width="0.5"/>
    </pattern>
  </defs>
  <rect width="960" height="540" fill="url(#grid)"/>

  <!-- Cards, connectors, hub go here -->

</svg>
```

### Pixel Card Component

A card is a dark rectangle with:
- Dark background fill
- Cyan or coloured border (1px)
- Small corner accent squares (pixel art style)
- An 8×8 pixel icon
- Monospace label text

```svg
<!-- Card at (x=50, y=200), size 120×80 -->
<g transform="translate(50, 200)">
  <!-- Background -->
  <rect width="120" height="80" fill="#060c18" stroke="#06b6d4"
        stroke-width="1" stroke-opacity="0.5" shape-rendering="crispEdges"/>
  <!-- Corner accents (pixel style) -->
  <rect x="0" y="0" width="4" height="4" fill="#06b6d4" shape-rendering="crispEdges"/>
  <rect x="116" y="0" width="4" height="4" fill="#06b6d4" shape-rendering="crispEdges"/>
  <rect x="0" y="76" width="4" height="4" fill="#06b6d4" shape-rendering="crispEdges"/>
  <rect x="116" y="76" width="4" height="4" fill="#06b6d4" shape-rendering="crispEdges"/>
  <!-- Scanline texture (optional) -->
  <rect width="120" height="80"
        fill="url(#scanlines)" opacity="0.04" shape-rendering="crispEdges"/>
  <!-- Pixel icon (centered, 32×32) -->
  <g transform="translate(44, 12)">
    <!-- 8×8 pixel icon rects go here -->
  </g>
  <!-- Label -->
  <text x="60" y="62" text-anchor="middle"
        font-family="'Courier New', monospace" font-size="9"
        fill="#94a3b8" letter-spacing="1">POSTGRES</text>
  <!-- Status dot -->
  <circle cx="110" cy="10" r="3" fill="#4ade80">
    <animate attributeName="opacity" values="1;0.3;1" dur="2s"
             repeatCount="indefinite"/>
  </circle>
</g>
```

### Center Hub Component

The octagonal hub uses a `<polygon>` with 8 computed points:

```svg
<!-- Hub centered at (480, 270), size ~80px -->
<g transform="translate(480, 270)">
  <!-- Rotating dashed ring -->
  <circle cx="0" cy="0" r="52" fill="none"
          stroke="#06b6d4" stroke-width="1"
          stroke-dasharray="6 4" stroke-opacity="0.4">
    <animateTransform attributeName="transform" type="rotate"
                      from="0" to="360" dur="12s" repeatCount="indefinite"/>
  </circle>
  <!-- Octagon border: cut corners at 45°, size 40 -->
  <!-- Points: (x1,y0)(x2,y0)(x3,y1)(x3,y2)(x2,y3)(x1,y3)(x0,y2)(x0,y1) -->
  <polygon
    points="-14,-40 14,-40 40,-14 40,14 14,40 -14,40 -40,14 -40,-14"
    fill="#060c18" stroke="#06b6d4" stroke-width="1.5"
    shape-rendering="crispEdges"/>
  <!-- OmniQuery pixel icon (centered 32×32) -->
  <!-- Place icon rects here with transform="translate(-16,-16)" -->
  <!-- Pulse dot -->
  <circle cx="0" cy="0" r="3" fill="#06b6d4">
    <animate attributeName="r" values="3;6;3" dur="2s" repeatCount="indefinite"/>
    <animate attributeName="opacity" values="1;0;1" dur="2s" repeatCount="indefinite"/>
  </circle>
</g>
```

### Connector Paths

Connectors go from card edge to hub. Use cubic bezier curves:

```svg
<!-- Left card (right edge at x=170) to Hub (left edge at x=440) -->
<path d="M 170,240 C 305,240 305,270 440,270"
      fill="none" stroke="#06b6d4" stroke-width="1.5"
      stroke-opacity="0.35" stroke-dasharray="4 3"
      shape-rendering="crispEdges">
  <!-- Dash shimmer animation -->
  <animate attributeName="stroke-dashoffset"
           values="0;-14" dur="1.2s" repeatCount="indefinite"/>
</path>
```

### Animated Flow Dots on Connectors

Dots move along the connector path using `<animateMotion>`:

```svg
<!-- Dot flowing LEFT → HUB (forward direction) -->
<circle r="3" fill="#06b6d4" filter="url(#glow)">
  <animateMotion
    path="M 170,240 C 305,240 305,270 440,270"
    dur="1.8s" repeatCount="indefinite"
    calcMode="spline"
    keySplines="0.4 0 0.6 1"/>
</circle>

<!-- Dot flowing HUB → RIGHT (path drawn right-to-left, use keyPoints="1;0") -->
<circle r="3" fill="#8b5cf6" filter="url(#glow)">
  <animateMotion
    path="M 790,270 C 655,270 655,240 520,240"
    dur="1.8s" repeatCount="indefinite"
    keyPoints="1;0" keyTimes="0;1"
    calcMode="spline"
    keySplines="0.4 0 0.6 1"/>
</circle>
```

> **Key rule**: If your path is drawn right-to-left but the dot should move left-to-right (hub → right card), add `keyPoints="1;0" keyTimes="0;1"` to reverse motion direction without redrawing the path.

### Section Labels / Headers

```svg
<!-- Section divider label -->
<rect x="50" y="20" width="160" height="18" fill="#06b6d4" fill-opacity="0.08"
      stroke="#06b6d4" stroke-width="0.5" shape-rendering="crispEdges"/>
<text x="130" y="32" text-anchor="middle"
      font-family="'Courier New', monospace" font-size="9"
      fill="#06b6d4" letter-spacing="2">DATA SOURCES</text>
```

---

## Part 3 — Animation Patterns

### Pulsing dot (status indicator)
```svg
<circle cx="10" cy="10" r="3" fill="#4ade80">
  <animate attributeName="opacity" values="1;0.3;1" dur="2s" repeatCount="indefinite"/>
</circle>
```

### Blinking pixel (cursor)
```svg
<rect x="20" y="20" width="4" height="4" fill="#f59e0b" shape-rendering="crispEdges">
  <animate attributeName="opacity" values="1;0;1" dur="1s" repeatCount="indefinite"/>
</rect>
```

### Rotating ring
```svg
<circle cx="0" cy="0" r="40" fill="none" stroke="#06b6d4"
        stroke-width="1" stroke-dasharray="8 4" stroke-opacity="0.5">
  <animateTransform attributeName="transform" type="rotate"
                    from="0" to="360" dur="10s" repeatCount="indefinite"/>
</circle>
```

### Path shimmer (connector animation)
```svg
<path d="M 0,0 L 200,0" stroke="#06b6d4" stroke-dasharray="6 4">
  <animate attributeName="stroke-dashoffset" values="0;-20"
           dur="1s" repeatCount="indefinite"/>
</path>
```

### Scan line sweep
```svg
<rect x="0" y="0" width="120" height="3" fill="#06b6d4" opacity="0.15">
  <animate attributeName="y" values="-3;80;-3" dur="3s" repeatCount="indefinite"/>
</rect>
```

---

## Part 4 — React Component Pixel Icon

For use inside Next.js/React components (e.g. `HeroSection.tsx`, `ArchitectureSection.tsx`):

```typescript
const MY_ICON_PIXELS = [
  0,0,1,1,1,1,0,0,
  0,1,0,0,0,0,1,0,
  // ... 64 values total
];

function PixelIcon({ size = 32 }: { size?: number }) {
  const cell = Math.floor((size - 4) / 8);
  return (
    <div
      className="grid p-0.5"
      style={{
        width: size,
        height: size,
        gridTemplateColumns: `repeat(8, ${cell}px)`,
        gridTemplateRows: `repeat(8, ${cell}px)`,
        gap: "1px",
        imageRendering: "pixelated",
      }}
    >
      {MY_ICON_PIXELS.map((on, i) => (
        <div key={i} style={{ backgroundColor: on ? "#06b6d4" : "transparent" }} />
      ))}
    </div>
  );
}
```

For multi-color icons, use an array of color strings instead of 0/1:
```typescript
const pixels = [
  "transparent", "#8b5cf6", "#8b5cf6", ...  // row 0
  "#06b6d4", ...                              // row 1
  "#f59e0b", ...                              // cursor pixel
];
// Render: style={{ backgroundColor: pixels[i] }}
```

---

## Part 5 — Named Icon Library

Quick reference for icon color assignments by service/concept:

| Icon | Color | Notes |
|------|-------|-------|
| PostgreSQL | `#60a5fa` | Blue, elephant silhouette or cylinder |
| MySQL | `#f97316` | Orange, dolphin or stacked discs |
| MongoDB | `#4ade80` | Green, leaf shape |
| S3 / MinIO | `#fbbf24` | Yellow, S-curve or bucket |
| Trino | `#06b6d4` | Cyan, T-bar shape |
| Snowflake | `#38bdf8` | Sky blue, snowflake/star |
| BigQuery | `#818cf8` | Indigo, lightning bolt |
| Slack | `#e879f9` | Pink, hash/grid |
| Teams | `#818cf8` | Indigo, T-person shape |
| Jira | `#38bdf8` | Sky blue, diamond arrow |
| Dashboard | `#818cf8` | Indigo, grid of squares |
| Charts | `#06b6d4` | Cyan, rising bars |
| iFrame | `#22d3ee` | Light cyan, nested frame |
| MCP App | `#f59e0b` | Amber, window + bubbles |
| LLM/AI | `#8b5cf6` | Purple, brain/neural net |
| OmniQuery Hub | multi | Cyan border, purple header, amber cursor |

---

---

## Part 6 — OmniQuery Logo (Official Pixel SVG)

### ⚠️ Watermark Rule
**ALWAYS add the OmniQuery watermark** to any card, flow diagram, architecture canvas, or standalone visual generated for a blog post or marketing asset. Place it in the **bottom-right corner** of the SVG canvas. Never omit it.

---

### Logo Mark Only (48×48) — for hub centers, small icons

The pixel art portion of the logo — octagonal cyan border, purple SQL header bar, two cyan data rows, blinking amber cursor:

```svg
<!-- OmniQuery logo mark — place with transform="translate(x, y)" -->
<g>
  <!-- Background square -->
  <rect width="48" height="48" fill="#060c18" shape-rendering="crispEdges"/>
  <rect width="48" height="48" fill="none" stroke="#06b6d4"
        stroke-width="1" stroke-opacity="0.40" shape-rendering="crispEdges"/>
  <!-- Pixel art (octagonal border + SQL window) -->
  <g filter="url(#glow)">
    <!-- Top border row -->
    <rect x="6.5"  y="0.5"  width="5" height="5" fill="#06b6d4" shape-rendering="crispEdges"/>
    <rect x="12.5" y="0.5"  width="5" height="5" fill="#06b6d4" shape-rendering="crispEdges"/>
    <rect x="18.5" y="0.5"  width="5" height="5" fill="#06b6d4" shape-rendering="crispEdges"/>
    <rect x="24.5" y="0.5"  width="5" height="5" fill="#06b6d4" shape-rendering="crispEdges"/>
    <rect x="30.5" y="0.5"  width="5" height="5" fill="#06b6d4" shape-rendering="crispEdges"/>
    <rect x="36.5" y="0.5"  width="5" height="5" fill="#06b6d4" shape-rendering="crispEdges"/>
    <!-- Left/right side pixels -->
    <rect x="0.5"  y="6.5"  width="5" height="5" fill="#06b6d4" shape-rendering="crispEdges"/>
    <rect x="42.5" y="6.5"  width="5" height="5" fill="#06b6d4" shape-rendering="crispEdges"/>
    <rect x="0.5"  y="12.5" width="5" height="5" fill="#06b6d4" shape-rendering="crispEdges"/>
    <rect x="12.5" y="12.5" width="5" height="5" fill="#06b6d4" shape-rendering="crispEdges"/>
    <rect x="18.5" y="12.5" width="5" height="5" fill="#06b6d4" shape-rendering="crispEdges"/>
    <rect x="24.5" y="12.5" width="5" height="5" fill="#06b6d4" shape-rendering="crispEdges"/>
    <rect x="30.5" y="12.5" width="5" height="5" fill="#06b6d4" shape-rendering="crispEdges"/>
    <rect x="42.5" y="12.5" width="5" height="5" fill="#06b6d4" shape-rendering="crispEdges"/>
    <rect x="0.5"  y="18.5" width="5" height="5" fill="#06b6d4" shape-rendering="crispEdges"/>
    <rect x="42.5" y="18.5" width="5" height="5" fill="#06b6d4" shape-rendering="crispEdges"/>
    <!-- Purple SQL header row -->
    <rect x="0.5"  y="24.5" width="5" height="5" fill="#06b6d4" shape-rendering="crispEdges"/>
    <rect x="12.5" y="24.5" width="5" height="5" fill="#8b5cf6" shape-rendering="crispEdges"/>
    <rect x="18.5" y="24.5" width="5" height="5" fill="#8b5cf6" shape-rendering="crispEdges"/>
    <rect x="24.5" y="24.5" width="5" height="5" fill="#8b5cf6" shape-rendering="crispEdges"/>
    <rect x="42.5" y="24.5" width="5" height="5" fill="#06b6d4" shape-rendering="crispEdges"/>
    <!-- Data row 2 -->
    <rect x="0.5"  y="30.5" width="5" height="5" fill="#06b6d4" shape-rendering="crispEdges"/>
    <rect x="12.5" y="30.5" width="5" height="5" fill="#8b5cf6" shape-rendering="crispEdges"/>
    <rect x="18.5" y="30.5" width="5" height="5" fill="#8b5cf6" shape-rendering="crispEdges"/>
    <rect x="42.5" y="30.5" width="5" height="5" fill="#06b6d4" shape-rendering="crispEdges"/>
    <!-- Amber blinking cursor row -->
    <rect x="0.5"  y="36.5" width="5" height="5" fill="#06b6d4" shape-rendering="crispEdges"/>
    <rect x="12.5" y="36.5" width="5" height="5" fill="#f59e0b" shape-rendering="crispEdges">
      <animate attributeName="opacity" dur="1.1s" values="1;0;1" repeatCount="indefinite"/>
    </rect>
    <rect x="42.5" y="36.5" width="5" height="5" fill="#06b6d4" shape-rendering="crispEdges"/>
    <!-- Bottom border row -->
    <rect x="6.5"  y="42.5" width="5" height="5" fill="#06b6d4" shape-rendering="crispEdges"/>
    <rect x="12.5" y="42.5" width="5" height="5" fill="#06b6d4" shape-rendering="crispEdges"/>
    <rect x="18.5" y="42.5" width="5" height="5" fill="#06b6d4" shape-rendering="crispEdges"/>
    <rect x="24.5" y="42.5" width="5" height="5" fill="#06b6d4" shape-rendering="crispEdges"/>
    <rect x="30.5" y="42.5" width="5" height="5" fill="#06b6d4" shape-rendering="crispEdges"/>
    <rect x="36.5" y="42.5" width="5" height="5" fill="#06b6d4" shape-rendering="crispEdges"/>
  </g>
</g>
```

---

### Full Logo (mark + wordmark) — for watermarks on canvases

Dimensions: **180×36** (fits neatly in a corner). Scale down with `transform="scale(0.75)"` for smaller canvases.

```svg
<!--
  OmniQuery full logo watermark
  Usage: place at bottom-right with transform="translate(canvasW - 196, canvasH - 48)"
  The #glow filter must be defined in the parent SVG <defs>
-->
<g opacity="0.55">
  <!-- Icon background -->
  <rect width="36" height="36" fill="#060c18" shape-rendering="crispEdges"/>
  <rect width="36" height="36" fill="none" stroke="#06b6d4"
        stroke-width="0.75" stroke-opacity="0.40" shape-rendering="crispEdges"/>
  <!-- Scaled-down pixel art (original 48px → 36px = scale 0.75) -->
  <g transform="scale(0.75)" filter="url(#glow)">
    <rect x="6.5"  y="0.5"  width="5" height="5" fill="#06b6d4" shape-rendering="crispEdges"/>
    <rect x="12.5" y="0.5"  width="5" height="5" fill="#06b6d4" shape-rendering="crispEdges"/>
    <rect x="18.5" y="0.5"  width="5" height="5" fill="#06b6d4" shape-rendering="crispEdges"/>
    <rect x="24.5" y="0.5"  width="5" height="5" fill="#06b6d4" shape-rendering="crispEdges"/>
    <rect x="30.5" y="0.5"  width="5" height="5" fill="#06b6d4" shape-rendering="crispEdges"/>
    <rect x="36.5" y="0.5"  width="5" height="5" fill="#06b6d4" shape-rendering="crispEdges"/>
    <rect x="0.5"  y="6.5"  width="5" height="5" fill="#06b6d4" shape-rendering="crispEdges"/>
    <rect x="42.5" y="6.5"  width="5" height="5" fill="#06b6d4" shape-rendering="crispEdges"/>
    <rect x="0.5"  y="12.5" width="5" height="5" fill="#06b6d4" shape-rendering="crispEdges"/>
    <rect x="12.5" y="12.5" width="5" height="5" fill="#06b6d4" shape-rendering="crispEdges"/>
    <rect x="18.5" y="12.5" width="5" height="5" fill="#06b6d4" shape-rendering="crispEdges"/>
    <rect x="24.5" y="12.5" width="5" height="5" fill="#06b6d4" shape-rendering="crispEdges"/>
    <rect x="30.5" y="12.5" width="5" height="5" fill="#06b6d4" shape-rendering="crispEdges"/>
    <rect x="42.5" y="12.5" width="5" height="5" fill="#06b6d4" shape-rendering="crispEdges"/>
    <rect x="0.5"  y="18.5" width="5" height="5" fill="#06b6d4" shape-rendering="crispEdges"/>
    <rect x="42.5" y="18.5" width="5" height="5" fill="#06b6d4" shape-rendering="crispEdges"/>
    <rect x="0.5"  y="24.5" width="5" height="5" fill="#06b6d4" shape-rendering="crispEdges"/>
    <rect x="12.5" y="24.5" width="5" height="5" fill="#8b5cf6" shape-rendering="crispEdges"/>
    <rect x="18.5" y="24.5" width="5" height="5" fill="#8b5cf6" shape-rendering="crispEdges"/>
    <rect x="24.5" y="24.5" width="5" height="5" fill="#8b5cf6" shape-rendering="crispEdges"/>
    <rect x="42.5" y="24.5" width="5" height="5" fill="#06b6d4" shape-rendering="crispEdges"/>
    <rect x="0.5"  y="30.5" width="5" height="5" fill="#06b6d4" shape-rendering="crispEdges"/>
    <rect x="12.5" y="30.5" width="5" height="5" fill="#8b5cf6" shape-rendering="crispEdges"/>
    <rect x="18.5" y="30.5" width="5" height="5" fill="#8b5cf6" shape-rendering="crispEdges"/>
    <rect x="42.5" y="30.5" width="5" height="5" fill="#06b6d4" shape-rendering="crispEdges"/>
    <rect x="0.5"  y="36.5" width="5" height="5" fill="#06b6d4" shape-rendering="crispEdges"/>
    <rect x="12.5" y="36.5" width="5" height="5" fill="#f59e0b" shape-rendering="crispEdges">
      <animate attributeName="opacity" dur="1.1s" values="1;0;1" repeatCount="indefinite"/>
    </rect>
    <rect x="42.5" y="36.5" width="5" height="5" fill="#06b6d4" shape-rendering="crispEdges"/>
    <rect x="6.5"  y="42.5" width="5" height="5" fill="#06b6d4" shape-rendering="crispEdges"/>
    <rect x="12.5" y="42.5" width="5" height="5" fill="#06b6d4" shape-rendering="crispEdges"/>
    <rect x="18.5" y="42.5" width="5" height="5" fill="#06b6d4" shape-rendering="crispEdges"/>
    <rect x="24.5" y="42.5" width="5" height="5" fill="#06b6d4" shape-rendering="crispEdges"/>
    <rect x="30.5" y="42.5" width="5" height="5" fill="#06b6d4" shape-rendering="crispEdges"/>
    <rect x="36.5" y="42.5" width="5" height="5" fill="#06b6d4" shape-rendering="crispEdges"/>
  </g>
  <!-- Wordmark next to icon -->
  <text x="42" y="24"
        font-family="'Courier New', Courier, monospace"
        font-size="14" font-weight="700" letter-spacing="-0.2"
        fill="white">OmniQuery<tspan fill="#06b6d4">.ai</tspan></text>
</g>
```

### Watermark Placement Formula

```
Canvas W × H  →  translate(W - 196, H - 48)

Examples:
  960 × 540   →  translate(764, 492)
  800 × 450   →  translate(604, 402)
  600 × 400   →  translate(404, 352)
  400 × 300   →  translate(204, 252)
```

Always wrap in `<g opacity="0.55">` so it doesn't overpower the main content. Reduce to `opacity="0.35"` on very busy/dark backgrounds.

---

## Workflow

1. **Understand the request** — what type of asset: single icon, icon set, flow diagram, or architecture canvas?
2. **Choose the right approach**:
   - Single icon → 8×8 pixel map → SVG rects or React component
   - Flow/architecture → full SVG canvas with cards, hub, connectors, animations
3. **Pick colors** from the brand palette above — match by service/concept role
4. **Build the SVG** — always include `shape-rendering="crispEdges"` on all pixel rects
5. **Add animations** — at minimum: pulsing status dots; for flow diagrams: animateMotion dots + path shimmer
6. **⚠️ Add OmniQuery watermark** — for ANY card, flow diagram, architecture canvas, or blog visual:
   - Use the full logo snippet from Part 6
   - Place at `transform="translate(W - 196, H - 48)"` (bottom-right)
   - Wrap in `<g opacity="0.55">`
   - **This step is mandatory and must never be skipped**
7. **Save to the right location**:
   - Standalone SVG → `new-landing-page/public/{name}.svg`
   - React icon → inline in the relevant component file
   - Flow/architecture diagram → `new-landing-page/public/{name}.svg` + render via `<Image unoptimized>`
8. **Verify**: open in browser, check animations play, check watermark is visible in bottom-right corner
