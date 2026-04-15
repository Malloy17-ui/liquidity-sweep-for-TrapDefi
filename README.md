malloy — liquidity sweep v2
operator manual · @TrapDefi · BTC 1–3m

install (60 seconds)

open TradingView, pull up your BTC chart, set timeframe to 1m or 3m
bottom panel → Pine Editor
paste the full .pine file in, hit Save (name it whatever)
hit Add to chart
chart loads with pool lines + dashboard top-right. you're live.

if you want it on every BTC chart by default: right-click the indicator name → Apply Indicators to Entire Layout or favorite it for one-click add.

what you're looking at
three things on the chart:

dotted gray lines — cold pools. lone pivots. tracked but won't fire alerts.
solid red/green lines — armed pools. clustered liquidity (equal highs/lows). these are the ones that matter.
labels with stars — fired signals. SWEEP = liquidity was taken. SHORT/LONG = reclaim entry trigger.

dashboard (top-right):
MALLOY · sweep v2     BTCUSDT
regime                ACTIVE
ATR(14)               142.30
↑ pool above          67,890.0  (1.24 ATR)  ×3
↓ pool below          66,420.0  (0.87 ATR)  ×2
armed pools           4 ↑   3 ↓
read it like this:

regime — ACTIVE = trade. CHOP = sit down, signals are unreliable here, this is the no-trade zone you asked for.
pool above/below — nearest armed pool, how far away in ATR units, and how many pivots are clustered (×3 = triple-tap, premium).
armed pools — total loaded liquidity each side. high count = chart is primed.


reading signals
every signal label has a star rating:

★ — minimum quality. armed pool got swept. that's it.
★★ — armed pool with 3+ cluster OR strong volume + depth. better.
★★★ — both. the rare ones. premium.

SWEEP HI ★★ means: a clustered high-side pool just got wicked through and price closed back inside, on above-average volume. the liquidity is taken. now you wait for the reclaim.
↓ SHORT ★★ means: within 5 bars of a sweep high, a momentum bear bar just closed back below the pool. that's the entry trigger. (LONG works the same way, mirrored.)
chop downgrade: if regime = CHOP, all stars get reduced by 1 and signals render in gray. if you're seeing gray labels, the chart is telling you to skip.

the workflow

graze the chart. glance at dashboard.
regime CHOP? close the tab. come back later.
regime ACTIVE + armed pool nearby (< 1 ATR)? sit down. price is hunting it.
sweep label fires. liquidity is taken. don't enter yet.
reclaim label fires within ~5 bars. that's your entry. or skip it if quality < your threshold.
no reclaim within 5 bars? skip. the sweep was just a poke, not a reversal setup.


settings — what to actually tune
most defaults are dialed for BTC 1–3m. four knobs you'll touch:
1 · pool detection → min cluster size to arm pool

2 (default) — standard equal H/L. fires often.
3 — only triple-taps arm. way fewer signals, much higher quality.
start at 2. if you're getting too much noise after a week, push to 3.

2 · sweep quality → require volume confirmation

on (default) — sweep bar must trade 1.3× avg volume.
off — fires on any depth/reclaim regardless of volume.
leave on for BTC. crypto sweeps without volume are usually fakes.

4 · regime filter → chop ATR percentile threshold

0.30 (default) — bottom 30% of recent ATR = CHOP.
raise to 0.40 if you want the chop filter to be more aggressive (more chop classification, fewer signals).
lower to 0.20 if it's calling chop when you think it's fine.

6 · alerts → min quality stars for alert

1 (default) — every signal alerts.
2 — only ★★ and ★★★. recommended once you've got a feel for it.
3 — premium only. very few alerts, very high quality.


setting up alerts

right-click the chart → Add alert
condition: malloy — liquidity sweep v2
pick which event to alert on:

the four alertcondition options (Sweep High, Sweep Low, Reclaim Short, Reclaim Long) — TV's native dialog
OR select any alert() function call to fire on every quality-gated signal at once with the rich payload (recommended)


set notifications: phone push, email, whatever
expiration: Open-ended (paid TV plan) or set max
save

recommended setup: one alert with "any alert() function call" + min stars set to 2 in indicator settings. you'll get pinged on the good stuff with full context in the message, no spam.

troubleshooting
too many signals, getting noisy

bump min cluster size to 3
bump min stars for alert to 2
raise volume × threshold to 1.5

too quiet, missing setups

drop equal H/L tolerance to 0.15 ATR
drop volume × threshold to 1.2
turn off chop filter temporarily to see what it's muting

dashboard says CHOP but chart looks fine to me

raise chop threshold to 0.20 (less aggressive)
or just trust it and move on — it's flagging that recent ATR is low relative to history, which is when sweep setups statistically fail more

labels clipping off screen on phone

label size → large
or zoom out one notch

lines cluttering the chart

turn off show un-armed (cold) pools — only armed lines render
lower max active pools per side to 10

reclaim signal never fires

widen reclaim window from 5 to 8 bars
or drop momentum bar size threshold from 0.3 to 0.2 ATR


what this indicator is and isn't
is responsible for: detecting clustered liquidity pools, marking sweeps with quality context, firing reclaim entry triggers, gating signals by regime.
is not responsible for: position sizing, stop placement, take-profits, holding through the move, or any outcome that follows from your decisions after a signal fires.
the operator is the variable.

revisions

2 revisions included within 14 days
bug reports, parameter tuning, label/color tweaks, alert tuning — all count as revisions
new signal logic, added detection types, HTF bias layers — that's new scope, separate quote

DM me with anything. screenshots help.
