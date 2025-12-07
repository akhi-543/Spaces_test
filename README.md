# Release_test
Spaces-version(1.0.0)
# Spaces

Spaces is a keyboard-first, Electron + Vite overlay for organizing and quickly launching links, local files, and small notes grouped into "Spaces". It focuses on speed and minimal distraction with keyboard navigation, quick creation, and a clean glassmorphism UI.

## Features
- Create and manage named Spaces to group links, files, and notes
- Quick global hotkey to open the overlay (configurable)
- Keyboard-first navigation and item management (arrows, Enter, Delete)
- Add items by pasting URLs, typing notes, or attaching local files
- Global `@all` search across all Spaces
- Recycle Bin for soft-deleted Spaces
- Lightweight persistent storage using `electron-store`

## Quick Start (dev)
Requirements:
- Node.js 18+ (or compatible LTS)
- npm

Install and run in development:

```bash
npm install
npm run dev
```

Open the app UI at the local dev server shown by Vite (usually `http://localhost:5173`). The Electron main process integration runs when using the Electron dev task (see package.json scripts).

## Build / Package
Build the web assets and then package the Electron app (project includes platform build scripts):

```bash
npm run build      # builds the front-end (Vite)
npm run dist:win   # example: build Windows distributable (configured in repo)
```

Adjust packaging commands in `package.json` / `electron-builder` config to match target platforms.

## Keyboard & Commands (overview)
- Global hotkey: `Shift + Space` (configurable in Settings)
- Search bar: type to search spaces or items
- Commands: type `@` to show commands, including `@all`, `@recycle`, `@settings`, `@file`
- While inside a Space:
  - `Enter` — open selected item (or restore when in Recycle Bin)
  - `Shift + Enter` — force-add typed content as a new item
  - `Delete` — remove selected Space (moves to Recycle Bin) or permanently delete from Recycle Bin
  - `Ctrl + Enter` — "Launch All" (open all URLs/files in the current view)
- Add items by:
  - Pasting a URL (auto-fetches title metadata when available)
  - Typing text and pressing `Enter` (creates a note)
  - Using the Add File button or `@file` command to pick local files/folders

## Storage
Spaces and deleted spaces are persisted using `electron-store` (see `electron/main.js`). Settings (theme, hotkey) are also persisted.

## Project Structure (important files)
- `electron/` — Electron main & preload files
  - `electron/main.js` — app lifecycle, global shortcut registration, IPC handlers
  - `electron/preload.js` — secure IPC bridge
- `src/` — React UI
  - `src/App.jsx` — main controller and top-level routing between LaunchPad / SpaceView / Settings
  - `src/components/LaunchPad.jsx` — spaces grid and creation UI
  - `src/components/SpaceView.jsx` — items list/grid inside a space, add/launch logic
  - `src/components/NoteEditor.jsx` — note editing/preview
  - `src/components/Settings.jsx` — theme / hotkey UI
- `package.json` — scripts and dependencies
- `tailwind.config.js` — design tokens and Tailwind config

## Contributing
- Run `npm install` and `npm run dev` to start developing.
- Follow the existing style (Tailwind + utility classes). Keep UI changes minimal and consistent.
- For Electron changes, ensure IPC handlers are secure and context-isolation is enabled.

## Troubleshooting
- If hotkey doesn't register, check global shortcut conflicts on your OS and update the hotkey in Settings or from `electron-store` defaults.
- If file dialogs or path operations fail, confirm the app has necessary permissions and the path exists.

## License
Include a license file if you plan to open-source this project. By default, none is provided in this repo.

---

If you want, I can:
- Add this README to the repo (I already created it at `README.md`).
- Add example screenshots and a short GIF of the overlay in use.
- Add packaging specifics for macOS / Linux.
