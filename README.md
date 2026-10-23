# Protein Log

Log protein by meal through the day, against a daily target set from your target weight.

Live at **https://alirghase.github.io/protein-log/**.

## How it works

- **Target:** target weight × grams per kg (1.6–2.2, default 1.8). Protein is set from the weight
  you're heading to, not today's, because extra fat doesn't need feeding with protein. Add your
  height and current weight to see your BMI now and at your target.
- **Logging:** pick a meal (breakfast, lunch, dinner, snacks), then tap a food. Use − and + to change
  the amount. **Undo** removes the last add.
- **By weight:** meat asks for grams (type any weight or tap 50–400 g in 50 g steps; each button shows
  its protein) and works out the protein from its per-100 g value. It remembers your last weight for
  each food. In the day's list, type a new weight or nudge it by 50 g.
- **Built-in foods:** staples (oats, protein scoop, protein yoghurt, rice pouch), fish, meat by
  weight (raw), air-fried meat and fish (weighed cooked), and a few others. Values are typical UK label figures.
- **Aldi rice pouches:** the eight Worldwide Foods 250 g pouches, one tap each.
- **Aldi range:** Aldi's salmon, trout, white fish, tuna, mackerel, chicken, turkey, beef and lamb, air-fried
  and weighed cooked (hot smoked fish is ready to eat). Each has quick buttons for 1 or 2 fillets or steaks
  at their typical cooked weight, so you can log without scales; weigh it for an exact figure.
- **Your own foods:** type a name and its protein; it's saved to **My foods** for one-tap adds.
- **Last 7 days:** each day against the target. Tap a day to see or edit it.
- **Example week:** a sample rotation of two main proteins a day (chicken, sardines, white fish and
  red meat), with the day you're viewing highlighted.

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
