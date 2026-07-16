# Infinite Canvas (monorepo)

Fork / working copy of [basketikun/infinite-canvas](https://github.com/basketikun/infinite-canvas), organized as the upstream monorepo layout, with a Seedream-compatible image API fix.

## Layout

```text
.
├── web/                 # Vite + React frontend
├── canvas-agent/        # Local MCP Canvas Agent
├── plugins/             # Codex app plugin
├── docs/                # Documentation
├── Dockerfile
├── docker-compose.yml
├── nginx.conf
└── FIX-OUTPUT-FORMAT.md # Patch notes
```

## Fix included

`web/src/services/api/image.ts` no longer sends hardcoded:

```ts
output_format: "png"
```

Some models (e.g. Doubao Seedream) reject that parameter. Requests keep:

```ts
response_format: "b64_json"
```

Verified on `https://canvas.aobrodzo.dpdns.org` (incognito generation succeeded).

## Local development

```bash
cd web
bun install
bun run dev
```

## Docker

```bash
docker compose up -d
```

Default: `http://localhost:3000`

## Notes

- Browser storage holds API keys / canvas data by default
- If a normal browser still shows the old `output_format` error, hard-refresh or clear site data for the canvas domain; custom channel scripts can also inject that field
