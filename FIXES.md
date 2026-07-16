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
