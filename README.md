# AI Small Business Hisab

Hindi-first (also English) accounting app for Indian small businesses: customers and udhar, suppliers and payables, sales, expenses, monthly report, voice entry, and an admin panel. Plain HTML/JS, Supabase for auth and database.

## Files
- `index.html` – the app (Supabase-connected). Deploy this.
- `supabase/migrations/001_core_schema_rls.sql` – tables, constraints, Row Level Security.
- `supabase/migrations/002_admin_panel.sql` – admin table and `admin_overview()` function.
- `prototype/hisab-local-only.html` – earlier version, data stays in the browser only.
- `netlify.toml` – Netlify config.

## Setup
1. Supabase: run the two SQL files in order (SQL Editor, or `supabase db push`).
2. In `index.html` set `SB_URL` and `SB_KEY` near the top of the script. Use the **publishable** key only. Never put a `service_role` or secret key in this file.
3. Supabase → Authentication → URL Configuration: add your site URL. If "Confirm email" is on, users must confirm before login.
4. Make an admin: sign up once, then run the commented `insert into public.admins ...` line at the bottom of `002_admin_panel.sql` with your email.
5. Deploy: drag this folder to Netlify, or push to GitHub and connect the repo.

## Known limits
- Saving a credit sale writes the sale and its ledger entry in separate calls, not one atomic transaction. On error the app reloads server data.
- Not built yet: inventory, invoices, PDF/Excel export (CSV only), handwritten scanner, AI advisor, staff roles, multi-business, billing.
- Admin panel shows summaries and recent activity, polled every 15 seconds (not realtime).
