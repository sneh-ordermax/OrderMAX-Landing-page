# OrderMAX Landing Page — Project Context

## 1. What This Project Is

A static, single-file marketing website and supporting privacy-policy page for **OrderMAX** — a free Shopify cart upsell and cross-sell app. The site's sole job is to convert cold paid-traffic visitors into app installs, with a secondary goal of booking 15-minute founder calls.

There is no build system, no bundler, no Node dependencies, and no framework. Everything ships as vanilla HTML, inline CSS, and vanilla JavaScript.

---

## 2. Business Context

| Field | Detail |
|---|---|
| **Product** | OrderMAX — Shopify cart upsell & cross-sell app |
| **Shopify listing** | https://apps.shopify.com/ordermax-1 |
| **Live demo store** | https://morae-labs.myshopify.com (password-bypassed URL in the floating button) |
| **Pricing** | Free — every feature included |
| **Rating** | 5.0 ★ (1 review, Shopify App Store) |
| **Company address** | Manhattan, New York, NY, United States |
| **Privacy email** | privacy@ordermax.app |
| **Founder call booking** | https://cal.com/chloe.parker/15min |
| **Analytics** | Google Analytics 4 — property `G-RB49RESFSD` |

### Core value proposition

Shopify merchants running paid advertising pay per click. If each order only contains one item, the acquisition cost can wipe out margin. OrderMAX solves this with:

1. **Adaptive storefront widgets** — cart upsells, cross-sells, and free-gift offers that automatically inherit the store theme's typography, spacing, and button styles; a visual design editor is available for full control.
2. **Real-time funnel analytics** — tracks every funnel step (offer viewed → offer accepted → checkout started → order placed), revenue influenced, discount cost, and drop-off points.
3. **Automated A/B testing** — suggests tests, runs variants side-by-side, auto-shifts traffic to the winner, and surfaces a plain-language takeaway.
4. **Shopify Sidekick integration** — manage campaigns, restyle widgets, and pull reports conversationally through Shopify's native AI assistant.
5. **Founder-led onboarding** — personal support call offered to every new install.

---

## 3. File Structure

```
OrderMAX-landing-page/
├── index.html              # Main landing page (703 lines, ~54 KB, all-in-one)
├── privacy-policy/
│   └── index.html          # Privacy policy page (261 lines, ~21 KB)
├── images/
│   ├── logo.png            # App icon / favicon (~1.2 MB)
│   └── social-preview.png  # OG / Twitter card image (1672x941 px, ~1.8 MB)
└── context.md              # This file
```

No `package.json`, no `node_modules`, no CSS files, no JS files — everything is embedded inline in each HTML document.

---

## 4. Main Landing Page (`index.html`)

### 4.1 Head / Meta

- **Title:** `OrderMAX — Shopify Upsell & Cross-Sell App | Make Paid Traffic Profitable`
- **Meta description:** focuses on the free-to-install angle, adaptive widgets, real-time analytics, A/B testing.
- **Canonical URL:** `https://apps.shopify.com/ordermax-1` (points to the Shopify listing, not the domain)
- **OG image:** `https://ordermax.io/images/social-preview.png`
- **Structured data (JSON-LD):**
  - `SoftwareApplication` schema with a `Free` offer, 5.0 aggregate rating.
  - `FAQPage` schema with 6 Q&A pairs mirroring the FAQ section.

### 4.2 Fonts

Loaded via Fontshare CDN (no local files):
- **Cabinet Grotesk** — weights 500, 700, 800 — used for headings, brand name, big numbers.
- **Switzer** — weights 400, 500, 600 — used for body copy, nav, buttons, labels.

### 4.3 Design Tokens (inline CSS)

| Token | Value | Role |
|---|---|---|
| Background | `#F6F3EC` | Warm off-white page base |
| Dark text | `#17140D` | Near-black |
| Muted text | `#57503E` | Body copy |
| Subtle text | `#8B8471` | Meta, hints |
| Accent purple | `#4F3DF5` | Primary CTA, links, bars |
| Accent purple dark | `#3D2CE0` | Hover state |
| Accent purple light | `#DCD6FB` | Backgrounds, borders |
| Success green | `#2BA05A` / `#7CE3A4` | Live indicators, added state |
| Warning red | `#D14D3F` | Pain-point bullets |
| White card | `#fff` | Card surfaces |
| Off-white card | `#FBFAF6` | Subtle card variant |
| Dark footer | `#17140D` | Footer + ROI calculator bg |

### 4.4 Page Sections (in order)

| `data-screen-label` | `id` | Description |
|---|---|---|
| Nav | _(header)_ | Sticky, glass-blur navbar |
| Hero | `top` | H1, subhead, two CTAs, interactive demo cart |
| Marquee | _(div)_ | Horizontally scrolling ticker of feature keywords |
| Pain + Funnel | `pain` | Problem framing + interactive funnel visualizer |
| Features | `features` | 4-card feature grid |
| ROI Calculator | `calculator` | 3 sliders -> projected revenue lift |
| How it works | `how` | 3-step setup cards |
| Testimonial + Pricing | `proof` | One review + free pricing card |
| FAQ | `faq` | 6-item accordion |
| Final CTA | `cta` | Lavender-bg closing CTA with two buttons |
| Footer | _(footer)_ | Logo, copyright, nav links |

#### Nav

- Sticky, `backdrop-filter: blur(14px)` frosted glass effect.
- Links: The Leak, Features, Calculator, FAQ.
- CTAs: **Book a call** (outline) + **Add app — Free** (purple filled).
- "Book a call" outline link hides at 560 px and below; nav links hide at 860 px and below.

#### Hero

- **H1:** "Paying for traffic that barely converts?" — with a decorative underline swatch on the blue words.
- Sub-paragraph summarises the three pillars: native cart upsells, funnel analytics, A/B tests.
- **Primary CTA:** Add app on Shopify — Free (with Shopify bag SVG icon).
- **Secondary CTA:** Book a 15-min founder call.
- Interactive demo cart widget (below the hero copy):
  - Shows a single "Barrier Repair Cleanser" item ($34).
  - Two upsell offers rendered from `offersData`: Hydrating Serum ($18) and Moisture Cream ($10).
  - Clicking "Add" toggles the item into the cart; the total updates and a pop/spring animation plays.
  - A "A/B TEST · LIVE — Variant B +15.8% conv." chip floats top-right of the card.
  - A `[data-tilt]` 3D perspective tilt effect on mouse move.

#### Marquee

Words: CART UPSELLS · CROSS-SELLS · FREE GIFTS · FUNNEL ANALYTICS · AUTOMATED A/B TESTING · SIDEKICK CONTROL · REVENUE INFLUENCED · ADAPTIVE WIDGETS. Loops via CSS `@keyframes om-marquee`. Pauses on hover.

#### Pain + Funnel

Left column: framing copy ("You paid to get them to the cart. Then what happened?") with three red X bullets.

Right column: an "Offer funnel — last 30 days" widget with sample data:

| Stage | Value | Rate |
|---|---|---|
| Viewed offer | 4,800 | — |
| Accepted offer | 2,304 | 48% |
| Checkout started | 2,150 | 93% |
| Orders placed | 1,520 | 70% |

Hovering each row highlights it and swaps the insight callout at the bottom. Funnel bars animate in on scroll via polling.

#### Features

Four cards in a 2-column grid, each with a number badge, heading, body, and chip tags:

| # | Title | Accent colour |
|---|---|---|
| 01 | Adaptive storefront widgets | Lavender `#F0EDFD` |
| 02 | Real-time funnel analytics | Mint `#E4F0E6` |
| 03 | Automated A/B testing | Peach `#FAEBDD` |
| 04 | Sidekick control + AI guidance | Sky `#E2EDF8` |

Each card has a `[data-glow]` radial-gradient cursor-follow sheen effect.

#### ROI Calculator

Three `<input type="range">` sliders:
- Monthly orders: 100–10,000 (default 1,200)
- Average order value: $15–$150 (default $42)
- Cart value lift: 3%–25% (default 10%)

Formula: `gain = orders x aov x (lift / 100)`. Output: potential extra monthly revenue, yearly, and new AOV. CTA: "Start free — add on Shopify". Disclaimer: illustrative only.

#### How It Works

Three numbered cards (3-column grid, collapses to 1 on mobile):
1. **Install free & enable** — add from App Store, switch on app block, no code.
2. **Launch a campaign** — guided flow with AI recommendations.
3. **Watch, test, improve** — real-time analytics + automated A/B tests.

#### Testimonial + Pricing

**Review (5 stars):**
"OrderMAX has been a great Shopify upsell and cross-sell app for our store. The widgets adapted perfectly to our theme and felt completely native. After optimizing our campaigns, we achieved a 21% AOV lift and improved ROAS. The founder was also very responsive and personally helped us maximize results."
— M/S Spice Kingdom, India · 2 months using the app

**Pricing card:**
- **Free** — every feature included
- Checklist: Adaptive upsell & cross-sell widgets, Free-gift campaigns & triggers, Funnel & campaign analytics, Automated A/B testing, Shopify Sidekick integration, Founder-led onboarding support.

#### FAQ

6 items (accordion, one open at a time):
1. Is OrderMAX really free?
2. How does OrderMAX help stores running paid ads?
3. Will the upsell widgets match my store's theme?
4. Do I need a developer to set it up?
5. How does the automated A/B testing work?
6. Does OrderMAX work on mobile?

#### Floating Demo Button

Fixed bottom-right pill (`#om-demo-float`), purple, with a pulsing green dot. Links to the live Morae Labs demo store. Hides on mobile (560 px and below).

---

## 5. Privacy Policy Page (`privacy-policy/index.html`)

Standalone page sharing the same design system (fonts, colours, nav, footer) but with no interactive JS.

**Last updated / effective:** 6 August 2026.

15 sections:
1. Who we are
2. Scope (covers marketing website only, not the app or shoppers)
3. Information collected (booking details via Cal.com; GA4 analytics; no account required)
4. How we use information
5. Legal bases under GDPR/UK GDPR (consent, legitimate interests, contract, legal obligation)
6. Cookies (`_ga`, `_ga_<container-id>` — analytics only; no ad cookies)
7. Sharing (Google Analytics, Cal.com, Fontshare, hosting provider)
8. International transfers (SCC safeguards)
9. Retention (GA4 14 months; bookings 24 months; server logs 90 days)
10. Security (HTTPS, minimal data collection)
11. Privacy rights (GDPR access/correction/deletion/portability; CCPA; GPC honoured)
12. Children's privacy (not directed at under-16)
13. The OrderMAX Shopify app (app acts as processor, merchant is controller; data deleted on uninstall via Shopify data-deletion webhooks)
14. Policy changes
15. Contact (`privacy@ordermax.app`, Manhattan NY)

Note: the privacy policy page uses a CDN-hosted logo URL (Shopify CDN) instead of the relative `images/logo.png` path used on the main page.

---

## 6. JavaScript Architecture (`index.html`)

All JS is in a single IIFE at the bottom of `index.html` ("use strict"). No external libraries.

### State Object

```js
var state = {
  orders: 1200,   // calculator slider
  aov: 42,        // calculator slider
  lift: 10,       // calculator slider
  openFaq: 0,     // currently expanded FAQ index (-1 = none)
  added: {},      // demo cart items toggled { serum: bool, cream: bool }
  hoverStage: -1  // hovered funnel stage index (-1 = none)
};
```

### Data Arrays

| Variable | Content |
|---|---|
| `offersData` | 2 demo cart upsell items (Hydrating Serum $18, Moisture Cream $10) |
| `faqsData` | 6 FAQ questions + answers |
| `stageInsights` | 4 contextual callout messages for the funnel stages |
| `funnelData` | 4 funnel stage labels, values, rates, and bar percentages |
| `features` | 4 feature card objects (num, title, body, chips, bg, border) |
| `steps` | 3 "How it works" step objects |
| `marqueeWords` | 8 marquee keyword strings |

### Render Functions

| Function | What it builds |
|---|---|
| `renderMarquee()` | Duplicates `marqueeWords` into `#marquee` for seamless loop |
| `renderFeatures()` | Builds 4 feature cards into `#features-grid` |
| `renderSteps()` | Builds 3 step cards into `#steps` |
| `renderFunnel()` | Builds 4 funnel rows into `#funnel`, wires mouseenter/leave |
| `paintFunnel()` | Updates funnel row highlights and insight callout on hover |
| `renderFaqs()` | Rebuilds accordion HTML into `#faqs` on every state change |
| `renderDemo()` | Builds upsell offer rows into `#demo-offers` |
| `paintDemoTotals()` | Updates cart total and banner text/colour |
| `paintCalc()` | Updates all calculator output `data-*` elements |
| `popTotal()` | Springs the cart total element on add (scale + green flash) |

### Wire / Effect Functions

| Function | Behaviour |
|---|---|
| `wireCalc()` | Listens on `[data-input]` range inputs; debounces GA4 event at 800 ms |
| `wireHover()` | Applies `data-sh` (hover) and `data-sa` (active/mousedown) inline styles; idempotent via `_omHoverWired` flag |
| `wireEffects()` | Magnetic CTA drift, hero card 3D tilt, card cursor glow sheen, marquee pause-on-hover |
| `cursorFollower()` | Custom ring cursor on pointer devices — expands + fills on interactive elements |
| `observeReveals()` | Marks off-screen `[data-reveal]` elements as hidden (opacity 0, translateY 22px) |
| `check()` | Scroll/resize handler: reveals hidden elements, animates bars, fires GA4 `section_view` and `scroll_depth` events |

### Analytics Events (GA4 via `window.omTrack`)

| Event | Trigger |
|---|---|
| `section_view` | Section enters viewport (top < 65% vh, bottom > 35% vh) |
| `scroll_depth` | Fires once at 25%, 50%, 75%, 100% scroll depth |
| `faq_open` | FAQ accordion item opens |
| `calculator_use` | Any slider moved (debounced 800 ms; includes field, orders, aov, lift) |
| `demo_interact` | Demo cart offer toggled on (first time only per offer id) |

CTA links carry `data-cta` attribute identifiers for GA4 click tracking (no extra JS needed).

### Boot Sequence

```
boot()
  ├── renderMarquee / Features / Steps / Funnel / Faqs / Demo
  ├── paintDemoTotals / paintFunnel / paintCalc
  ├── wireCalc / wireHover / wireEffects / observeReveals
  ├── cursorFollower
  ├── addEventListener scroll + resize -> check()
  ├── setInterval(check, 450)          // fallback polling
  ├── check()                          // immediate first pass
  └── setTimeout(4000) -> force-reveal any still-hidden [data-reveal]
```

---

## 7. Responsive Breakpoints

| Breakpoint | Changes |
|---|---|
| 860 px and below | `.om-grid-2`, `.om-grid-2b`, `.om-grid-3`, `.om-grid-2f`, `.om-proof` collapse to single column; `.om-nav-links` hidden |
| 560 px and below | `.om-nav-cta-outline` ("Book a call" in nav) hidden; `#om-demo-float` floating button hidden |

---

## 8. External Dependencies

| Resource | URL | Purpose |
|---|---|---|
| Google Analytics 4 | `https://www.googletagmanager.com/gtag/js?id=G-RB49RESFSD` | Analytics |
| Fontshare CDN | `https://api.fontshare.com` + `https://cdn.fontshare.com` | Cabinet Grotesk + Switzer fonts |
| Cal.com | `https://cal.com/chloe.parker/15min` | Founder call booking |
| Shopify App Store | `https://apps.shopify.com/ordermax-1` | App install destination |
| Morae Labs demo | `https://morae-labs.myshopify.com` | Live in-store demo |

No other third-party scripts, no CDN CSS libraries, no icon libraries.

---

## 9. SEO Details

- Single `<h1>` per page.
- `<link rel="canonical">` on both pages.
- Semantic HTML5 (`<header>`, `<nav>`, `<section>`, `<footer>`, `<figure>`, `<figcaption>`, `<blockquote>`).
- Structured data: `SoftwareApplication` + `FAQPage` JSON-LD on main page.
- `aria-label` on nav elements; `aria-hidden="true"` on decorative SVGs.
- OG and Twitter card meta tags with 1672x941 social preview image.
- `meta name="robots" content="index, follow"` on the privacy policy page.

---

## 10. CTA Targets and `data-cta` Identifiers

| `data-cta` value | Location | Destination |
|---|---|---|
| `add_app_nav` | Nav bar | Shopify listing |
| `book_call_nav` | Nav bar | Cal.com |
| `add_app_hero` | Hero section | Shopify listing |
| `book_call_hero` | Hero section | Cal.com |
| `add_app_calculator` | ROI calculator | Shopify listing |
| `add_app_pricing` | Pricing card | Shopify listing |
| `add_app_footer` | Final CTA | Shopify listing |
| `book_call_footer` | Final CTA | Cal.com |
| `see_demo_float` | Floating button | Live demo store |

---

## 11. Data Attributes Reference

| Attribute | Purpose |
|---|---|
| `data-screen-label` | Section name sent to GA4 `section_view` event |
| `data-reveal` | Scroll-reveal animation target (fade + slide up 22px) |
| `data-sh="css"` | Inline hover styles applied by `wireHover()` |
| `data-sa="css"` | Inline mousedown/active styles applied by `wireHover()` |
| `data-magnet` | Enables magnetic drift effect on CTAs |
| `data-tilt` | Enables 3D perspective tilt (hero demo card) |
| `data-glow` | Card with cursor sheen effect |
| `data-glow-fx` | Inner overlay div that receives the radial gradient |
| `data-bar="N"` | Funnel progress bar; width set to N% when scrolled into view |
| `data-funnel-stage="N"` | Funnel row; triggers insight swap on hover |
| `data-insight` | Insight callout box below the funnel |
| `data-insight-icon` | Icon span inside the insight callout |
| `data-insight-text` | Text span inside the insight callout |
| `data-input="field"` | Calculator slider; `field` maps to state key |
| `data-orders-label` | Calculator output span |
| `data-aov-label` | Calculator output span |
| `data-lift-label` | Calculator output span |
| `data-monthly-gain` | Calculator output span |
| `data-yearly-gain` | Calculator output span |
| `data-new-aov` | Calculator output span |
| `data-total` | Demo cart total display |
| `data-demo-banner` | Demo cart banner below total |
| `data-demo-id="id"` | Offer add button; `id` maps to `offersData` item |
| `data-faq-index="N"` | FAQ accordion button |
| `data-faq-item="N"` | FAQ accordion wrapper |
| `data-marquee` | Marquee container; pauses animation on hover |
| `data-chips` | A/B test floating chip on the hero demo card |
