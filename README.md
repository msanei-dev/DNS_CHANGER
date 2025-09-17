<div align="center">
  <h1>DNS_CHANGER — DNS Checker / Changer</h1>
  <p>Electron + Vite + React (TypeScript)</p>
</div>

سلام — این مخزن برای اجرای یک اپ دسکتاپ ساخته شده با Electron (برای main/preload) و Vite + React (برای renderer) آماده است.

This repository contains a desktop app scaffold using Electron (TypeScript) for the main and preload processes, and Vite + React for the renderer.

---

### Short quickstart — کوتاه و سریع

1. نصب وابستگی‌ها:

```powershell
npm install
```

2. حالت توسعه (دو ترمینال):

ترمینال ۱ — سرور توسعه رندرر:

```powershell
npm run dev
```

ترمینال ۲ — اجرای Electron (کامپایل main/preload قبل از اجرا):

```powershell
npm run start
```

3. ساخت تولیدی (برای تست محلی):

```powershell
npx vite build
npm run build:main
npm run build:preload
npm run start
```

---

### Why these custom scripts? — چرا این تغییرات لازم بود

- Electron cannot run `.ts` files directly. We compile `electron/*.ts` into `dist-electron/` before launching.
- Vite `base` is set to `./` so production `dist/index.html` uses relative asset paths and works with `file://`.
- The main process must load the compiled preload script (see `electron/main.ts`), not the `.ts` source.

### Troubleshooting — اشکال‌زدایی سریع

- Unknown file extension ".ts": اجرای `npm run build:main` و `npm run build:preload` حل می‌کند.
- ENOENT preload: مطمئن شوید `dist-electron/preload/preload.js` وجود دارد و `main.ts` به آن اشاره می‌کند.
- White screen / ERR_FILE_NOT_FOUND: یا `npx vite build` را اجرا کنید یا `npm run dev` را فعال کنید و سپس Electron را اجرا کنید.

---

If you want, I can also:

- Add an `MIT` license file.
- Add a GitHub Action to run `tsc --noEmit` and `npx vite build` on PRs.
- Normalize preload output name and simplify `main.ts` logic.

Tell me which of those you'd like me to add, and I'll commit and push the change.
