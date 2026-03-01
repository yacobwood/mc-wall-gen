# Blockworks

A browser-based Minecraft wall designer. Pick a block palette, set your dimensions, and export the result as a PNG reference image for your next build.

**By [Yacobwood](https://github.com/yacobwood)**

<img src="Blockwork%20cobble.png" alt="Cobblestone wall example" width="32%"> <img src="Blockwork%20Tuff.png" alt="Tuff wall example" width="32%"> <img src="Blockwork%20Bricks.png" alt="Bricks wall example" width="32%">

---

## Installation

No build step or package manager required — it's a single HTML file.

**Option 1 — Download**

1. Download `index.html`
2. Open it in any modern browser (Chrome, Firefox, Safari, Edge)

**Option 2 — Clone**

```bash
git clone https://github.com/yacobwood/mc-wall-gen.git
cd mc-wall-gen
open index.html
```

> Requires an internet connection on first load to fetch the VT323 font and real Minecraft textures. Works offline once cached.

---

## Usage

### Dimensions

Set **Width** (1–64) and **Height** (1–32) in blocks. Use the **Zoom** slider to scale the preview between 1× and 4× (16–64px per block).

Toggle **Show row & column numbers** to overlay a coordinate grid on the image — included in exports.

### Block Palette

Browse 137+ blocks organised into 11 categories with sub-categories. Click a block's thumbnail or name to add it to your palette.

#### Selected panel

The **Selected** section at the top of the palette shows all active blocks. Each row has:

- A percentage slider — drag to adjust how often that block appears
- A **lock button** (🔒) — pins the percentage so it isn't affected when other sliders are moved

Sliders are constrained so the total always equals **100%**. Moving one slider redistributes the remainder proportionally across unlocked blocks.

The same sliders and lock buttons appear in the full block list below, and both stay in sync.

### Seed

- **Randomize Wall** — generates a new wall with a fresh random seed
- **Seed input** — enter any 8-character hex value to reproduce or share a specific wall

### Presets

Load curated palettes from the **Presets** dropdown:

| Classic | Community | Themed |
|---|---|---|
| Dungeon / Ruins | Back from the Mines | End City |
| Nether Fortress | Overgrown Path | Ice Palace |
| Deep Cave | Woodcutter | Basalt Delta |
| Desert Temple | Grove of Ashes | Tuff Tower |
| Ocean Monument | Ghost Valley | Mushroom House |
| Polished Mix | Italian Path | Golden Palace |
| Mossy Ruin | Undergrove | |
| | Barrel Roll | |
| | Old Garage | |
| | Rusty Roof | |
| | Warmer Wood | |
| | Coal House | |
| | Magical Fungi | |
| | Candy Leaves | |
| | Cabin Shower | |
| | Steampunk Blacksmith | |
| | Mumbo Mountain | |
| | Meadow in the City | |

### Export

Click **Export PNG** to download a lossless PNG named with the current seed (e.g. `blockworks-A3F2C891.png`). Row/column numbers are baked in if the overlay is enabled.

---

## Block Categories

Blocks are organised into 11 categories, each with sub-categories:

| Category | Sub-categories |
|---|---|
| **Stone** | Natural · Polished · Tuff · Brick |
| **Deepslate** | Natural · Brick |
| **Nether** | Natural · Basalt · Blackstone · Brick · Fungal |
| **Wood** | Planks · Log Bark · Log Top · Stripped Log |
| **Nature** | Leaves · Ground |
| **Terracotta** | 9 colour variants |
| **Masonry** | Brick · Sandstone · Quartz · Ocean |
| **End** | End Stone · End Stone Bricks · Purpur Block |
| **Copper** | All 5 oxidation stages |
| **Special** | Ice · Misc |
| **Minerals** | Iron · Gold · Lapis · Emerald · Diamond · Netherite |

---

## How It Works

Real Minecraft block textures are fetched from [InventivetalentDev/minecraft-assets](https://github.com/InventivetalentDev/minecraft-assets) (1.21.4, CORS-safe). Blocks without a real texture fall back to procedural generation using the Canvas 2D API:

- **Flat noise** — uniform base colour with pixel-level variation
- **Voronoi** — irregular cell pattern for cobblestone variants
- **Brick** — running bond pattern with configurable mortar
- **Grain** — stripe variation for deepslate, sandstone, logs
- **Specks** — contrasting pixel speckles for granite, diorite, gilded blackstone
- **Wood planks** — horizontal plank strips with edge darkening
- **Log bark** — vertical column grain
- **Log top** — concentric ring end-grain pattern
- **Leaves** — dense noise with biome tint applied via canvas `multiply` blend

Walls are seeded with `mulberry32` (a fast 32-bit PRNG), so any seed always produces the same wall. Each block cell consumes two RNG values so texture variant selection is stable regardless of texture source.

---

## Browser Support

Requires `OffscreenCanvas` — available in all modern browsers (Chrome 69+, Firefox 105+, Safari 16.4+, Edge 79+).
