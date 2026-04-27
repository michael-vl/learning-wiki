# Learning Wiki

A personal wiki on Blender, Unity, and Godot, built with [Zensical](https://zensical.org).

## Topics

- **Blender — Shaders & Node Programming** — shader editor, geometry nodes, OSL.
- **Blender — Beginner to Advanced** — full pipeline including a dedicated topology guide.
- **Unity — Beginner to Advanced** — Unity 6 LTS, URP, new Input System, ScriptableObjects.
- **Godot — Beginner to Advanced** — Godot 4.x, GDScript 2.0, signals, custom resources.
- **KiCad — Beginner to Advanced** — schematic capture, PCB layout, custom libraries, fabrication outputs.

The actual wiki content lives in [`docs/`](./docs/). Browse it on GitHub or visit the deployed site (link below once Pages is enabled).
https://michael-vl.github.io/learning-wiki/

## Local development

```bash
# one-time setup
python3 -m venv .venv
source .venv/bin/activate          # Windows: .venv\Scripts\activate
pip install -r requirements.txt

# preview live with hot reload
zensical serve -o                  # opens browser at http://localhost:8000

# one-shot static build
zensical build --clean             # output in site/
```

## Deployment

The `.github/workflows/docs.yml` workflow builds and deploys to GitHub Pages on every push to `main` / `master`.

To enable:
1. Push this repo to GitHub.
2. Repo → Settings → Pages → Source: **GitHub Actions**.
3. Once the first run finishes (Actions tab), set `site_url` in `zensical.toml` to the URL GitHub gives you.
4. Push again so the canonical URL is baked into the build.

## Editing

Markdown files in `docs/`. Names like `index.md` define section landings. The navigation order is set explicitly in `zensical.toml` under `[project] nav`.
