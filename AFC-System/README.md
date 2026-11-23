# AFC System — Automated Fare Collection & Access Control

A complete **front-end prototype** for an automated railway ticketing and fare
management platform, built for **BIC 21203** as a five-member group project.

The prototype simulates the full revenue path of a rail network: a passenger
registers and loads a wallet, a travel medium is validated, a gate opens or
denies access, a distance-based fare is settled, and every transaction is
reconciled the next day by a central clearing house.

---

## 1. Running the prototype

The project is a static site and needs no build step.

**Via XAMPP (recommended — matches the assessment criteria for localhost deployment)**

1. Start **Apache** from the XAMPP Control Panel.
2. Confirm the folder sits at:
   `C:\xampp\htdocs\Project_ATS\Source Code\AFC-System`
3. Open:
   `http://localhost/Project_ATS/Source%20Code/AFC-System/index.html`

**Without a server**

Open `index.html` directly in any modern browser. All links are relative, so the
prototype works from the file system as well.

---

## 2. Technology stack

| Constraint | Status |
|---|---|
| HTML5 + CSS3 only | ✅ |
| No JavaScript (no `<script>`, no inline handlers, no `javascript:` URLs) | ✅ |
| No Bootstrap / Tailwind / jQuery / React / Vue / Angular | ✅ |
| No external CSS or JS libraries | ✅ |
| No CDN dependencies | ✅ |
| No external icon library (icons are inline SVG) | ✅ |
| All CSS in one external stylesheet | ✅ `assets/css/styles.css` |
| Responsive (desktop, laptop, tablet, mobile) | ✅ 12 media queries, 360 px → 1440 px+ |

Pseudo-classes (`:hover`, `:focus-visible`, `:active`) and native form controls
provide all interaction. There is no client-side logic anywhere in the build.

---

## 3. Folder structure

```text
AFC-System/
├── index.html                     Module index / landing page
├── README.md
├── pages/
│   ├── login.html                 M1 — Passenger sign-in
│   ├── register.html              M1 — Passenger registration
│   ├── passenger-dashboard.html   M1 — Passenger dashboard
│   ├── my-tickets.html            M1 — Issued tickets
│   ├── wallet.html                M1 — Wallet & top-up
│   ├── topup-history.html         M1 — Top-up transaction history
│   ├── passenger-ticket.html      M2 — Ticket with QR preview
│   ├── media-processing.html      M2 — Ticket validation console
│   ├── gate-control.html          M3 — Entry/exit gates + activity log
│   ├── station-management.html    M4 — Station register
│   ├── fare-management.html       M4 — Fare rules
│   ├── fare-calculation.html      M4 — Fare breakdown + settlement
│   ├── clearing-house.html        M5 — Clearing house dashboard
│   ├── transactions.html          M5 — Fare transaction register
│   └── reconciliation.html        M5 — Settlement reconciliation
└── assets/
    ├── css/
    │   └── styles.css             Single shared stylesheet (23 sections)
    └── images/                    Branded vector assets (SVG, no dependencies)
        ├── logo-mark.svg          App mark used in the landing header
        ├── platform-banner.svg    Platform banner on the passenger dashboard
        ├── travel-card.svg        Travel card artwork on the wallet page
        ├── gate-concourse.svg     Concourse gate bank on the gate control page
        ├── network-map.svg        Route diagram on the station management page
        └── fare-flow.svg          End-to-end module flow on the landing page
```

All six assets are inline vector SVG — they scale losslessly, carry `<title>`
and `<desc>` text, and require no image library, font or CDN.

16 pages in total, connected through working navigation.

---

## 4. Module ownership

| Module | Owner | Pages |
|---|---|---|
| **M1** Shared layout & Passenger Portal | **Aizat** | login, register, passenger dashboard, my tickets, wallet, top-up history |
| **M2** Media Processing | **Mirul** | passenger ticket, ticket validation |
| **M3** Gate Control | **Gate Control** | gate control (entry, exit, activity log, device register) |
| **M4** Fare Management | **Ile** | station management, fare management, fare calculation |
| **M5** Central Clearing House | **Harith Hakim** | clearing house dashboard, transactions, reconciliation |

The shared shell (sidebar, top bar, breadcrumbs, footer, buttons, cards, tables,
badges, forms) was built by M1 and reused by every other module, so the five
modules read as one system rather than five separate sites.

Every page carries an HTML comment identifying its module and owner.

---

## 5. Design system

**Palette** — defined once as custom properties in `:root` and never redefined:

| Token | Value | Use |
|---|---|---|
| Navy 900 | `#142B45` | Sidebar, primary buttons, dark panels |
| Navy 800 | `#203E5D` | Hover states, secondary surfaces |
| Teal 700 | `#0F766E` | Primary actions, active nav, accents |
| Teal 50 | `#E6F4F1` | Highlighted summary panels |
| Background | `#F4F7FA` | Page canvas |
| Ink / Muted | `#1E293B` / `#64748B` | Primary / secondary text |
| Success / Warning / Danger | `#16A34A` / `#F59E0B` / `#DC2626` | Status badges and lamps |
| Border | `#E2E8F0` | Card and table rules |

**Type** — Segoe UI Variable / Segoe UI with a system fallback stack. Identifiers
and amounts use a monospace face with tabular numerals so columns align.

**Layout** — a CSS Grid application shell: a fixed 268 px sidebar beside a fluid
main column, with a sticky top bar and a content container capped at 1440 px.

**Components** — `.card`, `.metric`, `.table`, `.badge`, `.btn`, `.field`,
`.alert`, `.verdict`, `.ticket`, `.qr`, `.gate`, `.fare`, `.recon`. All are
documented in section order inside `styles.css`.

**Responsive behaviour**

| Breakpoint | Behaviour |
|---|---|
| ≤ 1180 px | 4-up metric grids fall to 2-up; side columns stack |
| ≤ 1100 px | Sidebar narrows; clock hides |
| ≤ 960 px | Sidebar becomes a horizontal scrolling pill nav |
| ≤ 900 px | Two-column form/grid layouts single up; ticket stub stacks |
| ≤ 720 px | Breadcrumb module and user text hide |
| ≤ 560 px | Metrics go single column; buttons grow to 44 px targets |

Wide tables never break the layout: each is wrapped in `.table-wrap` with
`overflow-x: auto` and a fade cue indicating more columns.

---

## 6. Demonstration data

All records are **fictional**. Nothing is loaded from a database, an API or a
file — the values are written into the HTML.

One sample passenger is used consistently across every module so the journey can
be followed end to end:

| Field | Value |
|---|---|
| Passenger | `PSG-2026-004178` · Nurul Aisyah binti Rahman |
| Travel card | `AFC-CARD-4401982` |
| Ticket | `TKT-2026-884120` · Monthly Pass · Adult |
| QR / barcode reference | `QR-MYR-884120` / `BC-2026-884120` |
| Journey | KL Sentral → Subang Jaya · 18.6 km · 27 min |
| Fare | RM 2.60 |
| Wallet balance | RM 68.40 |

Supporting records: 5 passengers, 10 stations, 9 fare rules, 4 transit
operators, 14 fare transactions, 12 gate events, 7 media validations, 6 wallet
top-ups.

Daily clearing totals: 2,847 transactions, RM 18,462.30 collected,
RM 18,455.80 settled, RM 6.50 net difference across 2 discrepancies.

---

## 7. What is intentionally not implemented

This phase is front-end only. The following are static demonstrations:

- **Authentication** — sign-in and registration do not verify or store anything.
  Submitting either form simply opens the passenger dashboard.
- **Top-up** — no payment gateway is contacted and no balance changes.
- **QR / barcode** — the QR block is a decorative CSS placeholder. It is not
  generated from data and cannot be scanned.
- **Validation** — the form does not perform a lookup; both valid and invalid
  outcomes are shown side by side as static examples.
- **Gate control** — no barrier hardware is driven and no event is logged.
- **Fare calculation** — every figure is a fixed demonstration value; no
  arithmetic is executed.
- **Wallet deduction** — displayed as a visual change only.
- **Settlement reconciliation** — fixed sample records; no comparison logic runs.
- **Filters and search** — visual only, because filtering needs JavaScript or a
  server.

Pages state this explicitly with inline notices, and non-functional controls are
marked with a `demo-tag` or disabled so the prototype never implies real
processing.

---

## 8. Verification performed

The build was checked in a real browser (Chrome, via automation) and with a
static analyser:

- **16 pages** present, all reachable from `index.html`.
- **354 internal links** and all anchor targets resolve — 0 broken.
- **0** `<script>` elements, inline handlers, `javascript:` URLs, CDN references
  or external stylesheets.
- **0** unrendered template expressions in output.
- **32 page/viewport combinations** (1440 px and 390 px) checked for horizontal
  overflow — **0 failures**; the stylesheet loads on every page.
- Navigation click-tested across all five modules.
- Layout, component alignment and contrast reviewed from screenshots at desktop
  and mobile widths; sidebar and warning text raised to meet WCAG AA contrast.

---

## 9. Next phase

JavaScript and backend integration are deliberately out of scope here. The
natural next steps are:

1. Replace static tables with server-rendered records from a relational database
   (passengers, tickets, transactions, stations, fares, settlements).
2. Implement real form validation, authentication and role-based access.
3. Add fare-calculation logic driven by the fare rule table.
4. Implement QR encoding and reader integration for media processing.
5. Wire gate control to device APIs and persist gate events.
6. Automate the settlement comparison and discrepancy workflow.
