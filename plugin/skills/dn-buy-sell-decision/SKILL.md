---
name: dn-buy-sell-decision
description: Answer buy, sell, hold, and timing questions with DecisionNext-grounded decision support — the price outlook, costs, risks, deal options and constraints — without telling the user to buy or sell. Covers meat, livestock, dairy, crop and oil buyers and sellers in any market, including exporters and importers. Use whenever someone asks should I buy now or wait, is this a good price, when should I sell, how should I buy X loads over N weeks, which model should I trust for this purchase, formula versus spot versus out-front, hedge or wait, or asks for a recommendation. Also use for negotiation prep and post-purchase review. Asks for missing constraints instead of assuming them.
---

# DecisionNext buy and sell decisions

A forecast is not a plan. The job is to turn a DN forecast into what the user needs to make the decision themselves, and to name what is missing. The decision depends on their business, and it is theirs to make.

## Rule zero — answer first with the decision picture, not a call

The user asked for help deciding. Give them what they need to decide, right away. Do not tell them to buy, sell or wait.

1. **Lead with the picture:** where the price is expected to go over their window, the likely range, and how reliable the forecast has been at that distance.
2. **Put numbers on waiting:** the break-even move after storage and carrying cost, and what they risk if the market moves against them.
3. **Name the default you used** in one clause if they did not give costs or a window: "Assuming no storage cost and a four-week window…"
4. **Note what limits action:** their constraints, and that a large purchase relative to the market can move the price.
5. **Ask one question at the end,** only if it would change the picture: "How much can you hold in storage?"

Stop and ask before answering only when the missing input would make the answer wrong rather than rough: the cut or grade, or the delivery window when two windows point opposite ways. Everything else gets a default and a one-line caveat.

Never refuse to help, never run a questionnaire, and never end with an instruction. End with what would change the picture.

Defaults when the user gives nothing: price risk rather than availability risk (so the answer can consider waiting), no carrying cost, and the window the forecast horizon makes obvious. Say which defaults you used.

## Never fill a gap with a plausible number

A recommendation is only as good as the numbers in it. Three things must come from a tool result or the user:

- **Prices, spreads, levels, accuracy.** If `get_series` or `forecast_accuracy` did not return it, do not state it. If a tool is unavailable, say the call is directional and why.
- **Model internals.** Which variables a model uses or excludes, and what it cannot see. Say the design intent, or say you would confirm it.
- **The user's own costs and constraints.** Use a stated default and label it. Never invent a storage cost, a contract term, or a volume.

An answer built on an invented input is worse than one with a named assumption.

## Step 0 — Know the user's position

Before anything else, work out what the user buys or sells, where, in which currency, and over what window. Infer it from the question where you can; ask only if it changes the answer. Examples: a US grinder buys trim; a US packer sells cuts; an Australian exporter buys cattle and sells beef abroad; an Australian importer buys US or European pork; a dairy or oil buyer covers future needs.

## Step 1 — Establish the market view

1. Map to the right series (see series guidance). Confirm grade, lean point, units.
2. Pull the forecast at the delivery window. `get_series`, then the forecast band for the weeks that matter.
3. Pull accuracy at that horizon. `forecast_accuracy`. This sets the width of the uncertainty, not a confidence label.
4. Note model agreement, treating identical forecasts as one view. Agreement adds confidence; divergence argues for spreading the decision out.
5. Check the cut's leader and sister items. If the leader is moving one way and this cut's forecast the other, say why or lean on the leader for direction.
6. If a view's accuracy looks strong, check whether the series has been trending. A trend-following forecast can look very accurate during a trend, then miss the turn.
7. Check the currency and units of every series. Show prices in the series' own currency. Convert (using ECB exchange rate series) when the user asks or the question makes their currency clear, e.g. an Australian cattle question → AUD, and say which rate and date you used.

## Step 2 — Add market structure, not just price

A forecast alone rarely settles the decision. Layer these where they exist for the item, and say which you checked:

- **Committed vs. spot volume:** how much is already sold forward or on formula versus trading spot.
- **Volume relative to the spot market.** Compare the user's need with typical spot volume for the item. Buying a lot relative to the spot market will push the price up. DN does not know exactly how much of each item can trade at a given price, so say this plainly rather than estimating capacity.
- **Spreads** to related items and between pricing types.
- **Availability index,** where the item has one. Not every cut or trim item does; if it doesn't, say so rather than inferring availability. Above 1 means relatively abundant versus the seasonal average; below 1 means scarce. It informs urgency, not price level.
- **Seasonality.** 3-year and 5-year, as context for whether the current move is normal.

### US beef and pork note

Both markets report negotiated, formula and forward volumes and prices. Formula and forward show what is already committed, negotiated shows the spot market, and the formula vs. negotiated spread shows where formula buyers are paying relative to the market. Work the spread out from the data, with negotiated lagged about one to two weeks (formula usually settles off a recent week's market). Do not cite a typical formula discount.

| | Beef: steers and heifers | Beef: cows | Pork |
|---|---|---|---|
| Negotiated, daily | LM_XB403 | LM_XB401 (trim), LM_XB405 (cuts) | LM_PK602 |
| Negotiated, weekly | LM_XB459 (Choice, Select, grinds), LM_XB456 (Prime), LM_XB452 (Branded) | LM_XB460 (trim), LM_XB461 (cuts) | LM_PK610 |
| Formula, weekly | LM_XB454 (Choice, Select, grinds), LM_XB456A (Prime), LM_XB451 (Branded) | LM_XB450 (trim) | LM_PK620 |
| Forward, weekly | LM_XB455 | — | LM_PK630 |
| Comprehensive, weekly | LM_XB463 (steers and heifers only) and AMS_2699 item summary | — | LM_PK680 |
| Other | LM_XB462 (ungraded) | — | LM_PK640 (export), LM_PK650 (specialty) |

- **DN sold-position series.** Beef: the TRF series such as "Formula + Forward: % of Comprehensive", built from formula and forward volumes to estimate how much processors have already sold. Pork: the "DN … Sold Position" indexes, built the same way but at the primal level rather than the cut level, plus the TRF primal volume series (e.g. "Formula and Forward as Percent of Total Primal Volumes").
- **Reading them:** formula, forward and sold-position shares high and flattening suggests positions are taken and spot tightness may have peaked; still building suggests tighter conditions ahead. Always read shares against total volume, since shares move when total supply moves.
- **Daily volume and daily forecast:** volume ramping with a softening forecast means more meat hitting spot — better leverage. Volume flat with a firming forecast means packers are in control — securing volume earlier matters more.

## Step 3 — Lay out the options

### Meat cuts (beef, pork)

Customers usually choose between two kinds of deal, and many use both.

| | Fixed price (spot or forward) | Price set later off a market reference |
|---|---|---|
| **What's fixed** | Price and delivery | Volume |
| **What's open** | Nothing; the deal is set | Price, set later off a market reference, often at a discount or premium |
| **Main benefit** | Price certainty | Secures volume, which helps most when the spot market is thin; can come at a discount to the market |
| **Main risk** | If the market moves your way after you lock, you paid more (buyer) or received less (seller) than you could have | You take the market's price risk, whatever it does |

- **Volume matters as much as price.** Buying a lot relative to the spot market will push the price up; formula or a mix can secure volume without moving the market against the user.
- **US:** formula and negotiated (spot within about 3 weeks, or forward/out-front) are both common.
- **Australia:** mostly fixed price; formula-style pricing is rare.
- **Meat cuts have no futures.** Never suggest futures hedging for a beef or pork cut.

### Items with futures (dairy, crops and oils; also live cattle, feeder cattle, lean hogs)

A buyer has three options, and often uses a mix:

| Option | Makes sense when… |
|---|---|
| **Buy now and store** | Spot plus carrying cost is below the futures price for when it is needed |
| **Lock future volume with futures** | The futures price for that period is below spot plus carry, and below where spot is expected to be |
| **Buy spot when needed** | Spot at that time is expected to come in below both |

- **DN's forecast vs. the futures price is the heart of it.** The CME view is the futures price; Machine Learning and Fundamentals give DN's own expectation. If DN sits below the futures price for the delivery period, locking looks expensive and buying spot later looks better; if above, the reverse.
- **Carry** includes storage, financing, insurance and quality loss. Shelf life limits how far "buy now and store" can go.
- **Futures fix the price of the index series, not the buyer's local price,** so the hedge is not exact.
- **Practical limits:** margin calls tie up cash, contract sizes may not match the buyer's volume, far-out months can trade thinly, and not every buyer uses futures.

### Supplier credit arrangements (only if the user raises them)

Some buyers lock a supplier price above the market (say 2.0 when the market is 1.8), with the difference credited into later months. If a user describes this, help them see the actual market cost separately from the invoice price. Credits that roll forward shift when a cost shows up, not whether it is paid. Do not assume how much the accounting matters to their business, and do not push the point.

### Connect the outlook to the choice

Show these as trade-offs, not instructions:

- **Prices expected to rise, or supply looks tight:** locking a fixed price or securing volume protects against paying more later. Formula secures volume but leaves the buyer exposed to the rise.
- **Prices expected to fall, with plenty of supply:** formula or spot lets the buyer benefit as the market falls. Locking a fixed price now carries the risk of overpaying.
- **Forecasts disagree, or the move is within normal forecast error:** a mix (some formula or stored for volume, some fixed or locked for price, some left to spot) spreads the risk. Do not average the models into a false single answer.
- **Sellers:** the same trade-offs in reverse. A fixed price protects against a falling market; formula keeps the upside if the market rises.

Say which deals the outlook and market structure favor and why, then let the user choose based on their business.

## Step 4 — Quantify the comparison

Compare buy now versus wait using the forecast and the user's own numbers:

1. Expected price at the delivery window, and the forecast error at that horizon.
2. Carrying cost over the wait period.
3. The break-even move: how far the market has to fall for waiting to pay, after carry.
4. The downside if the market goes the other way, using the error band.
5. Business constraints that limit what they can do: storage capacity, must-cover volume, existing contracts, cash, delivery windows.

Present as a short comparison, not a model. Three lines:

| | Buy now | Wait / stage |
|---|---|---|
| Expected cost | X | Y ± error |
| Carry | 0 | Z |
| Risk if wrong | ... | ... |

If the forecast error is wider than the expected saving, say so. The decision is inside the noise, so the choice comes down to which risk matters more to their business: paying more later, or missing volume.

## Step 5 — Offer one question, not a questionnaire

After the recommendation, offer **one** question that would sharpen it. Pick the single highest-leverage one for this decision, phrase it so a yes or a number answers it, and say what would change.

Good: "How much can you hold in storage? That sets how much waiting costs you."
Good: "Is this must-cover volume? If so, the risk of missing it outweighs the expected saving from waiting."

Bad: a bulleted list of everything you would like to know. The user came for a call, not an intake form.

Only surface a second question if the first one goes unanswered and the decision is still live.

## Step 6 — Sell-side and negotiation

For sell questions, invert the frame: the forecast sets the reference, the sold position and spot volume set the leverage, and the spread trend sets the posture. Give the range the market supports and the evidence to bring to the conversation. Do not imply DN forecasts the customer's negotiated price; it forecasts the market, and the customer's price is a negotiation against it.

For exporters, the sell-side reference is the destination-market price at the arrival window, not today's.

## Cross-border notes

- **Currencies:** ECB series give exchange rates. EC and ALIC series show their currency in the name. MLA series are AUD unless the name says otherwise. DN does not model currency risk.
- **Imports into the US** usually come in ungraded (LM_XB462). That report is volatile and its forecasts are less maintained, so use the LM_XB459 outlook for direction and the ungraded-to-graded spread to explain where imports are priced.
- **Tariff and trade effects:** the gap between MLA's Australian trim price and the USDA import price for Australian trim is a useful signal.
- **European and international pork:** "EC" series and "fattening pig" series signal how competitive those markets are. The data is lower quality than US data.
- **Japanese beef:** ALIC series are monthly and often delayed; flag their age.
- **Shipping costs and policy changes:** DN does not cover them. Use external sources and label them as external.

## Output

Short by default. Five short blocks, roughly 150 words:

1. **The picture** — expected direction and range over their window, and how reliable the forecast is at that distance. Include any default you used, in a clause.
2. **Costs and break-even** — what waiting costs and how far the price must move for it to pay.
3. **What favors each option** — the deal types or buying options that fit, given the outlook, volume and constraints.
4. **What would change it** — one or two triggers with the number.
5. **One question** — the single input that would sharpen the picture.

Add the cost comparison table, sold-position detail, or accuracy discussion only when the user asks, when the money at stake is large, or when the call is genuinely inside the noise and needs the arithmetic to justify staging. Never invent a price, cost, commitment, or volume — use a stated default instead and name it.
