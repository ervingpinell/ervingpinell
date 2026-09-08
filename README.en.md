<div align="center">

### [🇪🇸 Español](https://github.com/ervingpinell/ervingpinell/blob/main/README.md) · 🇬🇧 English

</div>

# Hi, I'm Erving

Developer by profession, gamer by decision.

I work from Costa Rica, mostly with **Laravel, PHP and PostgreSQL**.

Before writing code I worked as a front-desk receptionist in tourism, dealing
with guests in Spanish and English every day. That's where I come from, and it's
why the software I build looks so much like a front desk: bookings, payments,
invoices and people waiting for an answer.

I don't have a degree hanging on the wall — I finished the coursework but never
completed the community-service requirement — so what I know I learned building
things somebody had to use the next morning. I'm still at it: reading the docs,
breaking things locally, and leaning on AI when it helps, without handing over
the part where I actually understand what I'm writing.

---

## PURAPP

**[purappcr.com](https://purappcr.com)** — live:
**[greenvacationscr.com](https://greenvacationscr.com)** ·
**[lutantravelcr.com](https://lutantravelcr.com)**

An ERP and booking engine for tour operators in Costa Rica. It isn't a booking
site with an admin panel bolted on: it covers a tour company's whole operation —
from the moment a customer lands on the website to the moment the tax authority
accepts the invoice — on a multi-company platform where every client runs on its
own deployment and its own database.

Each company gets its public site in **five languages** (Spanish, English,
French, German and Portuguese) with `hreflang`, and its back office behind it.

**Status:** over a year of work and still under active development. Companies
operate on the platform every day while modules keep being added. The **Viator
and GetYourGuide connections are live**: the agencies query availability and
create bookings against our API, and those bookings land in the same panel as
the ones from the website.

<details>
<summary><b>Modules</b></summary>

<br>

| Module | What it handles |
|---|---|
| **Bookings** | Cart and online payment, payment links, standalone charges, promo codes, manually agreed prices, and editing a booking with balance collection. |
| **Sales channels** | Viator and GetYourGuide connected supplier-side: availability, booking, amendment and cancellation, with outbound notices back to the agency. |
| **Pricing** | Rates by season and party size, retail price versus net price, partner commissions with percentage changes by date, and taxes included or added on depending on the agreement. |
| **E-invoicing** | Filing with the Costa Rican tax authority (v4.4): invoice, ticket, credit note, purchase invoice and receiver message. XAdES-EPES signing with the client's own certificate, validation against the official schemas, and control of the document key and sequence. |
| **Operations** | Daily departure list, assignment of guide, driver and vehicle, field check-in, appointments, incidents and logs. |
| **Tracking** | Live GPS through Traccar, with estimated arrival times and pickup-point matching when the agency sends it as free text. |
| **Transfers** | Point-to-point search: it places the origin on the map, resolves it against zones and areas, and builds the price per leg with whatever surcharges apply. |
| **Point of sale** | Tables, orders, modifiers, kitchen tickets, cash open and close. Simplified or standard tax regime, each with its own tax setup. |
| **Accounting** | A single source of truth for income and expenses. Supplier invoices imported straight from their XML, receivables and payables, and a payment file for the bank. |
| **Inventory and purchasing** | Catalog, recipes and ingredients, stock movements, purchase orders and waste. |
| **HR and payroll** | Payroll with Costa Rican social charges, job openings, candidates, interviews, absences and severance. |
| **Messaging** | Per-booking chat with inbound and outbound email threaded together, templates in all five languages, and automatic translation on creation. |
| **Reviews** | Sync with Google and Viator, moderation and review requests. |
| **Public site** | Home page per company, catalog, search-engine optimization, sitemap, and branding — name, logo, colors, social links — resolved from the database instead of hardcoded. |

</details>

<details>
<summary><b>Technical details</b></summary>

<br>

- **Multi-company, never a shared database.** Every client has its own database.
  That isn't purism: tax records and the key their invoices are signed with live
  in there. The server is shared, the data isn't.
- **The electronic signature, written by hand.** XAdES-EPES in PHP, no library
  in between: if the XML comes out badly signed, the tax authority rejects it
  and there is no invoice. It's validated against the official schemas before
  being sent, with one detail that took a while to find — an unsigned XML
  reports a false "missing node", so the validator inserts a stub signature to
  avoid fooling itself.
- **One accounting truth.** Income can arrive through a booking, a standalone
  charge or the point of sale, and all three can refer to the same money. It all
  goes through a single service that subtracts whatever was already counted
  elsewhere; otherwise the same amount shows up three times in the monthly
  report.
- **A mobile app that doesn't invent data.** With signal, the device forwards the
  operation to the server instead of running it on its own; without signal, it
  stores a pending entry and sends it once the connection is back. Payments and
  tax documents are never resolved offline.
- **Email through the Microsoft Graph API**, queued with Horizon, and customer
  replies come back into the chat thread of their booking.
- **Around 2,400 automated tests** covering bookings, pricing, taxes, tax filing
  and the agency contracts.

</details>

`Laravel 12` · `PHP 8.3` · `PostgreSQL` · `Redis / Horizon` · `Vue` · `Alpine.js`
· `Bootstrap` · `NativePHP` · `Stripe` · `PayPal` · `Traccar` · `DigitalOcean` + `Forge`

> Private codebase, in development since May 2025. To give a sense of size:
> about 185,000 lines of PHP, 180 models, 660 migrations and 130 console
> commands.

---

## Passiflora Massages

**[passifloramassages.com](https://passifloramassages.com)**

A site for a massage service in La Fortuna. Bilingual Spanish/English and built
for the phone: guests book from their handset while they're travelling.

Plain HTML, CSS and JavaScript — no build step, no framework, about 1,200 lines
in total — served as static files. Switching languages is one attribute per
string, and booking ends in WhatsApp with the message already written, which is
where the business actually replies.

It loads fast even on hotel wifi, which was the whole point.

`Custom site` · `Bilingual` · `Bookings`

---

## BabyShower Play

**[babyshowerplay.com](https://babyshowerplay.com)**

Ten games to liven up a baby shower, played by every guest at once from their own
phone. The host opens a room, shares a code, and everyone else joins from the
browser: nothing to install, no accounts to create.

It came out of a real problem: my girlfriend offered to run the games at a baby
shower and ran out of time to organize them.

<details>
<summary><b>Technical details</b></summary>

<br>

- **No browser dependencies.** HTML, CSS and JavaScript served as they are: no
  build, no framework, no `node_modules`. The page opens before a framework
  would have finished booting.
- **Shared state over WebSocket.** Fifteen phones watching the same scoreboard
  update live, with the clock synced across devices — every phone's clock is off
  by a little and that broke the countdown.
- **Deterministic puzzles.** Each room has a seed, and the word search, the
  crossword and the bingo cards all come from it: everyone plays the same board
  without the server having to send it.
- **Server-side validation.** Bingo is called against what was actually drawn and
  the card is rebuilt on the server, so marking extra squares gets you nowhere.
- **Genuinely bilingual.** Menus follow the phone's language and the games follow
  the room's; otherwise half the party would be playing a different puzzle.
- **Nine test suites**, including load tests and full end-to-end runs against a
  real server.

</details>

`Node.js` · `WebSocket` · `PWA` · `Capacitor`

---

## Contact

- **GitHub** — [@ervingpinell](https://github.com/ervingpinell)
- **Email** — erving@purappcr.com
