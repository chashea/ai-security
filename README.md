# AI Security Architecture

A single-page reference visualization of Microsoft's AI security stack — how **Microsoft Defender**, **Microsoft Purview**, **Microsoft Entra**, **Defender for Cloud**, and **Agent governance** fit together to secure AI workloads, agents, and data.

🔗 **Live site:** <https://chashea.github.io/ai-security/>

## What's inside

- **Interactive architecture diagram** — click any pillar to drill into its capabilities and signal flows
- **Five product pillars** with detailed capability cards (Defender XDR, Purview, Entra, Defender for Cloud, Agent governance)
- **Threat scenarios** — end-to-end walkthroughs (Shadow AI data leak, prompt injection, agent compromise, etc.) showing which products detect, contain, and remediate
- **Implementation roadmap** — a phased rollout plan

## Tech

- Single static `index.html`, no build step
- [Microsoft Fluent UI Web Components](https://learn.microsoft.com/fluent-ui/web-components/) (Fluent 2) loaded from the unpkg CDN
- Dark theme with Fluent 2 design tokens, Segoe UI Variable typography
- Hosted on GitHub Pages from `main`

## Local preview

```bash
# any static server works
python3 -m http.server 8000
# then open http://localhost:8000
```

## Deploy

Pushes to `main` are published automatically by GitHub Pages.
