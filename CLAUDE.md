# Shapez 2 Blueprints

Personal blueprint collection for Shapez 2.

## Tools

Companion repo: `~/Projects/shapez2-tools/` (https://github.com/agude/Shapez-2-Tools)

```bash
cd ~/Projects/shapez2-tools
uv run shapez2 info <file>           # Show blueprint info
uv run shapez2 icon <file>           # View icon
uv run shapez2 icon <file> --set ... # Set icon
uv run shapez2 decode <file>         # Decode to JSON
```

## Naming Convention

**Scale prefix:**
- `Full Belt` - handles full space belt throughput (12 lanes, manifolded 4x internally)
- `Quarter` - old bandwidth, single platform (1x1, 1x2, or 2x2)
- No prefix for specialized layouts (miners, crystallizers)

**Pattern:** `[Scale] [Operation] [Details]`

Examples:
- `Full Belt Rotate 90 CW`
- `Quarter Destroy East Half`
- `3 Level Balanced Miner`

## Icon Convention

Blueprints have 4 icon slots. Use `icon:<name>` or `shape:<code>`.

| Slot | Purpose | Examples |
|------|---------|----------|
| 1 | Scale | `icon:layout.Layout_SpaceBeltNode` (Full Belt), `icon:Platforms` (Quarter), `icon:layout.Layout_ShapeMiner` (Miner) |
| 2 | Input shape | `shape:RuRuRuRu`, or `null` |
| 3 | Modifier | `icon:Number3` (layers/count), or `null` |
| 4 | Operation | Building icon or output shape |

**By category:**

| Category | Slot 1 | Slot 2 | Slot 3 | Slot 4 |
|----------|--------|--------|--------|--------|
| Rotators | Scale | - | - | `icon:building.Rotator*Variant` |
| Stackers | Scale | - | - | `icon:building.StackerDefaultVariant` |
| Painters | Scale | - | - | `icon:building.PainterDefaultVariant` |
| Trash | Scale | - | - | `icon:building.TrashDefaultVariant` |
| Monitors | Scale | - | - | `icon:building.BeltReaderDefaultVariant` |
| Destroyers | Scale | Input | - | Output shape |
| Swappers | Scale | Before | - | After shape |
| Extractors | Scale | Input | - | Cutter icon or output |
| Balancers | Scale | - | Count | `icon:building.MergerTShapeVariant` |
| Crystallizer | Scale | - | Layers | `icon:building.CrystalGeneratorDefaultVariant` |
| Miners | Layout | - | Layers | `icon:building.ExtractorDefaultVariant` or `PumpDefaultVariant` |
| Pinners | Scale | - | - | `icon:building.PinPusherDefaultVariant` |

## File Format

`.spz2bp` files are: `SHAPEZ2-[version]-[base64(gzip(JSON))]$`

- Name/description: filename only (not in JSON)
- Icons: `BP.Icon.Data` array (4 slots)
- Buildings: `BP.Entries` array with X, Y, L (layer), R (rotation), T (type)

## Folder Structure

Folders appear as in-game categories. Keep non-blueprint files (like this one) as `.md` - they won't show in-game.
