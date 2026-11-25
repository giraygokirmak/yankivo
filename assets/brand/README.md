# Yankivo visual identity

## Files

- `yankivo-logo.svg`: Horizontal wordmark and icon, 1200 × 360 view box; used in the README.
- `yankivo-logo.png`: 1200 × 360 raster export of the logo.
- `yankivo-icon.svg`: Square source for avatars, application icons, and favicons; 512 × 512.
- `yankivo-icon.png`: 512 × 512 raster export of the icon.

## Design language

The microphone capsule and circuit stem beneath it represent voice and hardware. The paired
arcs on either side represent the listen-and-respond cycle. Deep navy represents the device;
the turquoise-to-mint gradient represents a live audio signal.

| Color | Hex | Use |
| --- | --- | --- |
| Night | `#10172F` | Main background |
| Navy | `#273664` | Background gradient |
| Signal | `#55E5D5` → `#7CECBA` | Microphone and audio waves |
| Wordmark | `#F3F9FF` | Lettering on the navy background |
| Circuit | `#8FB6DF` | Subtle circuit details |

The logo appears on a navy horizontal banner, so it looks the same on GitHub's light and dark
themes. There are no external font, CSS, or image dependencies; the lettering and shapes are
all SVG paths.

## Usage

- Keep clear space around the icon and wordmark of at least 10% of the icon's width.
- Do not skew the logo, change its gradients, or reposition its elements.
- Use only the square icon at small sizes.
- Preserve the SVG sources; generate raster exports at 1× and 2× sizes as needed.
