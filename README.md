# Myop Self-Hosted Components (Git-based)

This repository automatically syncs [Myop](https://myop.dev) components as static JSON files, committed directly into this repo.

When you release a component in the Myop dashboard, a GitHub Actions workflow exports it and commits the updated files here. You can then serve these files from any static host, or use them directly from the repo.

## How it works

```
Release in Myop dashboard
        |
        v
Myop fires repository_dispatch --> GitHub Actions runs
                                        |
                                  npx myop export
                                        |
                                  git commit & push
                                        |
                                  Components stored in /components/
```

## Setup

1. Add your Myop API key as a repository secret: **Settings > Secrets > Actions > `MYOP_API_KEY`**
2. Connect this repo from the Myop dashboard: **Rollout > Settings > Self-Hosting > Add GitHub Actions**
3. That's it — components will auto-sync on every release

## Serving the files

The exported JSON files in `/components/` can be served from:

- **GitHub Pages** — enable Pages on this repo pointing to the root or `/components`
- **Any static host** — clone/pull this repo in your deployment pipeline
- **Raw GitHub URLs** — use `raw.githubusercontent.com` (not recommended for production)

## File structure

```
components/
  {componentId}/
    production.json
    staging.json
    preview.json
  manifest.json
```

## Configuration

| Secret | Description |
|--------|-------------|
| `MYOP_API_KEY` | Your Myop API key from Dashboard > Self-Hosting |

See the [Myop self-hosting docs](https://docs.myop.dev/docs/self-hosting/) for more details.
