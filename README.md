# Crate Rush

A case-opening game in a single page: open crates, trade up, sell to The Prestige, and stay on the right side of the Black Market.

- `index.html` is the whole game: no build step. Vercel serves it as a static site.
- Accounts and cloud saves use Supabase (email + password). Each account has one row in `public.saves`, protected by row-level security so players can only read and write their own save.
