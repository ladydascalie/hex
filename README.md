# hex

hex is a design language: a token layer, self-hosted fonts, and the rules that
hold them together. This repository is the single definition. A host consumes a
pinned tag.

## What's here

| file | what it is |
| --- | --- |
| `tokens.css` | colour, type, spacing, radii, shadows, motion, as custom properties |
| `fonts.css` | the `@font-face` rules for Atkinson Hyperlegible Next, Atkinson Hyperlegible Mono and the Shade subset |
| `fonts/` | the self-hosted variable fonts, latin, each beside its licence |
| `DESIGN.md` | the contract: what each token means, and what a host may not do |
| `LICENSE` | FSL-1.1-MIT, for `tokens.css` and `fonts.css` |

## Consuming it

Fetch the tag you pinned from the releases:

```
https://github.com/ladydascalie/hex/releases/download/vX.Y.Z/tokens.css
https://github.com/ladydascalie/hex/releases/download/vX.Y.Z/fonts.css
https://github.com/ladydascalie/hex/releases/download/vX.Y.Z/fonts.tar.gz
https://github.com/ladydascalie/hex/releases/download/vX.Y.Z/LICENSE
```

`fonts.css` expects a `fonts/` directory beside it, and `fonts.tar.gz` unpacks
to one. Link `fonts.css` first, then `tokens.css`:

```html
<link rel="stylesheet" href="hex/fonts.css">
<link rel="stylesheet" href="hex/tokens.css">
```

The dark tier is `:root`, so it needs no attribute. Set `data-theme="light"` on
`<html>` for the light tier.

A host can vendor the files instead of fetching at build time, as long as it
records the tag it took and rebuilds when it moves.

## Changing it

- A changed value is a patch. A new token is a minor. A removed or renamed
  token is a major, because a host will break on it.
- Name a token by its role, not by the component that first needed it.
- Give every colour token a value in both tiers, unless it is a code-surface
  constant.
- Update `DESIGN.md` in the same commit as the token.
- Tag the commit. The release workflow publishes the assets, and a tag can be
  fetched but not edited, so read both tiers on a real surface before you tag.

## Licence

The token layer and `fonts.css` are FSL-1.1-MIT; see `LICENSE`. The fonts are
SIL OFL 1.1, and each licence file travels beside the font it covers.