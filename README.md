<div align="center">
<img width="1200" height="475" alt="GHBanner" src="https://github.com/user-attachments/assets/0aa67016-6eaf-458a-adb2-6e31a0763ed6" />
</div>

<div align="center">
   <h1>DNS Checker / DNS Changer</h1>
   <p>Electron + Vite + React (TypeScript)</p>
</div>

A small desktop app scaffold using Vite for the renderer and TypeScript for the Electron main & preload processes.

---

## Contents

- `electron/` — Electron sources (`main.ts`, `preload.ts`)
- `dist-electron/` — compiled Electron output (created by build scripts)
- `dist/` — Vite renderer build (created by `npx vite build`)
- Root files: `package.json`, `tsconfig.json`, `vite.config.ts`, app sources (React)

## Quick start

Requirements
- Node.js 18+ (LTS recommended)
- npm

Install:

```powershell
npm install
```

Development (fast iteration)

1) Start the Vite dev server (renderer):

```powershell
npm run dev
```

2) In a second terminal start Electron (it will compile the main & preload before launching):

```powershell
npm run start
```

This setup lets Electron load the dev server for the renderer while you edit React code.

Production build (local testing)

1) Build renderer assets:

```powershell
npx vite build
```

2) Compile Electron files (main & preload):

```powershell
npm run build:main
npm run build:preload
```

3) Launch the packaged app locally (this runs the compile steps automatically then starts Electron):

```powershell
npm run start
```

Packaging

```powershell
# Runs renderer build, compiles electron sources, then electron-builder
npm run build
```

Note: adjust `electron-builder` configuration in `package.json` if you need specific targets/packaging options.

## Important implementation notes

- Electron cannot execute `.ts` files directly. The repo contains `tsconfig.build.json` and npm scripts to compile `electron/*.ts` into `dist-electron/` before launching.
- Vite build `base` is set to `./` so production `dist/index.html` uses relative asset paths and works with the `file://` protocol.
- The main process must point to a compiled preload script in `dist-electron/preload/`. If you rename or reconfigure the preload output, update `electron/main.ts`.

## Troubleshooting

- "Unknown file extension .ts" — run the electron compile step: `npm run build:main`.
- "ENOENT preload" — ensure `npm run build:preload` produced `dist-electron/preload/preload.js` and that `electron/main.ts` points to it.
- White screen / ERR_FILE_NOT_FOUND in renderer — run `npx vite build` (or run `npm run dev` and start Electron while dev server runs).

If you still see issues, paste the exact console or terminal errors and I'll help further.

## Contributing

1. Fork the repo
2. Create a branch for your feature/fix
3. Commit, push, open a PR

## License

Add a `LICENSE` file (MIT, Apache-2.0, or similar) if you want others to use your code.
