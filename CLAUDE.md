# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Commands

```bash
npm install       # install dependencies
npm run dev       # start dev server at http://localhost:5173
npm run build     # production build
npm run lint      # run ESLint
npm run preview   # preview production build
```

No test suite is configured.

## Architecture

This is a single-page React app (Vite + React 19) with all logic in `src/App.jsx`. There is no backend — state is in-memory only (no persistence).

**Known intentional issues (part of a course):**
- Bug: `amount` is stored as a string, so `totalIncome` and `totalExpenses` use string concatenation instead of numeric addition. Fix: parse amount to float when creating a transaction or when reducing.
- "Freelance Work" (id: 4) is typed as `"expense"` but categorized as `"salary"` — intentionally inconsistent seed data.
- No delete functionality in the UI (`.delete-btn` CSS class exists but no button is rendered).

**Data model** — each transaction has: `id`, `description`, `amount` (string), `type` (`"income"` | `"expense"`), `category` (one of the `categories` array), `date` (ISO date string).

**Styling** is plain CSS in `src/App.css` and `src/index.css` (global resets). No CSS framework.
