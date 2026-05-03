PHASE 3 — CORE PAGES
Phase Objective

Implement complete content for all pages defined in SDD Sections 6.1–6.9. Every section of every page is built using Phase 2 components. Navigation interaction (dropdowns, mobile menu) is implemented in this phase. No forms have submit logic. No API calls. No analytics.

🔴 Company vs Product Positioning (MANDATORY)

The Kyna Labs website is a parent company website, not a single-product landing page.

Rules:
Homepage must be company-first
Describe Kyna Labs as a builder of browser-native software
Focus on operators in India
Focus on problems and solutions, not one product
TapEat must NOT dominate homepage
No TapEat-specific hero messaging on homepage
No product-specific language in opening section
Product-specific messaging belongs ONLY to:
/products/tapeat page
Homepage must include:
Company-level hero
Industry problem statement (not TapEat-specific)
Products section (TapEat as one product card)
General value propositions
Stats must be neutral or company-level
Avoid “TapEat-only” stats like “Restaurants using TapEat”
Use broader credibility or capability metrics
Future-ready structure
Homepage must support multiple products without redesign
Original SDD Sections Covered in Phase 3

(unchanged — keep your existing table here)

Original SDD Sections Deferred from Phase 3

(unchanged)

Phase 3 — Explicit Exclusions

(unchanged)

Phase 3 — Build Order
Step 1 — Complete Navigation

(unchanged)

Step 2 — Home Page (app/page.tsx)

Build all 8 sections from SDD Section 6.1 in order:

⚠️ IMPORTANT MODIFICATION (POSITIONING FIX)
HERO section must be company-level, NOT TapEat-specific
Replace any TapEat-specific messaging with company positioning
Correct Hero Direction:
Browser-native software
India-first operators
No app downloads
Instant usability

Sections:

HERO section (company-first, NOT TapEat-first)
PROBLEM STATEMENT (industry-wide, not product-specific)
PRODUCTS section (TapEat + future product card)
USE CASES strip
SOCIAL PROOF / TRACTION (neutral stats)
HOW IT WORKS (generic capability explanation)
COMPANY INTRO strip
FINAL CTA
Step 3 — TapEat Product Page

(app/products/tapeat/page.tsx)

(unchanged — this is where TapEat messaging belongs)

Step 4 — Products Overview Page

(unchanged)

Step 5 — About Page

(unchanged)

Step 6 — Use Cases Pages

(unchanged)

Step 7 — Resources Pages

(unchanged)

Step 8 — Contact Page

(unchanged)

Step 9 — Book Demo Page

(unchanged)

Step 10 — Future Product Placeholder

(unchanged)

Step 11 — Footer

(unchanged)

Step 12 — Custom 404 Page

(unchanged)

Phase 3 — Acceptance Criteria
🆕 AC-3.0 — Positioning (NEW)

□ Homepage hero is company-level, not TapEat-specific
□ TapEat is presented only inside Products section on homepage
□ No TapEat-specific messaging in first fold of homepage
□ TapEat product page contains full product-specific messaging
□ Homepage supports future products without redesign

AC-3.1 — All pages render

(unchanged)

AC-3.2 — Navigation

(unchanged)

AC-3.3 — CTA strategy

(unchanged)

AC-3.4 — Content accuracy

⚠️ UPDATE:

□ Home hero H1 must reflect company positioning, not TapEat-specific copy

(keep rest unchanged)

AC-3.5 — Responsive

(unchanged)

AC-3.6 — TypeScript

(unchanged)
