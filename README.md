# inference-to-agent

A weekend-hackathon curriculum: walk the LLM stack from one local inference call up to a hand-built document-Q&A agent. Fully local (Ollama), freeCodeCamp resources, right-sized models.

## What's here

- `public/index.html` — the curriculum site (self-contained, served by Cloudflare Pages)
- `weekend-ai-curriculum.html` — working copy of the same site
- `weekend-ai-curriculum.md` — the source curriculum in Markdown

## Deploy

Connected to Cloudflare Pages via native Git integration. Every push to `main` triggers a build.

- **Build command:** none (static)
- **Build output directory:** `public`

Edit `public/index.html`, commit, push. Cloudflare rebuilds automatically.
