# TCP Themes

Custom looks for **Thor Command Panel** (TCP), the AYN Thor's bottom-screen overlay. This repo was made from the TCP theme template. Share its link, and anyone can follow it in the app to get these looks and every update you push.

## Use these looks

1. In Thor Command Panel, open **Themes → Theme repos**.
2. Paste this repo's link (`https://github.com/<owner>/<repo>`) and press **Follow**.
3. The looks appear under **My looks**. Press **Update** later to get changes. The app also checks once a day when you open Themes.

Looks from a repo are replaced when the repo changes. To customize one, open it in Theme Studio and use **Save as new**, so your copy is never overwritten.

## Make your own theme repo

1. On GitHub, press **Use this template → Create a new repository**.
2. Build looks in the app's **Theme Studio**, then use **My looks → Export all as a pack**. It writes a pack to `/sdcard/TCP Themes/themes/` on the device, and the fonts it uses to `/sdcard/TCP Themes/fonts/`.
3. Copy the `.tcplooks.json` files into this repo's `themes/` folder. Commit and push.
4. Share the repo link.

You can also edit packs by hand. The format is below.

## Layout

```
themes/   Theme packs: *.tcplooks.json files. Each file holds any number of looks.
fonts/    Font files the packs use (.ttf / .otf), matched by file name. Not committed by default (see Fonts).
```

On the device, the app uses the same layout in `/sdcard/TCP Themes/`.

## Fonts

Packs reference fonts **by file name**. When someone adds a look, the app looks for the font in this order:

1. A font already installed in the app with that file name.
2. `/sdcard/TCP Themes/fonts/<file name>` on their device.
3. A download URL you list in the pack's `fonts` section. The app asks before downloading, and shows the host and license.
4. Otherwise the default font is used.

**Only list fonts you're allowed to share**, and prefer official sources. [Google Fonts](https://github.com/google/fonts) (SIL OFL) works well. Link the raw file:

```
https://github.com/google/fonts/raw/main/ofl/<family>/<File>.ttf
```

`fonts/` is in `.gitignore`, so you don't commit font files by accident. If a font's license allows redistribution and you want to ship it in the repo, remove that ignore rule.

## Pack format (`*.tcplooks.json`)

```json
{
  "format": "tcp-looks",
  "version": 1,
  "name": "My Pack",
  "author": "you",
  "description": "What these looks are about",
  "fonts": {
    "Orbitron.ttf": { "url": "https://github.com/google/fonts/raw/main/ofl/orbitron/Orbitron%5Bwght%5D.ttf", "license": "OFL" }
  },
  "looks": [
    { "id": "neon-terminal", "name": "Neon Terminal", "baseLook": "TERMINAL", "card": "NEON_TUBE" }
  ]
}
```

Each look starts from a `baseLook` and overrides only what you set. **Keep each look's `id` the same across updates.** That's how the app replaces a look in place instead of adding a duplicate. If you leave `id` out, it's derived from the name.

| Field | Values |
|---|---|
| `baseLook` | `AUTO`, `AURORA_GLASS`, `CARTRIDGE`, `TACTICAL_HUD`, `SOFT_CONSOLE`, `SOFT_CONSOLE_OLED`, `SEGMENT_LCD`, `BLOOM`, `NEON_ARCADE`, `TERMINAL`, `COCKPIT`, `STICKER_BOOK`, `INDUSTRIAL`, `JELLY`, `COMIC_PANEL`, `Y2K_CHROME`, `E_INK` |
| `card` | `SOLID`, `GLASS`, `BRUTALIST`, `CHAMFER_HUD`, `SOFT_EXTRUDED`, `LCD_RECESSED`, `BLOOM_TONAL`, `NEON_TUBE`, `TERMINAL_FRAME`, `BEZEL`, `STICKER_NOTE`, `HAZARD_PLATE`, `JELLY`, `INK_PANEL`, `CHROME_RIM`, `HAIRLINE`, `CUSTOM` |
| `tile` | `STOCK`, `PIXEL`, `GLASS_GLOW`, `BRUTALIST`, `HUD`, `SOFT_PRESS`, `LCD`, `BLOOM_BLOB`, `NEON`, `TERMINAL_ROW`, `SWITCH_LED`, `STICKER`, `PLATE`, `GEL`, `STARBURST`, `CHROME`, `INK_OUTLINE`, `CUSTOM` |
| `gauge` | `RING`, `GLOW_RING`, `SEGMENT_METER`, `SEGMENTED_ARC`, `INSET_RING`, `LCD_BAR`, `WAVY_ARC`, `NEON_RING`, `ASCII_BAR`, `NEEDLE_DIAL`, `STICKER_DONUT`, `RULER_BAR`, `CAPSULE`, `PIE`, `CHROME_RING`, `DITHER_BAR`, `CUSTOM` |
| `slider` | `STOCK`, `PIXEL`, `GLOW_GRADIENT`, `BRUTALIST`, `SEGMENTED`, `GROOVE`, `LCD_SEGMENTS`, `WAVY`, `NEON_TUBE`, `ASCII`, `FADER`, `STICKER`, `RULER`, `GEL`, `INK`, `CHROME`, `DITHER`, `CUSTOM` |
| `nav` | `TILE`, `GLASS_PILL`, `INK_BLOCK`, `BRACKETS`, `PRESSED`, `LCD_INVERT`, `EXPRESSIVE_PILL`, `NEON_UNDERLINE`, `PROMPT_INVERT`, `LED_SWITCH`, `STICKER`, `HAZARD_UNDERLINE`, `GEL_PILL`, `STARBURST`, `FOIL_PILL`, `UNDERLINE_ITALIC`, `CUSTOM` |
| `backdrop` | `SOLID`, `AURORA`, `PAPER_DOTS`, `HUD_GRID`, `LCD_PIXEL_GRID`, `SYNTH_GRID`, `HALFTONE` |
| `header` | `NONE`, `INK_STRIP`, `INDEXED_MONO`, `TITLED_FRAME` |
| `labelFont` / `displayFont` | `{"bundled": "MONO"}` (one of `DEFAULT`, `CONDENSED`, `CONDENSED_DISPLAY`, `MONO`, `SEGMENT`, `ROUNDED`, `STENCIL`, `COMIC`, `CHROME_WIDE`, `SERIF`) or `{"file": "Orbitron.ttf"}` |
| `panelCardShape`, `tileShape`, `sliderControlShape`, `sliderTrackShape`, `dialogShape`, `fpsBadgeShape` | `{"kind": "ROUNDED" \| "RECT" \| "CHAMFER" \| "SQUIRCLE" \| "PILL" \| "CIRCLE", "size": 12}` |
| `labelCase` | `NONE`, `UPPER`, `LOWER`, `SNAKE` |
| `colors` | `{"accent": "#FF22B8F0", "accent2": "…", "background": "…", "panel": "…"}`. Each is optional; leave one out to follow the device theme. |
| effects | `glow`, `scanlines`, `animate`, `liftedBackdrop`, `oledBackdrop`, `ghostSegments` (true/false); `outlineWidth`, `shadowOffset` (dp); `backdropPatternAlpha` (0–1); `letterSpacingEm` |
| fit | `ringDiameterRatio`, `ringValueScale`, `ringTitleScale`, `ringUnitScale`, `infoValueScale`, `qsLabelFontSize` |
| `custom` | Settings for parts set to `CUSTOM`. The easiest way to get these right is to build the look in Theme Studio and export it. |

Unknown values are ignored (the base look's value is used), and numbers are clamped to safe ranges. A typo won't break a pack.
