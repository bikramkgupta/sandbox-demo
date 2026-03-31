# Sandbox Demo: Snapshot, Fork, Preview

Demo application for DigitalOcean's Deploy conference showcasing the [do-app-sandbox](https://github.com/digitalocean-labs/do-app-sandbox) SDK's snapshot/fork/preview workflow.

## What's Inside

A **Flask + HTMX todo app** with 3 feature variants, demonstrating how an AI agent can deploy multiple implementations as live previews for a product manager to choose from.

| File | Description |
|------|-------------|
| `app.py` | Base todo app — clean UI, add/toggle/delete todos |
| `variants/priority_color_badges.py` | Adds colored priority dots (red/yellow/green) |
| `variants/priority_drag_reorder.py` | Adds drag-to-reorder with SortableJS |
| `variants/priority_smart_suggest.py` | Suggests priority from text keywords |
| `demo_runner.py` | Orchestrates the full demo flow |
| `deploy-demo-flow.pptx` | Conference presentation with screenshots |

## Quick Start (Local)

```bash
python3 -m venv .venv && source .venv/bin/activate
pip install flask
python app.py  # http://localhost:8080
```

Try each variant:
```bash
python variants/priority_color_badges.py
python variants/priority_drag_reorder.py
python variants/priority_smart_suggest.py
```

## Demo Flow (on App Platform)

```bash
pip install do-app-sandbox
source .env.demo  # Set SPACES_* and DIGITALOCEAN_TOKEN

# Full interactive demo
python demo_runner.py

# Or pre-create snapshot, then run from it live
python demo_runner.py --pre-snapshot
python demo_runner.py --from-snapshot <snapshot_id>
```

### What happens:

1. **Base app** is deployed to a sandbox on App Platform
2. **Snapshot** archives the running app (with deps) to DO Spaces
3. **Fork x3** restores the snapshot to 3 new sandboxes in parallel
4. Each sandbox gets a **different variant** uploaded and started
5. All 3 get **public HTTPS URLs** — open side by side, PM picks the winner

## Requirements

- Python 3.10+
- `do-app-sandbox` SDK (`pip install do-app-sandbox`)
- DigitalOcean account with API token
- DO Spaces bucket (for snapshots)

## Screenshots

| Base App | Color Badges | Drag Reorder | Smart Suggest |
|----------|-------------|-------------|--------------|
| ![base](screenshots/base_app.png) | ![badges](screenshots/color_badges.png) | ![drag](screenshots/drag_reorder.png) | ![smart](screenshots/smart_suggest.png) |

## License

MIT
