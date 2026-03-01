# Blockwork

A browser-based Minecraft wall designer. Set your dimensions, pick a block palette with percentage controls, and export the result as a PNG reference image.

**By [Yacobwood](https://github.com/yacobwood)**

## Installation

No build step or package manager required. It's a single HTML file.

**Option 1 — Download**

1. Download `index.html`
2. Open it in any modern browser (Chrome, Firefox, Safari, Edge)

**Option 2 — Clone**

```bash
git clone https://github.com/yourusername/minecraft-random-wall.git
cd minecraft-random-wall
open index.html
```

> **Note:** Requires an internet connection on first load to fetch the VT323 font from Google Fonts. The tool itself works fully offline once the font is cached.

---

## Usage

### Dimensions

Set the **Width** (1–64 blocks) and **Height** (1–32 blocks) of your wall. The canvas updates live as you type.

Use the **Block size** slider to zoom in or out — options are 16, 24, 32, 48, and 64px per block.

### Block Palette

Browse blocks by category in the left sidebar. Click a block's name or preview image to toggle it in your palette. When selected, a **percentage slider** appears beneath it.

Sliders are constrained so the total always equals **100%**. Dragging one slider redistributes the remainder proportionally across the other active blocks.

### Randomize

- **Randomize Wall** — generates a new wall with a fresh random seed
- **Same Seed** — re-renders the current wall (useful after changing the palette)
- **Seed input** — type any 8-character hex value to reproduce a specific wall and share it with others

### Presets

The **Presets** dropdown loads curated block combinations. Includes 7 classic Minecraft build styles and 18 community palettes:

| Classic | Community |
|---|---|
| Dungeon / Ruins | Back from the Mines |
| Nether Fortress | Overgrown Path |
| Deep Cave | Woodcutter |
| Desert Temple | Grove of Ashes |
| Ocean Monument | Ghost Valley |
| Polished Mix | Italian Path |
| Mossy Ruin | Undergrove |
| | Barrel Roll |
| | Old Garage |
| | Rusty Roof |
| | Warmer Wood |
| | Coal House |
| | Magical Fungi |
| | Candy Leaves |
| | Cabin Shower |
| | Steampunk Blacksmith |
| | Mumbo Mountain |
| | Meadow in the City |

### Export

Click **Export PNG** to download the wall as a lossless PNG, named with the current seed (e.g. `mc-wall-A3F2C891.png`).

---

## Block Categories

| Category | Blocks |
|---|---|
| **Stone** | Stone, Cobblestone, Mossy Cobblestone, Smooth Stone, Stone Bricks, Mossy Stone Bricks, Cracked Stone Bricks, Chiseled Stone Bricks |
| **Polished Stone** | Andesite, Polished Andesite, Diorite, Polished Diorite, Granite, Polished Granite |
| **Deepslate** | Deepslate, Cobbled Deepslate, Polished Deepslate, Deepslate Bricks, Mossy Deepslate Bricks, Deepslate Tiles, Cracked Deepslate Bricks |
| **Nether** | Nether Bricks, Cracked Nether Bricks, Red Nether Bricks, Blackstone, Polished Blackstone, Polished Blackstone Bricks, Gilded Blackstone, Crimson Planks, Warped Planks, Crimson Nylium |
| **Wood** | Oak, Dark Oak, Spruce, Birch, Jungle, Acacia, Mangrove, Cherry, Bamboo Planks |
| **Nature** | Oak Leaves, Spruce Leaves, Azalea Leaves, Grass Block, Coarse Dirt |
| **Terracotta** | Terracotta, Red, Orange, Yellow, Lime, White, Pink, Brown, Gray Terracotta |
| **Other** | Brick, Quartz Bricks, Sandstone, Red Sandstone, Mud Bricks, Prismarine, Prismarine Bricks, Dark Prismarine, Amethyst Block, Obsidian, Coal Block, Copper Block, Oxidized Copper, White Concrete, Red Concrete |

---

## How It Works

All block textures are procedurally generated in the browser using the Canvas 2D API — no image assets are loaded. Each block type uses one of several texture algorithms:

- **Flat noise** — uniform base colour with pixel-level random variation
- **Voronoi** — irregular stone cell pattern (cobblestone variants)
- **Brick** — configurable running bond pattern with mortar lines
- **Grain** — horizontal stripe variation (deepslate, sandstone)
- **Specks** — base colour with contrasting pixel specks (granite, diorite, gilded blackstone)
- **Wood planks** — horizontal plank strips with edge darkening and grain noise
- **Leaves** — dense noise with dark shadow patches; azalea variant adds pink flower pixels

Walls are seeded with `mulberry32`, a fast 32-bit PRNG, so any seed produces the same wall every time. Each block cell uses a unique sub-seed so identical block types never tile visibly.

---

## Browser Support

Requires `OffscreenCanvas` support — available in all modern browsers (Chrome 69+, Firefox 105+, Safari 16.4+, Edge 79+).
