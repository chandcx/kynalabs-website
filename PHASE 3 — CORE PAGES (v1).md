PHASE 3 — CORE PAGES
Phase Objective
Implement complete content for all pages defined in SDD Sections 6.1–6.9. Every section of every page is built using Phase 2 components. Navigation interaction (dropdowns, mobile menu) is implemented in this phase. No forms have submit logic. No API calls. No analytics.

Original SDD Sections Covered in Phase 3
SectionWhat is implementedSection 6.1 — Home pageAll 8 sections fully builtSection 6.2 — About pageAll sections fully builtSection 6.3 — Products overview pageAll sections fully builtSection 6.4 — TapEat product pageAll sections, including demo placeholder divSection 6.5 — Future product placeholder pageDynamic route with Coming Soon patternSection 6.6 — Use cases pagesOverview + all 3 sub-pagesSection 6.7 — Resources / BlogIndex + article template + 2 sample articlesSection 6.8 — Contact pagePage layout and form structure (no submission)Section 6.9 — Book Demo pagePage layout and form structure (no submission)Section 7.1–7.2 — Navigation dropdowns and mobile menuFull interaction implementedSection 7.3 — Footer with full column layoutComplete implementationSection 8.1–8.2 — Content hierarchy rulesApplied to all heading levelsSection 4.3 — Image directionPlaceholder images with correct dimensionsSection 11 — Responsive layout transformationsAll tables applied to pagesSection 14 — CTA strategy (placement and wiring)All CTAs placed, hrefs correctSection 4.1 — Brand voice copyAll copy written per brand voice guidelines
Original SDD Sections Deferred from Phase 3
SectionDeferred ToSection 17 — Form submission logic and API routesPhase 4Section 12 — SEO metadata (generateMetadata)Phase 5Section 13 — Analytics event callsPhase 5Section 15 — Full accessibility auditPhase 5Section 16.5 — Form API routesPhase 4TapEat interactive demoSeparate SDD (never in this document)

Phase 3 — Explicit Exclusions
DO NOT BUILD IN PHASE 3:

❌ Form submission handlers (forms render but submit does nothing)
❌ API routes (/api/contact, /api/book-demo, /api/waitlist)
❌ generateMetadata on any page
❌ Analytics event calls (trackEvent()) inside any component
❌ JSON-LD structured data scripts
❌ Sitemap or robots.txt
❌ Interactive TapEat demo (leave placeholder div as specified)
❌ Real images (use next/image with placeholder /images/ paths)
❌ Loading states or error states for forms

Phase 3 — Build Order
Build pages strictly in this order. Each page must render without errors before building the next.
Step 1 — Complete Navigation
Update Header.tsx with full dropdown interaction and mobile hamburger menu. This requires 'use client' on the navigation component only.
typescript// components/navigation/MobileMenu.tsx
'use client';
// Full slide-in menu — toggle logic implemented here
// Keyboard: Escape closes menu
// All links from SDD Section 7.1
typescript// components/navigation/Dropdown.tsx
'use client';
// Hover/click dropdown — products and use-cases
// Links per SDD Section 7.2
// Escape key closes dropdown
// aria-expanded, aria-haspopup per SDD Section 15
Step 2 — Home Page (app/page.tsx)
Build all 8 sections from SDD Section 6.1 in order:
1. HERO section
2. PROBLEM STATEMENT strip (dark background)
3. PRODUCTS section (TapEat card + Future product card)
4. USE CASES strip (3 tiles)
5. SOCIAL PROOF / TRACTION (stats row)
6. HOW IT WORKS (3 steps)
7. COMPANY INTRO strip
8. FINAL CTA section (purple background)
All content from SDD Section 6.1 must be present verbatim.
Step 3 — TapEat Product Page (app/products/tapeat/page.tsx)
Build all sections from SDD Section 6.4. This is the second most important page after home.
Include the demo placeholder div exactly as specified:
typescript{/* app/products/tapeat/page.tsx — demo placeholder */}
<div
  id="tapeat-demo-placeholder"
  data-note="Interactive demo injected from demo-sdd build"
  className="w-full min-h-[400px] bg-neutral-border/20 rounded-card flex items-center justify-center"
>
  <p className="text-neutral-gray text-small">
    Interactive demo — see TapEat Demo SDD
  </p>
</div>
Step 4 — Products Overview Page (app/products/page.tsx)
All sections from SDD Section 6.3.
Step 5 — About Page (app/about/page.tsx)
All sections from SDD Section 6.2.
Step 6 — Use Cases Pages
Build in this order:

app/use-cases/page.tsx — overview with 3 cards
app/use-cases/restaurants/page.tsx
app/use-cases/cafeterias/page.tsx
app/use-cases/food-courts/page.tsx

All sub-pages follow the template in SDD Section 6.6.
Step 7 — Resources Pages
Build in this order:

app/resources/page.tsx — index with article grid
app/resources/[slug]/page.tsx — article template
Content: render the 2 articles from content/articles/index.ts

For article content in v1, create markdown-equivalent content as TypeScript string constants. Do not install a markdown parser in Phase 3.
typescript// content/articles/qr-ordering-india.ts
export const qrOrderingIndiaContent = `
  <p>Most software assumes your customers have time, fast internet,
  and the patience to download an app. In India, that assumption
  fails constantly...</p>
  <!-- Full article content here -->
`;
Step 8 — Contact Page (app/contact/page.tsx)
Form structure from SDD Section 6.8. Fields rendered. No submit logic.
Step 9 — Book Demo Page (app/book-demo/page.tsx)
Form structure from SDD Section 6.9. Fields rendered. No submit logic.
Step 10 — Future Product Placeholder
Update app/products/[slug]/page.tsx:
typescriptimport { products } from '@/content/products';

export default function ProductPage({ params }: { params: { slug: string } }) {
  const product = products.find(p => p.slug === params.slug);

  // Known product — render product page
  if (product && product.status === 'live') {
    // This only applies to tapeat for now
    // tapeat has its own page at /products/tapeat
    // This catches future live products
    return <main><h1>{product.name}</h1></main>;
  }

  // Unknown slug — Coming Soon page
  return (
    <main>
      <h1>This product is on its way</h1>
      <p>We're building something new. Leave your email and we'll let you know when it's ready.</p>
      {/* Waitlist form structure — no submit logic until Phase 4 */}
    </main>
  );
}
Step 11 — Complete Footer
Update Footer.tsx with full 4-column layout, social icons, and all links per SDD Section 7.3.
Step 12 — Custom 404 Page
typescript// app/not-found.tsx — complete implementation

Phase 3 — Acceptance Criteria
AC-3.1 — All pages render
□ / loads with all 8 sections populated with content
□ /about loads with all sections
□ /products loads with TapEat card and future product card
□ /products/tapeat loads with all sections and demo placeholder div
□ /products/unknown-slug loads the Coming Soon page
□ /use-cases loads with 3 tiles
□ /use-cases/restaurants loads with full content
□ /use-cases/cafeterias loads with full content
□ /use-cases/food-courts loads with full content
□ /resources loads with 2 article cards
□ /resources/qr-ordering-india loads article content
□ /resources/reduce-wait-times-restaurant loads article content
□ /contact loads with form structure (no submit logic)
□ /book-demo loads with form structure (no submit logic)
AC-3.2 — Navigation
□ Desktop Products dropdown opens and shows TapEat link
□ Desktop Use Cases dropdown opens and shows 3 links
□ Mobile hamburger opens slide-in menu
□ Mobile menu has all nav links
□ Escape key closes both dropdowns and mobile menu
□ "Book a Demo" button in header links to /book-demo
□ All footer links resolve correctly
AC-3.3 — CTA strategy (SDD Section 14)
□ "Book a Demo" CTA visible above the fold on Home on mobile
□ Every page ends with a CTA section before footer
□ No CTA uses text "Click here" or "Learn more" standalone
□ Primary CTAs use filled purple button
□ Demo placeholder div has id="tapeat-demo-placeholder"
   and data-note attribute exactly as specified
AC-3.4 — Content accuracy
□ Home hero H1 present and matches SDD exactly
□ TapEat product page eyebrow "A Kyna Labs Product" present
□ How it works section has exactly 4 steps on TapEat page
□ Features section has exactly 6 features on TapEat page
□ Stats row shows 3 figures on Home and Book Demo pages
□ Article pages show author name, date, read time, category
□ Sidebar shows on article page (desktop), inline (mobile)
AC-3.5 — Responsive
□ Home page tested at 375px — all sections visible, no horizontal scroll
□ Navigation hamburger appears at < 768px, sidebar at ≥ 1024px
□ Product card grid: 1 col mobile, 2 col desktop
□ Feature grid: 1 col mobile, 2 col tablet, 3 col desktop
□ Stats row: 2×2 grid mobile, 4-column desktop
□ Article sidebar: inline mobile, sticky at 30% on desktop
AC-3.6 — TypeScript
bashnpx tsc --noEmit   # 0 errors
npm run build      # succeeds
