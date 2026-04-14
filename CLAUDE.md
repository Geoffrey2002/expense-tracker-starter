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

Single-page React app (Vite + React 19). No backend — state is in-memory only (no persistence).

### Component tree

```
App
├── Summary          — calculates and displays totalIncome, totalExpenses, balance
├── TransactionForm  — owns form field state; calls onAdd(transaction) prop when submitted
└── TransactionList  — owns filter state (filterType, filterCategory); renders the table
```

`App` is the single source of truth for the `transactions` array. It passes the array down to all three children and provides `handleAdd` to `TransactionForm` via the `onAdd` prop.

The `categories` constant is duplicated in `TransactionForm` and `TransactionList` — a candidate for extraction to a shared file if it ever changes.

### Data model

Each transaction: `id` (number), `description` (string), `amount` (number), `type` (`"income"` | `"expense"`), `category` (string), `date` (ISO date string `YYYY-MM-DD`).

### Styling

Plain CSS in `src/App.css` and `src/index.css` (global resets). No CSS framework. A `.delete-btn` class exists in `App.css` but no delete button is rendered yet.
