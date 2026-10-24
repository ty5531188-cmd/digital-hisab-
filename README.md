# AI Small Business Hisab

Hindi-first (also English) accounting app for Indian small businesses: customers and udhar, suppliers and payables, sales, expenses, monthly report, voice entry. Plain HTML/JS, Supabase for auth and database.

## Files
- `index.html` – the app (Supabase-connected). Deploy this.
- `supabase/migrations/001_core_schema_rls.sql` – tables, constraints, Row Level Security.
- `prototype/hisab-local-only.html` – earlier version, data stays in the browser only.
- `netlify.toml` – Netlify config.

## Setup
1. Supabase: run `supabase/migrations/001_core_schema_rls.sql` (SQL Editor, or `supabase db push`).
2. In `index.html` set `SB_URL` and `SB_KEY` near the top of the script. Use the **publishable** key only. Never put a `service_role` or secret key in this file.
3. Supabase → Authentication → URL Configuration: add your site URL. If "Confirm email" is on, users must confirm before login.
4. Google (Gmail) login: Google Cloud Console → APIs & Services → Credentials → create an OAuth client (Web). Add the Supabase callback URL (shown in Supabase → Authentication → Providers → Google) as an authorized redirect URI. Paste the Client ID and Secret into that Supabase Google provider and enable it. Also add your site URL under Authentication → URL Configuration. Each Google user gets their own private business automatically.
5. Deploy: drag this folder to Netlify, or push to GitHub and connect the repo.

## Known limits
- Saving a credit sale writes the sale and its ledger entry in separate calls, not one atomic transaction. On error the app reloads server data.
- Not built yet: inventory, invoices, PDF/Excel export (CSV only), handwritten scanner, AI advisor, staff roles, multi-business, billing.
