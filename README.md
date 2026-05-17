# PsyGames Web — ⚠ AUTO-GENERATED OUTPUT

> **🚫 DO NOT EDIT THIS REPO DIRECTLY.**
>
> This repo only hosts the built `dist/` of PsyGames for GitHub Pages serving.
> Every push to `psygames-native/main` overwrites everything here automatically.
> Any manual changes you make will be lost on the next CI run.

## 🏛 Source of truth → [psygames-native](https://github.com/donosov999-ai/psygames-native)

All editing happens there:
1. Clone `donosov999-ai/psygames-native`
2. Edit `frontend/app/games/*.tsx` (or whatever you need)
3. Push to `main`
4. CI rebuilds web + native (Mac/Win/Android) and pushes the web build here
5. GH Pages updates this site within ~1 minute

## Live site

https://donosov999-ai.github.io/psygames-web/

## Why two repos?

- **`psygames-native`** holds React Native (Expo Router) source code + Tauri config + GitHub Actions workflow that builds:
  - macOS arm64 `.app`
  - Windows `.exe` + `.msi`
  - Android signed `.apk`
  - Web `dist/` → pushed here
- **`psygames-web`** (this repo) only stores the static `dist/` so GitHub Pages can serve it. Smaller history, faster fresh clones, no node_modules.

## What's in this repo

```
.
├── index.html, statistics.html, settings.html, ...  ← entry points
├── games/                                          ← one HTML per game
├── _expo/static/js/web/entry-<hash>.js              ← single JS bundle
├── assets/, favicon.ico
├── .nojekyll                                       ← required for GH Pages
└── README.md                                       ← this file (preserved by CI)
```

## Deploy mechanism (for reference)

The CI job in `psygames-native` runs (simplified):

```bash
# 1. Build web with baseUrl=/psygames-web
cd frontend && npx expo export -p web

# 2. Replace this repo's contents (preserves .git, .nojekyll, README.md)
cd psygames-web-target
find . -maxdepth 1 ! -name '.git' ! -name '.nojekyll' ! -name 'README.md' ! -name '.' -exec rm -rf {} +
cp -R ../frontend/dist/* .
touch .nojekyll

# 3. Commit + push
git commit -m "Auto-deploy from psygames-native@<sha>"
git push
```

Token: `PSYGAMES_WEB_DEPLOY_TOKEN` secret in psygames-native repo.

## Manual override (emergency only)

If for some reason you need to push a manual change here (e.g. rollback), know that the **next push to `psygames-native/main` will overwrite it**. So either:
- Pause CI in psygames-native first (disable workflow in Actions UI)
- Or commit your fix to psygames-native instead so it survives

## License

Personal use, ODV999.
