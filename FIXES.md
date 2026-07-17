# Local fixes in this fork

## Seedream `output_format` fix

`web/src/services/api/image.ts` no longer sends hardcoded `output_format: "png"` for:

- `/images/generations`
- `/images/edits`

Some providers (for example Doubao Seedream) reject that parameter with:

```text
The parameter `output_format` specified in the request is not valid
```

Verified on `https://canvas.aobrodzo.dpdns.org` in incognito after patching the served frontend asset.


## Seedream size minimum fix

Seedream / Doubao / Volcengine Ark image generation rejects sizes under `3686400` total pixels:

```text
The parameter `size` specified in the request is not valid: image size must be at least 3686400 pixels
```

`web/src/services/api/image.ts` now:

- detects Seedream-like providers by model **or** base URL (`seedream`, `doubao`, `volces`, `volcengine`, `ark`, `ep-`)
- enforces `SEEDREAM_MIN_PIXELS = 3686400`
- auto-scales ratio / pixel sizes up to the minimum
- always sends an explicit legal `size` for Seedream-like models (including `auto`)
- defaults image quality to `medium` for safer first-run sizes
