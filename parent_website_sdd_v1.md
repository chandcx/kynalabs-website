> **Spec-Driven Development Document**
> Parent Company Website
> Version 1.0 | Status: Implementation-Ready
> Intended for: Claude Code · Windsurf · Cursor
---
## DOCUMENT PURPOSE
This document is the single source of truth for building the parent company website. It covers information architecture, page specifications, design system, components, SEO, analytics, and technical implementation.
This is NOT the TapEat product site. TapEat appears as one product inside this website. The interactive TapEat demo is handled in a separate SDD. This document ends before that scope begins.
Hand this document directly to Claude Code, Windsurf, or Cursor as the build specification. Every decision is already made. The AI tool implements — it does not redesign.
---
## 1. PRODUCT IDENTITY AND BUSINESS GOALS
### 1.1 Company Identity
| Field | Value |
|---|---|
| Company name | **Kyna Labs** *(placeholder — replace before build)* |
| Tagline | **"We build software that works where your customers are"** |
| Category | B2B SaaS product company |
| Current product | TapEat — QR-based browser food ordering platform |
| Future products | To be defined. Website must accommodate them without redesign. |
| Business model | SaaS subscriptions + usage-based pricing per product |
| Target market | India-first, expanding to Southeast Asia |
### 1.2 Business Goals for This Website
Primary goals:
Establish Kyna Labs as a credible, multi-product technology company
Generate qualified vendor/business leads for TapEat
Create a foundation that accommodates future product launches
Enable demo booking and direct sales contact
Build SEO authority for the company brand and product categories
Secondary goals:
6. Attract talent (careers page optional in v2)
7. Build thought leadership via a resources/blog section
8. Give investors and partners a professional first impression
### 1.3 What Success Looks Like at Launch
- A visitor understands within 5 seconds that Kyna Labs builds digital products for businesses
- A restaurant owner can navigate to TapEat's product page in 2 clicks from anywhere
- A demo request can be submitted in under 60 seconds
- The site works completely on a mobile browser on 4G India
- The site loads in under 2.5 seconds on mobile (LCP target)
---
## 2. SCOPE AND NON-GOALS
### 2.1 In Scope
| # | In Scope |
|---|---|
| 1 | Parent company website with 8 core pages |
| 2 | TapEat product page (embedded in products section) |
| 3 | Placeholder structure for future products |
| 4 | Blog/resources section (structure + first 2 sample posts) |
| 5 | Contact and demo booking form |
| 6 | Navigation, footer, global header |
| 7 | Responsive design: mobile, tablet, desktop |
| 8 | SEO metadata, sitemap, robots.txt |
| 9 | Analytics event tracking (Google Analytics 4) |
| 10 | Accessibility: WCAG 2.1 AA on all pages |
### 2.2 Not In Scope (Non-Goals)
| # | Excluded | Reason |
|---|---|---|
| 1 | TapEat interactive demo / simulator | Separate SDD |
| 2 | Customer-facing ordering flow | TapEat product SDD |
| 3 | Vendor login or dashboard | TapEat product SDD |
| 4 | E-commerce or payment flows | Not needed for marketing site |
| 5 | CMS backend | Content hardcoded in v1. Headless CMS in v2. |
| 6 | Multi-language support | English only at launch |
| 7 | Careers page | v2 |
| 8 | Investor relations section | v2 |
| 9 | Customer portal / login | Not a marketing site concern |
| 10 | A/B testing infrastructure | v2 |
---
## 3. USERS AND TARGET AUDIENCES
### 3.1 Primary Audiences
| Persona | Who | What They Want | Where They Land |
|---|---|---|---|
| **Restaurant/Café Owner** | Single or multi-location F&B operator in India | To understand if TapEat solves their ordering problem. Book a demo. | Home → TapEat product page → Book Demo |
| **Corporate Cafeteria Manager** | Facilities or admin manager at an IT company or campus | To see if TapEat fits their cafeteria workflow. | Use Cases → TapEat page → Contact |
| **Tech-Curious Evaluator** | Someone who found the site via search or referral | To validate if Kyna Labs is a legitimate company | Home → About → Products |
| **Potential Partner / Investor** | VC, angel, or integration partner | Company overview, team credibility, product portfolio | Home → About → Contact |
### 3.2 Secondary Audiences
| Persona | Who | What They Want |
|---|---|---|
| **Journalist / Blogger** | Tech or F&B industry media | Company story, product differentiation |
| **Job Seeker** | Engineer or designer | Company culture, product quality signal |
| **Future Product Customer** | User of a product not yet launched | Will find a placeholder or waitlist |
### 3.3 Device Distribution Assumption
Mobile (Android Chrome): 65%
Desktop:                  28%
Tablet:                    7%
India mobile-first. All layouts designed mobile-first.
Desktop enhancement, not the primary design surface.
---
## 4. BRAND AND POSITIONING
### 4.1 Brand Voice
| Attribute | Description | Example |
|---|---|---|
| **Direct** | No corporate fluff. Short sentences. | "We build software your customers actually use." |
| **Confident** | State facts, not aspirations | "TapEat is live in cafeterias across Hyderabad." |
| **Human** | Avoid jargon. Talk like a founder. | "We noticed restaurants losing orders to wait times." |
| **India-aware** | Acknowledge the India context naturally | "Built for UPI, mobile browsers, and real kitchens." |
### 4.2 Visual Identity Direction
Primary color:     #3B0764  (deep purple — trust, tech)
Accent color:      #F59E0B  (amber — energy, India warmth)
Neutral dark:      #1E293B  (slate)
Neutral mid:       #64748B  (gray)
Background light:  #FAFAF9  (warm off-white)
Background dark:   #0F0F0F  (for dark sections)
Success:           #16A34A
White:             #FFFFFF
Typography:
Headings: Sora (Google Fonts) — bold, geometric
Body:     Inter (Google Fonts) — readable, neutral
Mono:     JetBrains Mono — for code/technical snippets
Border radius: 12px standard, 20px for cards, 999px for pills
Shadows: subtle — box-shadow: 0 2px 12px rgba(0,0,0,0.06)
### 4.3 Photography and Illustration Direction
Real photography preferred over stock. Authentic India café/canteen context.
If stock photos used: diverse, India-representative, not generic Western office scenes.
Illustrations: flat, geometric, consistent line weight.
Icons: Lucide React (consistent with product suite).
No AI-generated faces in v1.
### 4.4 Positioning Statement
**For** restaurant and cafeteria operators in India 
**Who** lose revenue and customers to slow manual ordering 
**Kyna Labs** builds browser-native software products 
**That** work without app downloads, on any device, on any network 
**Unlike** app-based platforms that create barriers for staff and customers
---
## 5. INFORMATION ARCHITECTURE
### 5.1 Site Map
kynalabs.in/
│
├── /                          Home
├── /about                     About Kyna Labs
├── /products                  Products overview (all products)
│   ├── /products/tapeat       TapEat product page
│   └── /products/[future]     Future product pages (placeholder pattern)
├── /use-cases                 Use cases by industry/role
│   ├── /use-cases/restaurants      Restaurants and cafes
│   ├── /use-cases/cafeterias       Corporate and campus cafeterias
│   └── /use-cases/food-courts      Food courts and malls
├── /resources                 Blog / articles / guides
│   └── /resources/[slug]      Individual article page
├── /contact                   Contact form
└── /book-demo                 Demo booking page (primary CTA destination)
Supporting:
├── /sitemap.xml               Auto-generated
├── /robots.txt                Auto-generated
└── 404.tsx                    Custom 404 page
### 5.2 Navigation Hierarchy
Primary nav (top):
Products ▾    (dropdown: TapEat + "More coming soon")
Use Cases ▾   (dropdown: Restaurants, Cafeterias, Food Courts)
Resources
About
[Book a Demo]  ← CTA button, always visible
Footer nav:
Company: About, Contact, Careers (coming soon)
Products: TapEat, [Future Product]
Resources: Blog, Case Studies (coming soon)
Legal: Privacy Policy, Terms of Service
---
## 6. PAGE-LEVEL SPECIFICATIONS
---
### 6.1 HOME PAGE (/)
**Purpose:** Communicate who Kyna Labs is, what problems they solve, and move visitors to a product page or demo booking. Must not feel like a TapEat-only site.
**URL:** /
**Title tag:** Kyna Labs — Software Built for Real Businesses
**Meta description:** Kyna Labs builds browser-native software products for restaurants, cafeterias, and beyond. No app downloads. No friction.
---
#### Sections (in order):
**HERO**
Layout: Full-width, min-height 100vh on desktop, auto on mobile
Left: Text block
Right: Abstract product visual OR short looping device mockup (no TapEat demo)
Headline (H1):
"Software your customers
use the moment they need it."
Subheadline:
"We build browser-native products for operators in India.
No app downloads. No barriers. Just working software."
CTAs:
Primary: "Explore Our Products"  → /products
Secondary: "Book a Demo"         → /book-demo
Badge strip below CTAs:
"India-First" | "Browser-Native" | "UPI-Ready" | "Real-Time"
**PROBLEM STATEMENT STRIP**
Layout: Dark background (#1E293B), 3-column on desktop, stacked on mobile
Headline: "Built for how India actually works"
3 pain points (icon + headline + 1 line):
"Customers won't download another app"
Most restaurant apps have < 5% conversion.
"Waiters are a bottleneck, not a feature"
Every missed order is lost revenue.
"Your tech should work on ₹8,000 Android phones"
Not just on the latest iPhone.
**PRODUCTS SECTION**
Headline: "What We Build"
Subheadline: "Software products for real operational problems."
Layout: Card grid — 2 columns desktop, 1 column mobile
Card 1: TapEat
Icon/logo: TapEat wordmark or icon
Tag: "Live Product"  (green pill)
Headline: "QR-based browser ordering for restaurants and cafeterias"
Body: "Customers scan, order, and pay in under 60 seconds.
No app. No login. Works on any Android or iOS browser."
CTA: "Learn More →"  → /products/tapeat
Card 2: [Future Product]
Tag: "Coming Soon" (amber pill)
Headline: "Our next product is in development"
Body: "We're building another solution for the food and
hospitality sector. Join the waitlist."
CTA: "Join Waitlist →"  → /contact (with pre-filled subject)
**USE CASES STRIP**
Headline: "Who We Build For"
3 tiles (icon + label):
Restaurants & Cafés | Corporate Cafeterias | Food Courts & Malls
Each links to /use-cases/[segment]
**SOCIAL PROOF / TRACTION**
Layout: Light background, centered
Headline: "Trusted by operators across India"
Note: In v1, if no customer logos available, use stat-based proof:
Stats row (3 numbers):
50+       Orders processed in pilot
3         Pilot vendors live
< 60 sec  Average time to place an order
Below stats: small disclaimer "Based on pilot data, April 2025"
If logos available: replace stats row with logo strip.
**HOW IT WORKS (brief — points to product page for detail)**
Headline: "From scan to kitchen in seconds"
3 steps (numbered, horizontal on desktop, vertical on mobile):
Scan        Customer scans QR. Menu opens in browser.
Order       Items added, UPI payment complete.
Kitchen     Order appears on kitchen dashboard. Instantly.
CTA below: "See full product details" → /products/tapeat
**COMPANY INTRO STRIP**
Layout: Split — left text, right abstract graphic
Headline: "We're Kyna Labs"
Body (2-3 sentences):
"We're a product company based in India, building software
that works where your customers already are — the browser.
We don't build apps that people have to download. We build
experiences that work instantly, on any device."
CTA: "About us →"  → /about
**FINAL CTA SECTION**
Background: Deep purple (#3B0764)
Headline: "Ready to see it in action?"
Subheadline: "Book a 20-minute demo. We'll show you live."
CTA: "Book a Demo"  → /book-demo (white button, purple text)
---
### 6.2 ABOUT PAGE (/about)
**Purpose:** Build credibility. Explain who built this, why, and what Kyna Labs stands for. Must feel like a real company with a real story, not a one-product landing page.
**Title tag:** About Kyna Labs — The Team Behind the Products
**Meta description:** Kyna Labs is a product company building browser-native software for businesses in India. Meet the team and our mission.
---
#### Sections:
**HERO**
Headline: "We build software for the way India works"
Subheadline (2-3 sentences):
"Most software assumes your customers have time, fast internet,
and the patience to download an app. Ours doesn't.
We build for real conditions — mobile browsers, 4G connections,
and people who just want to get things done."
**ORIGIN STORY**
Format: 2 column — left text, right image (team or office photo)
Headline: "Why we started"
Body (3-4 short paragraphs):
The observation (restaurants losing customers to friction)
The insight (browsers are universal apps)
The decision to build TapEat
The bigger vision (building a portfolio of such products)
**MISSION AND VALUES**
Headline: "What we stand for"
3 values (icon + name + 1-sentence explanation):
Browser-first     "The browser is the most installed app.
We build there."
India-native      "Built for UPI, for 4G, for Android.
Not adapted — built."
Operator-first    "We talk to vendors before we write code.
Always."
**TEAM SECTION**
Headline: "The team"
Layout: Card grid, 3-4 columns desktop, 2 mobile
Team member card:
Photo (square, rounded corners)
Name
Title
1-line bio
LinkedIn icon link
Note: If founding team < 3 people, show 2 cards + 1 "We're hiring" card
**COMPANY DETAILS STRIP**
4 facts (small, honest, specific):
Founded: 2025
Headquarters: Hyderabad, India
Products: 1 live, 1 in development
Model: SaaS — subscription + usage
**CLOSING CTA**
Headline: "Want to see what we're building?"
CTA: "View our products →"  → /products
---
### 6.3 PRODUCTS OVERVIEW PAGE (/products)
**Purpose:** Show all current and upcoming products. Acts as a hub. Must not be a TapEat page — it is a portfolio page with TapEat as the first entry.
**Title tag:** Products — Kyna Labs
**Meta description:** Explore Kyna Labs product portfolio. Browser-native software for operators in India's food and hospitality sector.
---
#### Sections:
**HERO**
Headline: "Products built for operators"
Subheadline:
"Each product we build solves one real operational problem.
Browser-native, India-first, production-ready."
**PRODUCT CARDS (Full)**
Card 1: TapEat                              [LIVE]
Logo/wordmark
Category pill: "Food Ordering"
Headline: "QR-based browser ordering for restaurants and cafeterias"
Feature list (4 bullets):
- No app download required
- UPI payment built-in
- Real-time kitchen dashboard
- Works on any mobile browser
CTA: "Learn more →"  → /products/tapeat
Secondary CTA: "Book a demo →"  → /book-demo
Card 2: [Product 2 placeholder]             [COMING SOON]
Category pill: "TBD"
Headline: "Something new is in development"
Body: "We're working on our next product.
Join the waitlist to be notified first."
CTA: "Join waitlist →"  → /contact
Note: This card uses a locked placeholder component.
When Product 2 launches, replace content and link.
The component structure stays the same.
**WHY KYNA LABS PRODUCTS**
Headline: "What every Kyna Labs product has in common"
3-column feature list:
Browser-native      No app stores. No downloads.
India-first         UPI, 4G, Android Chrome — all supported.
Operator-focused    Built from real operational problems.
---
### 6.4 TAPEAT PRODUCT PAGE (/products/tapeat)
**Purpose:** The definitive marketing page for TapEat. Explains the product, shows how it works, lists features, shows social proof, and drives demo booking. TapEat wow-demo is NOT included here — it will be added from a separate SDD.
**Title tag:** TapEat — QR Browser Ordering for Restaurants | Kyna Labs
**Meta description:** TapEat lets customers scan a QR code and order food in their browser — no app needed. Real-time kitchen dashboard. UPI payments. Built for India.
---
#### Sections:
**HERO**
Eyebrow: "A Kyna Labs Product"
Headline (H1): "Your customers scan. They order. You cook."
Subheadline:
"TapEat turns any table into an ordering point.
No app. No waiter needed. Orders go straight to the kitchen."
CTAs:
Primary: "Book a Demo"        → /book-demo
Secondary: "See how it works" → scrolls to #how-it-works
Visual: Device mockup showing mobile menu page (static screenshot)
Note: Interactive demo NOT included here — see demo SDD.
**PROBLEM SECTION**
Headline: "Every minute a customer waits, you lose money"
3 problems (icon + stat + explanation):
"60% of customers abandon orders when wait time exceeds 8 minutes"
"Waiter-dependent ordering limits your table throughput"
"App downloads kill conversion — most customers won't bother"
Source note: "Based on pilot observations, April 2025"
**HOW IT WORKS** (id="how-it-works")
Headline: "From scan to kitchen in under 60 seconds"
Step-by-step (horizontal timeline desktop, vertical mobile):
Step 1: Scan
Visual: Phone scanning QR on table
Headline: "Customer scans the table QR"
Body: "No app download. No login.
Browser opens instantly."
Step 2: Order
Visual: Mobile menu screenshot
Headline: "Menu opens in the browser"
Body: "Browse items. Add to cart.
Pay via UPI in seconds."
Step 3: Kitchen
Visual: Tablet kitchen dashboard screenshot
Headline: "Order appears on your dashboard"
Body: "Real-time. With an alert.
Accept, prepare, mark ready."
Step 4: Done
Visual: Customer status screen
Headline: "Customer tracks their order"
Body: "Status updates live.
No calls to the kitchen."
**FEATURES SECTION**
Headline: "Everything you need. Nothing you don't."
Feature grid (2 columns desktop, 1 mobile):
Feature 1: No App Required
Icon: Smartphone with X
Body: "Customers order in their browser.
Android, iOS — it works everywhere."
Feature 2: UPI-First Payments
Icon: Indian Rupee / payment
Body: "Pay via UPI, cards, or wallets.
Pay-before-order. Zero reconciliation friction."
Feature 3: Real-Time Kitchen Dashboard
Icon: Monitor / display
Body: "Orders appear instantly. Accept, prepare, complete.
Works on any Android tablet."
Feature 4: QR Table Management
Icon: QR code
Body: "Generate QR codes for every table and counter.
Download, print, done."
Feature 5: Role-Based Access
Icon: Users / shield
Body: "Owner, Manager, Kitchen Staff.
Each role sees exactly what they need."
Feature 6: Order Tracking for Customers
Icon: Clock / checkmark
Body: "Customers see their order status live.
No calling the kitchen."
**WHO IT'S FOR**
Headline: "Built for these operators"
3 tiles (icon + label + 2-line description):
Restaurants and Cafés
Corporate Cafeterias
Food Courts
Each tile links to corresponding /use-cases/[segment]
**SOCIAL PROOF**
Same traction stats as home page (or expand with pilot quotes if available).
If vendor quote available:
Blockquote with vendor name, business name, city.
No fake quotes. If no real quote, use stats only.
**DEMO CTA (sticky bottom on mobile)**
Full-width CTA section:
Headline: "See TapEat live in 20 minutes"
Body: "We'll walk you through the full flow.
Bring your menu. We'll set up a demo account."
CTA: "Book a Free Demo"  → /book-demo
**NOTE ON INTERACTIVE DEMO**
<!-- Placeholder for interactive TapEat demo widget -->
<!-- This section will be populated from the TapEat Demo SDD -->
<!-- Do not build the demo here. Leave a clearly marked div: -->
<div id="tapeat-demo-placeholder"
    data-note="Interactive demo injected from demo-sdd build">
 <!-- Demo goes here -->
</div>
````
6.5 FUTURE PRODUCT PLACEHOLDER PAGE (/products/[slug])
Purpose: When the next product launches, a page already exists in the routing structure. This prevents dead links and enables early SEO.
Pattern:
File: app/products/[slug]/page.tsx
Behavior:
 - If slug = 'tapeat' → render TapEat page (hardcoded)
 - If slug matches a known future product → render that page
 - If slug is unknown → render Coming Soon page
Coming Soon page content:
 Headline: "This product is on its way"
 Body: "We're building something new. Leave your email
        and we'll let you know when it's ready."
 Form: Email input + "Notify me" button (POST to /api/waitlist)
 Back link: "← Back to all products"
6.6 USE CASES PAGES (/use-cases + sub-pages)
Purpose: Reach buyers searching for solutions by their industry or role, not by product name. SEO-rich pages targeting specific operator types.
Use Cases Overview Page (/use-cases)
Title: "Use Cases — Kyna Labs"
Hero: "Find your use case"
3 cards linking to sub-pages:
 - Restaurants & Cafés
 - Corporate Cafeterias
 - Food Courts & Malls
Sub-page pattern (all 3 follow same template):
URL: /use-cases/restaurants
Title: "QR Ordering for Restaurants and Cafés | Kyna Labs"
Meta: "See how TapEat helps restaurants reduce wait times,
      increase table turns, and accept UPI payments. No app required."
Sections:
1. HERO
  Headline specific to segment:
  "Restaurants: Turn every table into an ordering point"
2. THE PROBLEM (specific to segment)
  3 pain points real for this operator type
3. THE SOLUTION
  How TapEat solves these specific problems
  Screenshots relevant to this context
4. KEY BENEFITS
  3-4 quantified or qualified outcomes
5. WORKFLOW
  Before TapEat vs After TapEat
  Simple 2-column comparison table
6. CTA
  "Book a demo for your [restaurant/cafeteria/food court]"
  → /book-demo
7. RELATED USE CASES
  Links to other use case pages
6.7 RESOURCES / BLOG (/resources)
Purpose: Build SEO authority. Provide value to potential customers. Establish Kyna Labs as a knowledgeable team.
Index page (/resources)
Title: "Resources — Kyna Labs"
Layout: Blog grid — 3 columns desktop, 1 mobile
Filter tabs: All | Product | Industry | How-To
Each card:
 - Category pill
 - Title (H3)
 - 1-line excerpt
 - Author name + date
 - "Read →" link
For v1: Pre-populate with 2 sample articles
Sample articles for v1:
Article 1:
 Slug: /resources/qr-ordering-india
 Title: "Why QR-based ordering is the right model for India"
 Category: Industry
Article 2:
 Slug: /resources/reduce-wait-times-restaurant
 Title: "5 ways to reduce wait times in your restaurant without hiring more staff"
 Category: How-To
Individual article page (/resources/[slug])
Layout:
 Left (70%): Article content
 Right (30%): Sticky sidebar
   - Author bio card
   - "Book a Demo" CTA card
   - Related articles (2 links)
Article content:
 - H1 title
 - Author + date + read time
 - Cover image
 - Article body (markdown rendered)
 - Tags
 - End CTA: "Want to see this in action? Book a demo."
6.8 CONTACT PAGE (/contact)
Purpose: Catch-all contact for non-demo inquiries: partnerships, press, general questions.
Title tag: Contact Kyna Labs
Meta description: Get in touch with the Kyna Labs team. Partnerships, press, general inquiries.
Sections:
1. HEADER
  Headline: "Let's talk"
  Subheadline: "Have a question, partnership idea, or press inquiry?
                Drop us a message."
2. CONTACT FORM
  Fields:
    Name (required)
    Email (required)
    Company (optional)
    Subject — select:
      [ General inquiry ]
      [ Partnership ]
      [ Press / Media ]
      [ Product feedback ]
      [ Waitlist for upcoming product ]
    Message (required, min 20 chars)
  Submit: "Send message"
 
  POST to: /api/contact
  On success: Inline thank you message
  On error: Inline error, preserve form values
3. CONTACT DETAILS
  Email: hello@kynalabs.in
  Response time: "We typically respond within 1 business day"
 
4. LOOKING FOR A DEMO?
  "If you want to see TapEat in action, book a demo directly."
  CTA: "Book a demo →"  → /book-demo
6.9 BOOK DEMO PAGE (/book-demo)
Purpose: Primary conversion page. A visitor arrives here from multiple CTAs across the site. Must be fast, friction-free, and specific.
Title tag: Book a TapEat Demo — Kyna Labs
Meta description: Book a free 20-minute demo of TapEat. We'll show you the full ordering flow, kitchen dashboard, and QR setup. Live. No slides.
Sections:
1. HERO
  Headline: "See TapEat live in 20 minutes"
  Subheadline:
    "No slides. No pre-recorded video. A real product demo,
     set up for your use case."
 
  What to expect (3 bullet points):
    ✓ Full customer ordering flow on a real device
    ✓ Live kitchen dashboard walkthrough
    ✓ Your questions answered by the team
2. DEMO BOOKING FORM
  Fields:
    Full name (required)
    Email (required)
    Phone number (required — India mobile format)
    Business name (required)
    Business type — select:
      [ Restaurant / Café ]
      [ Corporate Cafeteria ]
      [ Food Court ]
      [ Hotel / Hospitality ]
      [ Other ]
    Number of locations — select:
      [ 1 location ]
      [ 2–5 locations ]
      [ 6+ locations ]
    How did you hear about us — select:
      [ Google search ]
      [ Referral ]
      [ LinkedIn ]
      [ WhatsApp ]
      [ Other ]
    Preferred time (optional, text field):
      "Any preference for time/day?"
 
  Submit: "Request Demo"
  POST to: /api/book-demo
 
  On success:
    Replace form with confirmation:
    "We've received your request. Expect a WhatsApp or email
     from us within 4 business hours."
 
  On error: Inline error, preserve form values.
3. TRUST SIGNALS (below form)
  "Join operators across India already using TapEat"
  3 small stat pills:
    3 Pilot Vendors | 50+ Orders | < 60s avg order time
7. NAVIGATION MODEL
7.1 Global Header
Layout: Sticky on scroll, transparent → white on scroll
Height: 64px desktop, 56px mobile
Left:    Kyna Labs logo (SVG wordmark)
Center:  Navigation links (desktop only)
Right:   "Book a Demo" CTA button + optional hamburger (mobile)
Desktop nav links:
 Products  (dropdown trigger)
 Use Cases (dropdown trigger)
 Resources
 About
Mobile nav:
 Hamburger → full-screen slide-in menu
 Same links as desktop, stacked
 "Book a Demo" prominent at top of mobile menu
7.2 Dropdowns
Products dropdown:
TapEat                  → /products/tapeat
 ↳ "Scan. Order. Eat."
── divider ──
More products coming soon
 ↳ [No link — greyed out]
Use Cases dropdown:
Restaurants & Cafés     → /use-cases/restaurants
Corporate Cafeterias    → /use-cases/cafeterias
Food Courts & Malls     → /use-cases/food-courts
7.3 Footer
Layout: 4-column desktop, 2-column tablet, 1-column mobile
Column 1: Brand
 Kyna Labs logo
 Tagline: "Software built for real businesses"
 Social links: LinkedIn, Twitter/X (icons only)
Column 2: Products
 TapEat
 [Future Product] (greyed)
Column 3: Company
 About
 Contact
 Careers (coming soon — greyed)
 Resources
Column 4: Legal
 Privacy Policy  → /privacy
 Terms of Service → /terms
Bottom bar:
 © 2025 Kyna Labs. All rights reserved.
 "Made in India 🇮🇳"
8. CONTENT HIERARCHY
8.1 Heading Hierarchy Rules
H1: One per page. Page's primary keyword topic.
H2: Major sections within a page.
H3: Subsections, card titles, feature names.
H4: Supporting labels, form section titles.
Body: 16px, line-height 1.6 minimum.
Caption: 14px, color: #64748B.
Never skip heading levels.
Never use headings purely for size — use CSS for that.
8.2 Copy Length Standards
ElementMax LengthH1 headline8 wordsH2 section headline10 wordsCard headline10 wordsCard body2-3 sentences, 40 wordsMeta description155 charactersPage subheadline25 words
9. DESIGN SYSTEM DIRECTION
9.1 Color Tokens
typescript// tokens/colors.ts
export const colors = {
 brand: {
   purple:      '#3B0764',
   purpleMid:   '#6D28D9',
   purpleLight: '#EDE9FE',
   amber:       '#F59E0B',
   amberLight:  '#FEF3C7',
 },
 neutral: {
   slate:     '#1E293B',
   slateLight:'#334155',
   gray:      '#64748B',
   grayLight: '#94A3B8',
   border:    '#E2E8F0',
   bg:        '#FAFAF9',
   bgDark:    '#0F0F0F',
 },
 semantic: {
   success: '#16A34A',
   error:   '#DC2626',
   warning: '#F59E0B',
   info:    '#1D4ED8',
 },
 white: '#FFFFFF',
};
9.2 Typography Scale
typescript// tokens/typography.ts
export const type = {
 display:  { size: '56px', weight: 800, lineHeight: 1.1 },  // hero H1
 h1:       { size: '40px', weight: 700, lineHeight: 1.2 },
 h2:       { size: '30px', weight: 700, lineHeight: 1.3 },
 h3:       { size: '22px', weight: 600, lineHeight: 1.4 },
 h4:       { size: '18px', weight: 600, lineHeight: 1.4 },
 body:     { size: '16px', weight: 400, lineHeight: 1.6 },
 bodyLg:   { size: '18px', weight: 400, lineHeight: 1.6 },
 small:    { size: '14px', weight: 400, lineHeight: 1.5 },
 caption:  { size: '12px', weight: 400, lineHeight: 1.4 },
 label:    { size: '13px', weight: 500, lineHeight: 1.4, letterSpacing: '0.05em' },
};
9.3 Spacing Scale
4, 8, 12, 16, 20, 24, 32, 40, 48, 64, 80, 96, 128 (px)
Use Tailwind's default spacing scale.
Section padding: 80px vertical desktop, 48px mobile.
Container max-width: 1200px, horizontal padding: 24px.
9.4 Breakpoints
Mobile:  < 768px    (design base)
Tablet:  768–1024px
Desktop: > 1024px
Wide:    > 1280px   (max-width container stops expanding)
10. REUSABLE COMPONENT ARCHITECTURE
10.1 Component File Structure
components/
├── layout/
│   ├── Header.tsx          Global sticky header
│   ├── Footer.tsx          Global footer
│   ├── Container.tsx       Max-width wrapper with padding
│   └── Section.tsx         Section wrapper with vertical padding
│
├── navigation/
│   ├── NavLink.tsx         Single nav link with active state
│   ├── Dropdown.tsx        Hover/click dropdown menu
│   └── MobileMenu.tsx      Full-screen mobile nav
│
├── ui/
│   ├── Button.tsx          Primary, secondary, ghost, text variants
│   ├── Badge.tsx           Pill badges (Live, Coming Soon, etc.)
│   ├── Card.tsx            Reusable card with slot children
│   ├── Input.tsx           Form input with error state
│   ├── Select.tsx          Dropdown select with error state
│   ├── Textarea.tsx        Multi-line input
│   ├── FormField.tsx       Label + input + error message wrapper
│   └── Icon.tsx            Lucide icon wrapper with size/color props
│
├── sections/               Reusable page sections
│   ├── HeroSection.tsx     Headline + sub + CTAs + visual
│   ├── FeatureGrid.tsx     Icon + title + body grid
│   ├── StepProcess.tsx     Numbered horizontal/vertical steps
│   ├── CTABanner.tsx       Full-width CTA with background
│   ├── StatsRow.tsx        3–4 stat numbers in a row
│   ├── ProductCard.tsx     Product overview card (used in grid)
│   ├── UseCaseTile.tsx     Use case icon + label + link
│   └── TestimonialCard.tsx Quote + author + company
│
├── blog/
│   ├── ArticleCard.tsx     Blog index card
│   └── ArticleLayout.tsx   Blog post page layout
│
└── forms/
   ├── ContactForm.tsx     /contact page form
   └── DemoBookingForm.tsx /book-demo page form
10.2 Button Component Spec
typescript// components/ui/Button.tsx
type ButtonProps = {
 variant:  'primary' | 'secondary' | 'ghost' | 'text';
 size:     'sm' | 'md' | 'lg';
 href?:    string;           // if set, renders as <a>
 onClick?: () => void;
 disabled?: boolean;
 loading?:  boolean;
 children:  React.ReactNode;
 className?: string;
};
// Styles:
// primary:   bg-brand-purple text-white hover:bg-brand-purpleMid
// secondary: border-2 border-brand-purple text-brand-purple hover:bg-brand-purpleLight
// ghost:     bg-transparent text-brand-purple underline-offset
// text:      text-brand-purple hover:underline (no border/bg)
// Size:
// sm: px-4 py-2 text-sm
// md: px-6 py-3 text-base  (default)
// lg: px-8 py-4 text-lg
10.3 ProductCard Component Spec
typescript// components/sections/ProductCard.tsx
type ProductCardProps = {
 name:        string;
 tagline:     string;
 description: string;
 status:      'live' | 'coming-soon' | 'beta';
 features:    string[];      // up to 4 bullet points
 href:        string;
 ctaLabel:    string;
 icon?:       React.ReactNode;
};
// Status badge colors:
// live:         green background, "Live" label
// coming-soon:  amber background, "Coming Soon" label
// beta:         blue background, "Beta" label
11. RESPONSIVE BEHAVIOR
11.1 Rules
1. Mobile-first CSS. Write base styles for mobile, enhance for desktop.
2. No horizontal scroll on any page at any breakpoint.
3. Touch targets: minimum 44×44px on all interactive elements.
4. Font sizes: never below 16px for body text on mobile.
5. Images: use next/image with sizes prop for responsive loading.
6. Tables: scroll horizontally on mobile, or restructure as stacked cards.
11.2 Layout Transformations
ComponentMobileTabletDesktopHeroStacked, text firstStacked, larger text2-column splitNavHamburger → slide-inHamburger → slide-inHorizontal linksProduct cards1-column2-column2-columnFeature grid1-column2-column3-columnStats row2×2 grid4-column row4-column rowFooter1-column stacked2-column4-columnBlog grid1-column2-column3-columnStep processVertical numberedVertical numberedHorizontalFormFull width600px centered600px centered
12. SEO REQUIREMENTS
12.1 Per-Page Metadata
Every page must export metadata using Next.js generateMetadata:
typescript// Pattern for every page:
export const metadata: Metadata = {
 title:       'Page Title — Kyna Labs',
 description: 'Meta description max 155 chars.',
 openGraph: {
   title:       'Page Title',
   description: 'OG description',
   url:         'https://kynalabs.in/[slug]',
   siteName:    'Kyna Labs',
   images: [{
     url:    '/og/[page]-og.png',   // 1200×630 px static image
     width:  1200,
     height: 630,
   }],
   locale: 'en_IN',
   type:   'website',
 },
 twitter: {
   card:        'summary_large_image',
   title:       'Page Title',
   description: 'Twitter description',
   images:      ['/og/[page]-og.png'],
 },
 alternates: {
   canonical: 'https://kynalabs.in/[slug]',
 },
};
12.2 Metadata Per Page
PageTitlePrimary KeywordHomeKyna Labs — Software Built for Real Businesseskyna labsAboutAbout Kyna Labs — The Team Behind the Productskyna labs teamProductsProducts — Kyna Labskyna labs productsTapEatTapEat — QR Browser Ordering for Restaurants | Kyna Labsqr ordering restaurants indiaUse Cases: RestaurantsQR Ordering for Restaurants and Cafés | Kyna Labsqr menu restaurant indiaUse Cases: CafeteriasDigital Ordering for Corporate Cafeterias | Kyna Labscafeteria ordering system indiaUse Cases: Food CourtsQR Food Ordering for Food Courts | Kyna Labsfood court ordering systemResourcesResources — Kyna Labsrestaurant technology indiaContactContact Kyna Labskyna labs contactBook DemoBook a TapEat Demo — Kyna Labstapeat demo
12.3 Technical SEO
□ Sitemap: /sitemap.xml (auto-generated by Next.js)
□ Robots: /robots.txt (allow all in production)
□ Canonical URLs: set on every page
□ Structured data (JSON-LD):
   - Organization schema on Home and About
   - SoftwareApplication schema on TapEat product page
   - BlogPosting schema on article pages
□ Image alt text: required on every <Image> component
□ Internal linking: every page links to at least 2 other pages
□ Heading hierarchy: validated on every page (H1 → H2 → H3)
□ Core Web Vitals targets:
   LCP < 2.5s
   FID < 100ms
   CLS < 0.1
12.4 Structured Data — Organization (Home page)
json{
 "@context": "https://schema.org",
 "@type": "Organization",
 "name": "Kyna Labs",
 "url": "https://kynalabs.in",
 "logo": "https://kynalabs.in/logo.png",
 "description": "Kyna Labs builds browser-native software products for businesses in India.",
 "address": {
   "@type": "PostalAddress",
   "addressLocality": "Hyderabad",
   "addressCountry": "IN"
 },
 "sameAs": [
   "https://linkedin.com/company/kynalabs",
   "https://twitter.com/kynalabs"
 ]
}
13. ANALYTICS EVENTS
13.1 Setup
Tool: Google Analytics 4
Implementation: next-ga4 or gtag via Next.js Script component
Tracking ID: G-XXXXXXXXXX (set via env var NEXT_PUBLIC_GA_ID)
13.2 Events to Track
Event NameTriggerParameterspage_viewEvery page loadpage_path, page_titlecta_clickAny CTA button clickcta_label, cta_location, destination_urlnav_clickNav link clickednav_item, nav_type (desktop/mobile)demo_form_startFirst interaction with demo formpage_pathdemo_form_submitDemo form submitted successfullybusiness_type, locationsdemo_form_errorDemo form submission failederror_typecontact_form_submitContact form submittedsubjectproduct_page_view/products/[slug] loadedproduct_nameuse_case_view/use-cases/[slug] loadeduse_casearticle_view/resources/[slug] loadedarticle_title, categorywaitlist_signupWaitlist form submittedproduct_interestdropdown_openNav dropdown openeddropdown_name
13.3 Implementation Helper
typescript// lib/analytics.ts
export function trackEvent(
 eventName: string,
 params?: Record<string, string | number>
) {
 if (typeof window === 'undefined') return;
 if (!window.gtag) return;
 window.gtag('event', eventName, params);
}
// Usage:
trackEvent('cta_click', {
 cta_label: 'Book a Demo',
 cta_location: 'hero',
 destination_url: '/book-demo',
});
14. CTA STRATEGY
14.1 Primary CTA
"Book a Demo" — appears in:
Global header (all pages, all times)
Hero section on Home
Hero section on TapEat product page
End of every use case page
End of every blog article
Footer (mobile only, as a bottom bar)
14.2 Secondary CTAs
CTA LabelWhereDestination"Explore Our Products"Home hero/products"Learn More"Product cards/products/tapeat"See how it works"TapEat hero#how-it-works (same page)"Join Waitlist"Future product card/contact"Read More"Blog card/resources/[slug]"Contact Us"About page/contact
14.3 CTA Placement Rules
1. Every page has at least one primary CTA visible above the fold.
2. Every page ends with a CTA section before the footer.
3. CTAs use action verbs: Book, See, Explore, Join, Read.
4. Never use "Click here" or "Learn more" as standalone text.
5. Primary CTA: filled button, brand purple.
6. Secondary CTA: outlined button or text link.
7. Maximum 2 CTAs side by side. Never 3.
15. ACCESSIBILITY REQUIREMENTS
15.1 Standards
Target: WCAG 2.1 Level AA
Testing tools: axe-core, Lighthouse, manual keyboard testing
15.2 Checklist
Color and Contrast:
□ Normal text: minimum 4.5:1 contrast ratio
□ Large text (18px+): minimum 3:1 ratio
□ UI components (buttons, inputs): 3:1 minimum
□ Purple #3B0764 on white: passes (check with tool)
Keyboard Navigation:
□ All interactive elements reachable via Tab key
□ Focus ring visible on all focusable elements (do not remove outline)
□ Dropdown menus closable with Escape key
□ Mobile menu closable with Escape key
□ Skip-to-content link at top of every page
Images:
□ All images have descriptive alt text
□ Decorative images: alt=""
□ Product screenshots: alt describes what is shown
Forms:
□ All inputs have associated <label>
□ Error messages programmatically associated with inputs (aria-describedby)
□ Required fields indicated (aria-required="true")
□ Form submission feedback announced to screen readers
ARIA:
□ Navigation landmark: <nav aria-label="Main navigation">
□ Main content: <main>
□ Footer: <footer>
□ Dropdown: aria-expanded, aria-haspopup on trigger
□ Mobile menu: aria-expanded on hamburger button
Responsive:
□ Text resizes correctly to 200% without horizontal scroll
□ No content lost when text size increased
16. TECHNICAL IMPLEMENTATION GUIDANCE
16.1 Tech Stack
LayerTechnologyVersionFrameworkNext.js App Router14+LanguageTypeScript5.4+ strictStylingTailwind CSSv3+UI componentsshadcn/ui (select components only)LatestIconsLucide React0.378+FontsNext.js Google Fonts (next/font/google)Built-inImagesnext/imageBuilt-inFormsReact Hook Form + ZodLatestEmail/form backendResend or Formspreev1AnalyticsGoogle Analytics 4 (gtag)LatestHostingVercelPro or Hobby
16.2 File Structure
kynalabs-website/
├── app/
│   ├── layout.tsx                  Root layout (Header + Footer)
│   ├── page.tsx                    Home
│   ├── about/page.tsx
│   ├── products/
│   │   ├── page.tsx                Products overview
│   │   └── [slug]/
│   │       └── page.tsx            Dynamic product page
│   ├── use-cases/
│   │   ├── page.tsx
│   │   └── [segment]/page.tsx
│   ├── resources/
│   │   ├── page.tsx
│   │   └── [slug]/page.tsx
│   ├── contact/page.tsx
│   ├── book-demo/page.tsx
│   ├── not-found.tsx
│   ├── sitemap.ts
│   ├── robots.ts
│   └── api/
│       ├── contact/route.ts
│       ├── book-demo/route.ts
│       └── waitlist/route.ts
│
├── components/                     Per Section 10.1
├── content/
│   ├── products.ts                 Product data (name, tagline, features)
│   ├── use-cases.ts                Use case data
│   ├── team.ts                     Team member data
│   └── articles/
│       ├── qr-ordering-india.md
│       └── reduce-wait-times.md
│
├── lib/
│   ├── analytics.ts
│   ├── validations.ts              Zod schemas for forms
│   └── utils.ts                    cn(), formatDate()
│
├── public/
│   ├── logo.svg
│   ├── og/                         OG images per page
│   └── images/
│
├── tokens/
│   ├── colors.ts
│   └── typography.ts
│
├── tailwind.config.ts
├── next.config.ts
└── .env.local
16.3 Environment Variables
bash# .env.local
# Analytics
NEXT_PUBLIC_GA_ID=G-XXXXXXXXXX
# App URL
NEXT_PUBLIC_SITE_URL=https://kynalabs.in
# Form handling (choose one)
RESEND_API_KEY=                    # If using Resend
CONTACT_EMAIL=hello@kynalabs.in   # Destination for form submissions
# Or use Formspree:
NEXT_PUBLIC_FORMSPREE_ID=          # If using Formspree
16.4 Content Data Pattern
typescript// content/products.ts
export type Product = {
 slug:        string;
 name:        string;
 tagline:     string;
 description: string;
 status:      'live' | 'coming-soon' | 'beta';
 features:    string[];
 href:        string;
};
export const products: Product[] = [
 {
   slug:        'tapeat',
   name:        'TapEat',
   tagline:     'QR-based browser ordering for restaurants and cafeterias',
   description: 'Customers scan, order, and pay in under 60 seconds. No app. No login.',
   status:      'live',
   features: [
     'No app download required',
     'UPI payment built-in',
     'Real-time kitchen dashboard',
     'Works on any mobile browser',
   ],
   href: '/products/tapeat',
 },
 {
   slug:        'coming-soon',
   name:        'Next Product',
   tagline:     'Something new is in development',
   description: "We're working on our next product. Join the waitlist.",
   status:      'coming-soon',
   features:    [],
   href:        '/contact',
 },
];
16.5 Form API Routes
typescript// app/api/book-demo/route.ts
import { z } from 'zod';
const DemoSchema = z.object({
 name:          z.string().min(2),
 email:         z.string().email(),
 phone:         z.string().min(10).max(13),
 businessName:  z.string().min(2),
 businessType:  z.enum(['restaurant','cafeteria','food-court','hotel','other']),
 locations:     z.enum(['1','2-5','6+']),
 hearAboutUs:   z.string().optional(),
 preferredTime: z.string().optional(),
});
export async function POST(req: Request) {
 const body = await req.json();
 const result = DemoSchema.safeParse(body);
 if (!result.success) {
   return Response.json(
     { error: 'Invalid form data', issues: result.error.issues },
     { status: 400 }
   );
 }
 // Send email via Resend or Formspree
 // Log to console in dev
 console.log('[Demo request]', result.data);
 return Response.json({ success: true });
}
16.6 Article Rendering
typescript// Use next-mdx-remote for .md files in /content/articles/
// Or use a simple fs.readFile approach for v1
// Article frontmatter structure:
---
title: "Article title"
slug: "article-slug"
excerpt: "One sentence excerpt"
category: "Industry | Product | How-To"
author: "Author Name"
authorTitle: "Co-founder, Kyna Labs"
date: "2025-04-01"
readTime: "5 min read"
---
17. ACCEPTANCE CRITERIA
17.1 Per-Page Acceptance Criteria
All pages:
Loads without console errors in Chrome and Safari
Passes Lighthouse accessibility score ≥ 90
All images have alt text
Meta title and description present and correct length
Canonical URL set
Responsive at 375px, 768px, 1280px viewport widths
No horizontal scroll at any breakpoint
All links resolve (no 404s)
All CTAs lead to correct destinations
Home:
H1 is present and contains company name or primary keyword
Product section shows TapEat card and future product card
Demo CTA button appears above the fold on mobile
Stats section shows correct data
TapEat product page:
Eyebrow "A Kyna Labs Product" present
Demo placeholder div present with correct data-note attribute
All 4 "how it works" steps visible
Features grid renders 6 features on desktop, stacked on mobile
Contact and Demo forms:
All required fields validated on submit
Error messages appear inline per field
Success state replaces form (no page reload)
POST to API route returns correct response
Keyboard-navigable (Tab through all fields)
Blog/Resources:
Index page shows 2+ articles
Article page renders markdown content
Sidebar sticky on desktop, inline on mobile
Related articles shown
17.2 Performance Targets
Lighthouse scores (mobile):
 Performance:    ≥ 85
 Accessibility:  ≥ 90
 Best Practices: ≥ 90
 SEO:            ≥ 90
Core Web Vitals:
 LCP < 2.5s
 FID < 100ms
 CLS < 0.1
Bundle:
 First load JS < 150KB (gzipped)
 CSS < 30KB (gzipped)
18. AI CODING HANDOFF INSTRUCTIONS
Read this section carefully before writing a single line of code.
18.1 What You Are Building
You are building a parent company marketing website for Kyna Labs. This is NOT a product application. It is a marketing and lead-generation website.
TapEat is one product featured on this site. The site exists to represent the company, not just TapEat. Future products will be added to the same site without requiring a redesign.
18.2 Non-Negotiable Rules
1. Stack: Next.js 14 App Router, TypeScript strict, Tailwind CSS v3.
  Do NOT substitute. Do not use Remix, Gatsby, Vite, or any other framework.
2. Content: Use the content/products.ts, content/use-cases.ts pattern.
  Do not hardcode content inside component JSX.
3. Components: Follow the component structure in Section 10.1 exactly.
  Do not merge or skip components.
4. Design tokens: Use the color and typography tokens in Section 9.
  Do not introduce new colors not in the token file.
5. TapEat demo: Do NOT build the interactive demo. Leave the placeholder
  div exactly as specified in Section 6.4.
6. Images: Use next/image for all images. Never use raw <img> tags.
7. Forms: Use React Hook Form + Zod for both contact and demo forms.
  Do not use uncontrolled inputs.
8. Analytics: Implement GA4 events per Section 13 exactly.
  Do not skip or rename events.
9. Accessibility: All WCAG 2.1 AA requirements in Section 15 are mandatory.
  Focus rings must not be removed.
10. Mobile-first: Write Tailwind classes mobile-first (base = mobile,
   sm/md/lg = enhancements). Never write desktop-only layouts.
18.3 Build Sequence
Build in this exact order. Confirm completion of each step before moving to the next.
Step 1: Project init + tokens + layout
Step 2: Shared components (Button, Badge, Card, Icon, Container)
Step 3: Header + Footer + Navigation (desktop + mobile)
Step 4: Home page (all sections)
Step 5: About page
Step 6: Products overview page
Step 7: TapEat product page
Step 8: Use cases (overview + 3 sub-pages)
Step 9: Resources (index + article template + 2 sample articles)
Step 10: Contact page + API route
Step 11: Book Demo page + API route
Step 12: 404 page
Step 13: Sitemap + robots.txt
Step 14: SEO metadata on all pages
Step 15: Analytics events
Step 16: Accessibility audit and fixes
Step 17: Lighthouse performance audit and fixes
18.4 Before You Start — Ask For
1. Company name (placeholder is "Kyna Labs" — confirm if different)
2. Domain name (for canonical URLs)
3. GA4 Measurement ID (for analytics)
4. Contact/Resend API key (for form handling)
5. Team member photos and bios (for About page)
6. Real vendor testimonial quotes (or confirm using stats only)
7. Logo SVG file (or confirm you should create a text wordmark placeholder)
------------------------------------
This is a marketing website for Kyna Labs, a B2B SaaS company.
TapEat is one of their products. The site must represent the
full company, not just TapEat.
BEFORE YOU START — ask me for:
1. Confirmed company name (default: Kyna Labs)
2. Domain name (for canonical URLs and OG tags)
3. GA4 Measurement ID
4. Email service preference: Resend or Formspree
5. Logo file or confirm text wordmark placeholder
STACK (locked — do not deviate):
- Next.js 14 App Router
- TypeScript strict mode
- Tailwind CSS v3
- React Hook Form + Zod for all forms
- Lucide React for icons
- next/font/google for Sora and Inter fonts
- next/image for all images
- Google Analytics 4 via gtag
DO NOT:
- Build the TapEat interactive demo (see Section 18.2)
- Use any other CSS framework
- Use raw <img> tags
- Hardcode content in component JSX
- Remove focus rings from interactive elements
- Create layouts that only work on desktop
BUILD IN THIS ORDER (confirm each step before proceeding):
Step 1:  Project init, tailwind.config.ts, color + type tokens,
        root layout.tsx with Header + Footer shells
Step 2:  All shared UI components (Button, Badge, Card, Icon, Container, Section)
Step 3:  Header (desktop nav + dropdowns + mobile hamburger menu)
Step 4:  Footer (4-column, responsive)
Step 5:  Home page — all sections per SDD Section 6.1
Step 6:  About page — all sections per SDD Section 6.2
Step 7:  Products overview page — per SDD Section 6.3
Step 8:  TapEat product page — per SDD Section 6.4
        (include demo placeholder div — do NOT build the demo)
Step 9:  Dynamic product page for future products (/products/[slug])
Step 10: Use cases overview + 3 sub-pages — per SDD Section 6.6
Step 11: Resources index + article template + 2 sample articles — Section 6.7
Step 12: Contact page + /api/contact route — Section 6.8
Step 13: Book Demo page + /api/book-demo route — Section 6.9
Step 14: 404 custom page
Step 15: app/sitemap.ts + app/robots.ts
Step 16: SEO metadata (generateMetadata) on all pages — Section 12
Step 17: Analytics events wired to all CTAs and forms — Section 13
Step 18: Accessibility audit: keyboard nav, focus rings, ARIA, alt text — Section 15
Step 19: Lighthouse audit. Fix until Performance ≥ 85, Accessibility ≥ 90 on mobile.
ACCEPTANCE:
At the end of each step, confirm:
- No TypeScript errors (npx tsc --noEmit)
- No console errors in browser
- Page renders correctly at 375px and 1280px
CONTENT:
- Use content/products.ts and content/use-cases.ts for all data
- Never hardcode product names or feature lists inside components
- Sample article content can be placeholder Lorem-style but must be
 structured correctly with frontmatter
DESIGN:
- Primary: #3B0764 (purple)
- Accent:  #F59E0B (amber)
- Font:    Sora (headings), Inter (body)
- Mobile-first Tailwind. Base styles = mobile.
Start by confirming you have read the SDD and listing the
5 items you need from me before writing code.
Reply "READY" when confirmed.
