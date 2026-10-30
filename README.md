# Protein Log

Log protein and calories by meal through the day, against a protein target set from your target
weight and an estimate of what you burn.

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
- **Built-in foods:** staples (oats, honey, protein scoop, protein yoghurt, fruit), tinned fish,
  air-fried chicken breast and Roosters Hot & Spicy chicken tenders (weighed cooked; the tenders have
  half-pack buttons from the label), and a salmon fillet logged by its raw pack weight (474 g
  to start; type any weight). No ready meals. Values are typical UK label figures. Each
  food is listed once: anything in the Aldi range below isn't repeated as a generic item.
- **Calories:** every built-in food shows its calories next to its protein (per serving, or per 100 g
  for foods logged by weight). The day's total sits under the protein total, against an estimate of
  what you burn, with how far under or over you are. Each meal and each logged food shows its calories.
- **Calorie target:** your burn minus 500 (about 0.5 kg of fat a week), the same every day. The bar
  turns orange past it. It's deliberately conservative: it assumes you only eat and walk.
- **Burn estimate:** resting burn (Katch–McArdle from lean mass once the Body section has your waist
  and neck, otherwise Mifflin–St Jeor from weight, height and age) × 1.2 for a desk day, plus walking
  for your average steps beyond the ~5,000 a desk day already covers (default 10,000; about 0.5 kcal
  per kg per km). Gym and sport aren't counted.
- **Real burn (a check only):** once there are 6+ weigh-ins over 14+ days in the last 28, with food
  logged on 80% of those days, the settings show what you actually burn: average calories eaten plus
  the weight lost (a least-squares trend × 7,700 kcal per kg), with your waist change over the same
  days. The target doesn't use it.
- **Usual day:** **Log staples** adds porridge, honey and a scoop at breakfast and yoghurt and a banana
  as snacks; an empty day also offers **Copy the day before**. Undo takes back the whole batch.
- **Aldi rice pouches:** the eight Worldwide Foods 250 g pouches, one tap each.
- **Aldi range:** Aldi's salmon, trout, white fish, tuna, mackerel, chicken, turkey, beef and lamb, air-fried
  and weighed cooked (hot smoked fish is ready to eat). Each has quick buttons for 1 or 2 fillets or steaks
  at their typical cooked weight, so you can log without scales; weigh it for an exact figure.
- **Your own foods:** type a name, its protein and (optionally) its calories; it's saved to **My foods**
  for one-tap adds.
- **Last 7 days:** protein or calories (switch at the top) for each day against its target. Tap a day
  to see or edit it. Below it, the average
  calories over the finished days, how far under or over your burn that is, and what that means in kg
  of fat a week.
- **Body:** a quick weigh-in box (shows the 7-day average against the week before), the waist chart,
  and a small trend line for each tape measurement. Weight is shown as a number, not a chart.
- **Check-in:** **Copy for Claude** copies the last 28 days as plain text (targets, each logged day's
  protein and calories, averages, body measurements and the most-logged foods) to paste into Claude or
  another AI for a summary. Food starts at your first logged day if that's later, so earlier days don't
  count as missed. Nothing is sent anywhere; it only goes to the clipboard.
- **Example week:** a sample rotation of two main proteins a day (chicken, sardines, white fish and
  red meat), with the day you're viewing highlighted.

Add it to your home screen for an app icon (`manifest.webmanifest`).

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

The tables (`protein_days`, one row per logged day, and `protein_profile`, one row per account, which
also holds age and steps a day for the burn estimate) and
their row rules live with the Gym Plan project, in
[`gym-plan/supabase/migrations`](https://github.com/alirghase/gym-plan/tree/main/supabase/migrations).
