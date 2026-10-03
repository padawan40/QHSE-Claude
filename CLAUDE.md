# CLAUDE.md — 7AS QHSE Audit v2

Offline-first QHSE audit tool for 7AS Consulting. Runs entirely client-side — no backend, data lives in the browser (IndexedDB via Dexie).

## Commands (npm)

```bash
npm run dev        # vite dev server
npm run build      # tsc && vite build — build MUST pass before declaring done
npm run preview
```

No test suite. `npm run build` (which includes `tsc`) is the verification gate.

## Stack

- Vite + React 18 + TypeScript, React Router 6
- **State**: Zustand (`src/store/`)
- **Persistence**: Dexie / IndexedDB (`src/db/`) — offline-first, no server calls
- **Exports**: xlsx (Excel), jspdf + jspdf-autotable (PDF), docx (Word) — in `src/utils/`
- Charts: Recharts. Icons: lucide-react.

## Structure

```
src/
  App.tsx, main.tsx
  components/   # UI
  data/         # static audit reference data (norms, checklists)
  db/           # Dexie schema + queries
  store/        # Zustand stores
  types/        # shared TS types
  utils/        # export generators (PDF/Excel/Word)
```

## Rules

- **No backend and no data network calls** — the app must work offline. Known exception: Google Fonts are loaded from `index.html` (self-host them to make this fully true).
- Dexie schema changes require a version bump in the Dexie DB definition; never mutate an existing version's schema.
- UI and generated documents (PDF/Word/Excel) are in **French** — 7AS is a French QHSE consulting brand.
- Keep export layouts consistent: check the existing generators in `src/utils/` before changing PDF/Excel formatting.
