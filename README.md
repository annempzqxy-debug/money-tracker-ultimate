# money-tracker-ultimate

# MoneyTracker Ultimate

A personal finance desktop app built with Python and CustomTkinter. Track expenses, set budget limits, monitor saving streaks, manage savings goals, and view spending analytics — all stored locally in a SQLite database.

---

## Features

- **Multi-user authentication** — sign up, log in, and sign out with hashed passwords
- **Expense tracking** — add and delete transactions with flexible date input formats
- **Budget limits** — set daily, weekly, monthly, or yearly spending limits
- **Saving streaks** — automatically tracks consecutive periods spent under budget
- **Streak calendar** — visual month calendar showing successful, current, and failed budget periods
- **Savings goals** — create goals with a target amount, deposit savings, withdraw, and view history
- **Reports & analytics** — bar chart and pie chart with theme-aware colors, filtered by period
- **Summary page** — per-category progress bars filtered by today, week, month, or year
- **Goal status on overview** — overview page shows all savings goals at a glance
- **Custom categories** — add or delete spending categories; custom ones appear in all graphs
- **Profile picture** — upload a profile photo that persists across logout/login sessions
- **Dark / Light / System theme** — switchable from Settings
- **Export report** — save transaction history to a `.txt` file

---

## Pages

| Page | Description |
|---|---|
| Overview | Summary cards, spending chart, recent transactions, goal status |
| Transactions | Full transaction list with search and time filters |
| Summary | Per-category budget progress bars with period filter |
| Goals & Streaks | Savings goals, streak history, and streak calendar |
| Reports | Bar chart and pie chart of spending by period |
| Categories | View, add, and delete spending categories |
| Settings | Profile, budget, notifications, theme, and export |

---

## Requirements

- Python 3.10+
- [CustomTkinter](https://github.com/TomSchimansky/CustomTkinter)
- Matplotlib
- Pillow

Install dependencies:

```bash
pip install customtkinter matplotlib pillow
```

---

## Running the App

```bash
python main.py
```

The app window opens at 1500×900 (minimum 1100×700). A SQLite database file `moneytracker.db` is created automatically in the same folder on first run.

---

## Default Admin Account

A default account is created on first launch:

| Field | Value |
|---|---|
| Username | `admin` |
| Password | `Admin123!` |

Change the password after first login via **Settings → Profile**.

---

## Project Structure

```
├── main.py                     # Entry point
├── app.py                      # Main app class (assembles all mixins)
├── config.py                   # Theme setup and shared constants
├── database.py                 # SQLite setup, queries, streak and budget logic
├── models.py                   # User, Transaction, Expense, Income classes
├── date_utils.py               # Flexible date parsing helpers
├── mixin_base.py               # Base class with shared attribute declarations
│
├── auth_mixin.py               # Login, sign up, reminder prompt, budget setup
├── navigation_mixin.py         # Sidebar, page routing, app initialization
├── dashboard_mixin.py          # Overview and Summary pages
├── transactions_mixin.py       # Transactions page, add/delete, search
├── budget_mixin.py             # Goals & Streaks page, budget progress
├── reports_mixin.py            # Reports page, bar chart, pie chart, calendar
├── settings_mixin.py           # Settings and Categories pages
│
├── moneytracker.db             # SQLite database (auto-created)
├── profile_pics/               # Saved profile pictures (auto-created)
└── app_before_mixin_split.py   # Legacy single-file version (reference only)
```

---

## Architecture

The app uses Python's multiple inheritance (mixin pattern) to split the UI into focused files. `MoneyTrackerUltimate` in `app.py` inherits from all seven mixin classes and `ctk.CTk`, combining them into one window instance. Shared state (current user, budget limit, streak counters, etc.) is declared in `AppMixin` in `mixin_base.py` so Pylance and the runtime can resolve attributes across all mixins.

---

## Changelog

### v2
- Savings goals with deposit, withdraw, and history
- Goal Status card on Overview page replacing the old Budget Status textbox
- Streak calendar with correct period-block coloring (whole week/month turns amber or gray)
- Streak history box and header label stay in sync on Goals & Streaks page
- Returning users skip the budget setup popup on login
- Add/Delete category panels placed side by side in Categories page
- Pie chart uses a bottom legend to eliminate label overlap; figure size increased
- Bar chart grid lines, ₱ amount labels on bars, and theme-aware background colors
- `mixin_base.py` now declares shared attributes for correct Pylance type resolution
- Profile picture persists across logout/login (saved path stored in database)
- Custom categories appear in Reports graphs and Summary progress bars immediately after adding

### v1
- Multi-user login and sign up with SHA-256 password hashing
- Expense tracking with flexible date formats
- Budget limits with daily/weekly/monthly/yearly periods
- Saving streak tracking and streak calendar
- Per-category summary progress bars
- Bar and pie chart reports
- Dark/light/system theme toggle
- Profile picture upload
- Export transactions to `.txt`
