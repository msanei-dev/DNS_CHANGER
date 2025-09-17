<div align="center">
  <h1>DNS_CHANGER</h1>
  <p>DNS Checker / DNS Changer — Electron + Vite + React (TypeScript)</p>
</div>

Overview
--------

This repository is a desktop application scaffold using Electron for the main and preload processes (TypeScript), and Vite + React for the renderer. The project compiles Electron TypeScript files into `dist-electron/` before launching so Electron does not attempt to execute `.ts` sources directly.

Quick start
-----------

Requirements
- Node.js 18+ (LTS recommended)
- npm

Install dependencies:

```powershell
npm install
```

Development (recommended)

1. Start Vite (renderer dev server):

```powershell
npm run dev
```

2. In a second terminal start Electron (this will compile main & preload automatically before launching):

```powershell
npm run start
```

Production build (local test)

```powershell
# Build renderer
npx vite build

# Compile electron main & preload
npm run build:main
npm run build:preload

# Start the app (uses compiled electron files)
npm run start
```

Packaging
---------

The `build` script in `package.json` runs the renderer build, compiles electron sources, then executes `electron-builder`. Configure `electron-builder` settings in `package.json` before releasing.

Important notes
---------------

- Electron cannot execute TypeScript directly. Use the provided build scripts (`build:main`, `build:preload`) so `dist-electron/` contains runnable JS.
- Vite `base` is set to `./` so production asset paths are relative and work with the `file://` protocol in packaged apps.
- Ensure `electron/main.ts` points to the compiled preload file inside `dist-electron/preload/`.

Troubleshooting
---------------

- "Unknown file extension .ts": run `npm run build:main`.
- "ENOENT preload": run `npm run build:preload` and verify `dist-electron/preload/preload.js` exists.
- Renderer white screen or `ERR_FILE_NOT_FOUND`: run `npx vite build` to create `dist` or run `npm run dev` and start Electron while the dev server is running.

Contributing & next steps
-------------------------

If you want, I can add:

- A LICENSE file (MIT by default).
- A GitHub Actions workflow to run `tsc --noEmit` and `npx vite build` on pushes/PRs.
- A convenience script like `npm run dev:electron` that launches the renderer dev server and Electron together.

Tell me which of the above you'd like and I'll add it and push to the remote.
