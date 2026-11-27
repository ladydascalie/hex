# The hex design language

The documented contract for `tokens.css`. Use the tokens, never raw values.

## Palette

Dark-first: `:root` is the dark tier, and the light tier overrides it. Both
tiers are first-class, and nothing may hard-code a tier-specific colour.

| Role | Seed | Tokens |
|---|---|---|
| Brand and accent | head green `#3D6756` | `--accent`, `--accent-strong`, `--accent-lt`, `--on-accent` |
| Surfaces and chrome | wing slate `#363341` | `--bg`, `--surface`, `--surface-2`, `--nav-*`, `--border*` |
| Text and muted | neck lavender `#ACAFC4` | `--text`, `--muted` |
| Links, info, focus | speculum periwinkle `#7B8CAB` | `--link` |
| Danger | chest oxblood `#54140A` | `--danger` |
| Warn | bill amber `#E0A94C` (derived) | `--warn` |

Rules:

- Status is never the brand. `--success`, `--warn`, `--danger` and `--link` are
  distinct from `--accent`, so a done check, a destructive badge and a link are
  never confused.
- Code surfaces stay dark in both tiers. Use the constant `--code-*` tokens
  inside a code block; a tier role there renders dark on dark in the light tier.
- Motion and shadows have tokens (`--duration-*`, `--ease`, `--shadow-*`). Do
  not invent values.

## Typography

- UI text is **Atkinson Hyperlegible Next** (`--font-sans`). Commands and code
  are **Atkinson Hyperlegible Mono** (`--font-mono`). Both are variable, latin
  and SIL OFL.
- `--font-shade` is **Shade Mono**, a small subset of Noto Sans Mono covering
  box drawing and shade blocks (`░▒▓`). Atkinson does not hold those glyphs, and
  the subset keeps a rail, a terminal grid or a shade mark identical instead of
  falling back to the OS.
- Code weight is `--mono-weight`: 450, or 600 under a bold-code preference.
- The type scale is `--text-2xs` to `--text-2xl`, every step multiplied by
  `--text-scale`. A reading-size preference moves `--text-scale` and nothing
  else; spacing and structural sizes stay put.
- Prose caps at `--measure` (72ch). Tables and code keep the column.

## Shape, spacing and density

- Radii are squared off: `--radius-sm|md|lg` (4, 6, 8px). Tickboxes are square.
- Spacing comes from `--space-hair` to `--space-7`; no raw px in margin, padding
  or gap. `--space-hair` is the sub-scale gap below `--space-1`.
- Interactive controls take their height from `--ctrl-pad-y`, so buttons,
  inputs and selects line up.
- Badges are bracketed `[ label ]`, not filled pills.
- Dark-on-light strokes read thinner, hence `--mono-weight: 450` by default.

## Hooks

- Dark: `:root`, with no attribute.
- Light: `html[data-theme="light"]`.
- Material writes its scheme to `<body>`, so the light tier also answers
  `body[data-md-color-scheme="default"]`. That second selector is an integration
  hook, not the theme's own; a host on another stack sets `data-theme`.

A host that needs an extra hook adds it in its own stylesheet if it can express
the tier from the tokens, and asks hex for one if it cannot.

## Changing a token

1. Decide the role, not the component. A token named after one component gets
   copied by the next one.
2. Add or change it in both tiers.
3. Add it to the table above in the same commit.
4. Move the version by the rule in the README: value is a patch, new is a minor,
   removed or renamed is a major.
5. Tag, and read the change on a real surface in both tiers before the tag
   leaves the machine.