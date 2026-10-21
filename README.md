# Protein Log

Log protein by meal through the day, against a daily target set from your target weight.

Live at **https://alirghase.github.io/protein-log/**.

## How it works

- **Target:** target weight × grams per kg (1.6–2.2, default 1.8). Protein is set from the weight
  you're heading to, not today's, because extra fat doesn't need feeding with protein. Add your
  height and current weight to see your BMI now and at your target.
- **Logging:** pick a meal (breakfast, lunch, dinner, snacks), then tap a food. Use − and + to change
  the amount (×2 of "Chicken breast, 100 g raw" is 200 g). **Undo** removes the last add.
- **Built-in foods:** staples (oats, protein scoop, protein yoghurt, rice pouch), fish, meat per 100 g
  raw, and a few others. Values are typical UK label figures.
- **Your own foods:** type a name and its protein; it's saved to **My foods** for one-tap adds.
- **Last 7 days:** each day against the target. Tap a day to see or edit it.

## Saving

**Signed in** (email and password), the log is saved online in Supabase and shows up on any device
you sign in on. It shares the [Gym Plan](https://github.com/alirghase/gym-plan) Supabase project, so
one account works for both apps. Row-level security means each account can only read and write its
own rows. The key in `index.html` is Supabase's publishable key, which is public by design. The first
sign-in on a browser moves any log saved there into the account; days already online win.

**Signed out**, the page still works, but the log is saved only in that browser's local storage,
and clearing the browser deletes it.

## Development

One `index.html`: plain HTML, CSS and JavaScript, no build step. `supabase-js` and the fonts load
from CDNs.

The tables (`protein_days`, one row per logged day, and `protein_profile`, one row per account) and
their row rules live with the Gym Plan project, in
[`gym-plan/supabase/migrations`](https://github.com/alirghase/gym-plan/tree/main/supabase/migrations).
