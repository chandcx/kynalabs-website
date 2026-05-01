PHASE 5 — SEO, ANALYTICS AND PERFORMANCE
Phase Objective
Complete all SEO metadata, wire Google Analytics 4 with all events from SDD Section 13, conduct the full accessibility audit from SDD Section 15, generate sitemap and robots.txt, implement structured data, and optimise for Core Web Vitals targets.

Original SDD Sections Covered in Phase 5
SectionWhat is implementedSection 12 — SEO requirementsAll generateMetadata calls on all pagesSection 12.2 — Per-page metadata tableTitle, description, OG, Twitter on all 13 pagesSection 12.3 — Technical SEOSitemap, robots, canonical URLs, structured dataSection 12.4 — JSON-LD Organization schemaHome and About pagesSection 13 — All analytics eventsFull GA4 wiring for all 15 event typesSection 13.1–13.3 — Analytics setupgtag setup, trackEvent implementationSection 15 — Accessibility requirementsFull WCAG 2.1 AA audit and fixesSection 15.1 — Standardsaxe-core test run, Lighthouse auditSection 15.2 — Accessibility checklistAll 25+ checklist items verifiedSection 10.2 — Core Web VitalsPerformance optimisation until targets metSection 17 — Acceptance criteria (performance)Lighthouse scores verifiedSection 4.3 — OG imagesStatic OG images per page (1200×630px)
Nothing deferred from Phase 5
Phase 5 completes the full original SDD. After Phase 5, the website matches the complete specification in parent_website_sdd_v1.md.

Phase 5 — Explicit Exclusions
DO NOT BUILD IN PHASE 5:

❌ New pages or new features
❌ Changes to page content or copy
❌ The TapEat interactive demo (separate SDD — never in this document)
❌ CMS integration (content remains hardcoded as per original SDD v1 scope)
❌ New npm packages beyond what is specified below
❌ A/B testing (explicitly out of scope per SDD Section 2.2)
❌ Multi-language support (explicitly out of scope per SDD Section 2.2)
❌ Careers page (explicitly deferred to v2 per SDD Section 2.2)

Phase 5 — Build Step 1: Dependency Addition
bash# Only if not using next/script for gtag:
# No new packages required for Phase 5.
# GA4 uses next/script + gtag pattern (built into Next.js).

Phase 5 — Build Step 2: GA4 Setup and Full Analytics Wiring
app/layout.tsx — Add GA4 script
typescript// app/layout.tsx — Phase 5 update (analytics)
import Script from 'next/script';

const GA_ID = process.env.NEXT_PUBLIC_GA_ID;

// Inside <head> (via Next.js metadata or Script component):
{GA_ID && (
  <>
    <Script
      src={`https://www.googletagmanager.com/gtag/js?id=${GA_ID}`}
      strategy="afterInteractive"
    />
    <Script id="ga4-init" strategy="afterInteractive">
      {`
        window.dataLayer = window.dataLayer || [];
        function gtag(){dataLayer.push(arguments);}
        gtag('js', new Date());
        gtag('config', '${GA_ID}', { page_path: window.location.pathname });
      `}
    </Script>
  </>
)}
lib/analytics.ts — Full Implementation
typescript// lib/analytics.ts — Phase 5 full implementation
// Replaces the Phase 4 stub

type GTagEvent = {
  action: string;
  params?: Record<string, string | number | boolean>;
};

declare global {
  interface Window {
    gtag: (...args: unknown[]) => void;
  }
}

export function trackEvent(
  eventName: string,
  params?: Record<string, string | number>
) {
  if (typeof window === 'undefined') return;
  if (typeof window.gtag !== 'function') return;
  window.gtag('event', eventName, params);
}

// Named event helpers per SDD Section 13.2:
export const analytics = {
  pageView:         (path: string, title: string) =>
    trackEvent('page_view', { page_path: path, page_title: title }),

  ctaClick:         (label: string, location: string, dest: string) =>
    trackEvent('cta_click', { cta_label: label, cta_location: location, destination_url: dest }),

  navClick:         (item: string, type: 'desktop' | 'mobile') =>
    trackEvent('nav_click', { nav_item: item, nav_type: type }),

  demoFormStart:    (path: string) =>
    trackEvent('demo_form_start', { page_path: path }),

  demoFormSubmit:   (businessType: string, locations: string) =>
    trackEvent('demo_form_submit', { business_type: businessType, locations }),

  demoFormError:    (errorType: string) =>
    trackEvent('demo_form_error', { error_type: errorType }),

  contactFormSubmit:(subject: string) =>
    trackEvent('contact_form_submit', { subject }),

  productPageView:  (productName: string) =>
    trackEvent('product_page_view', { product_name: productName }),

  useCaseView:      (useCase: string) =>
    trackEvent('use_case_view', { use_case: useCase }),

  articleView:      (title: string, category: string) =>
    trackEvent('article_view', { article_title: title, category }),

  waitlistSignup:   (productInterest: string) =>
    trackEvent('waitlist_signup', { product_interest: productInterest }),

  dropdownOpen:     (name: string) =>
    trackEvent('dropdown_open', { dropdown_name: name }),
};
Wire analytics to all CTA buttons and navigation
Update Button.tsx to accept an optional analyticsEvent prop.
Update NavLink.tsx and Dropdown.tsx to call analytics.navClick() and analytics.dropdownOpen().
Update all product pages, use case pages, and article pages to call the appropriate page-view event on mount.

Phase 5 — Build Step 3: SEO Metadata on All Pages
Implement generateMetadata export on every page file per SDD Section 12.2.
typescript// Pattern for every page (using Home as example):
// app/page.tsx

import type { Metadata } from 'next';

export const metadata: Metadata = {
  title:       'Kyna Labs — Software Built for Real Businesses',
  description: 'Kyna Labs builds browser-native software products for restaurants, cafeterias, and beyond. No app downloads. No friction.',
  openGraph: {
    title:       'Kyna Labs — Software Built for Real Businesses',
    description: 'Browser-native products for operators in India.',
    url:         'https://kynalabs.in',
    siteName:    'Kyna Labs',
    images: [{
      url:    '/og/home-og.png',
      width:  1200,
      height: 630,
    }],
    locale: 'en_IN',
    type:   'website',
  },
  twitter: {
    card:        'summary_large_image',
    title:       'Kyna Labs — Software Built for Real Businesses',
    description: 'Browser-native products for operators in India.',
    images:      ['/og/home-og.png'],
  },
  alternates: {
    canonical: 'https://kynalabs.in',
  },
};
Apply to all 13 pages per the metadata table in SDD Section 12.2.

Phase 5 — Build Step 4: Sitemap and Robots
typescript// app/sitemap.ts
import type { MetadataRoute } from 'next';

const BASE = process.env.NEXT_PUBLIC_SITE_URL ?? 'https://kynalabs.in';

export default function sitemap(): MetadataRoute.Sitemap {
  return [
    { url: BASE,                                  lastModified: new Date(), changeFrequency: 'weekly',  priority: 1.0 },
    { url: `${BASE}/about`,                       lastModified: new Date(), changeFrequency: 'monthly', priority: 0.8 },
    { url: `${BASE}/products`,                    lastModified: new Date(), changeFrequency: 'weekly',  priority: 0.9 },
    { url: `${BASE}/products/tapeat`,             lastModified: new Date(), changeFrequency: 'weekly',  priority: 0.95 },
    { url: `${BASE}/use-cases`,                   lastModified: new Date(), changeFrequency: 'monthly', priority: 0.7 },
    { url: `${BASE}/use-cases/restaurants`,       lastModified: new Date(), changeFrequency: 'monthly', priority: 0.8 },
    { url: `${BASE}/use-cases/cafeterias`,        lastModified: new Date(), changeFrequency: 'monthly', priority: 0.8 },
    { url: `${BASE}/use-cases/food-courts`,       lastModified: new Date(), changeFrequency: 'monthly', priority: 0.8 },
    { url: `${BASE}/resources`,                   lastModified: new Date(), changeFrequency: 'weekly',  priority: 0.7 },
    { url: `${BASE}/resources/qr-ordering-india`, lastModified: new Date(), changeFrequency: 'monthly', priority: 0.6 },
    { url: `${BASE}/resources/reduce-wait-times-restaurant`, lastModified: new Date(), changeFrequency: 'monthly', priority: 0.6 },
    { url: `${BASE}/contact`,                     lastModified: new Date(), changeFrequency: 'yearly',  priority: 0.6 },
    { url: `${BASE}/book-demo`,                   lastModified: new Date(), changeFrequency: 'monthly', priority: 0.9 },
  ];
}
typescript// app/robots.ts
import type { MetadataRoute } from 'next';

export default function robots(): MetadataRoute.Robots {
  return {
    rules: {
      userAgent: '*',
      allow:     '/',
      disallow:  ['/api/'],
    },
    sitemap: `${process.env.NEXT_PUBLIC_SITE_URL}/sitemap.xml`,
  };
}

Phase 5 — Build Step 5: Structured Data (JSON-LD)
typescript// components/seo/OrganizationSchema.tsx
// Added to app/layout.tsx and app/about/page.tsx

export function OrganizationSchema() {
  const schema = {
    '@context':   'https://schema.org',
    '@type':      'Organization',
    'name':       'Kyna Labs',
    'url':        'https://kynalabs.in',
    'logo':       'https://kynalabs.in/logo.png',
    'description':'Kyna Labs builds browser-native software products for businesses in India.',
    'address': {
      '@type':          'PostalAddress',
      'addressLocality':'Hyderabad',
      'addressCountry': 'IN',
    },
    'sameAs': [
      'https://linkedin.com/company/kynalabs',
      'https://twitter.com/kynalabs',
    ],
  };

  return (
    <script
      type="application/ld+json"
      dangerouslySetInnerHTML={{ __html: JSON.stringify(schema) }}
    />
  );
}
typescript// components/seo/SoftwareAppSchema.tsx
// Added to app/products/tapeat/page.tsx

export function SoftwareAppSchema() {
  const schema = {
    '@context':       'https://schema.org',
    '@type':          'SoftwareApplication',
    'name':           'TapEat',
    'applicationCategory': 'BusinessApplication',
    'operatingSystem':'Web Browser',
    'description':    'QR-based browser ordering for restaurants and cafeterias in India.',
    'offers': {
      '@type':    'Offer',
      'priceCurrency': 'INR',
    },
  };

  return (
    <script
      type="application/ld+json"
      dangerouslySetInnerHTML={{ __html: JSON.stringify(schema) }}
    />
  );
}

Phase 5 — Build Step 6: OG Images
Create static OG images in /public/og/ for all pages:
home-og.png
about-og.png
products-og.png
tapeat-og.png
use-cases-og.png
resources-og.png
contact-og.png
book-demo-og.png
Each: 1200×630px, Kyna Labs brand colors, page title text. Create as static PNG files.

Phase 5 — Build Step 7: Full Accessibility Audit
Work through every item in SDD Section 15.2:
Color and Contrast:
□ Run Lighthouse → verify all text passes contrast ratios
□ Verify #3B0764 on white passes 4.5:1 (it does: ~12:1)
□ Verify amber #F59E0B on white passes for large text (3:1)
□ Verify all form input borders pass 3:1 against background

Keyboard Navigation:
□ Tab through every page — all interactive elements reachable
□ Focus ring visible on Header nav links
□ Focus ring visible on all Buttons
□ Focus ring visible on all form inputs
□ Dropdowns close with Escape key (verified in Phase 3, re-audit)
□ Mobile menu closes with Escape key
□ Skip-to-content link: add at top of Header

  
    href="#main-content"
    className="sr-only focus:not-sr-only focus:absolute focus:top-4 focus:left-4
               bg-brand-purple text-white px-4 py-2 rounded-DEFAULT z-50"
  >
    Skip to content
  </a>

□ Add id="main-content" to <main> in root layout

Images:
□ Audit every <Image> component — all have descriptive alt text
□ Decorative images: alt=""
□ Product screenshots: alt describes content shown
□ Team photos: alt="[Name], [Title]"

Forms:
□ All inputs have associated <label> (verified in Phase 4, re-audit)
□ Required fields: aria-required="true" added to all required inputs
□ Error messages: aria-describedby linking input to error paragraph
□ Form success state: role="alert" aria-live="polite"

ARIA:
□ <nav aria-label="Main navigation"> on Header
□ <nav aria-label="Footer navigation"> on Footer
□ <main id="main-content"> in root layout
□ <footer> landmark present
□ Dropdowns: aria-expanded on trigger button
□ Mobile menu: aria-expanded on hamburger button

Responsive text:
□ Test at 200% browser zoom — no horizontal scroll, no content loss

Phase 5 — Build Step 8: Performance Optimisation
□ Run Lighthouse mobile audit on all pages
□ Fix until all pages reach:
    Performance ≥ 85
    Accessibility ≥ 90
    Best Practices ≥ 90
    SEO ≥ 90

Common fixes to apply:
□ next/image: add sizes prop to all images
   sizes="(max-width: 768px) 100vw, (max-width: 1200px) 50vw, 33vw"
□ next/image: set priority prop on above-the-fold images (hero images)
□ Verify first load JS < 150KB gzipped
   Run: npm run build — check .next/analyze output
□ Verify no layout shifts (CLS < 0.1):
   Add explicit width/height to all images
□ Verify LCP < 2.5s:
   Hero image must have priority={true}
   Font-display: swap already set via next/font

Phase 5 — Acceptance Criteria
AC-5.1 — SEO metadata
□ All 13 pages have title tags matching SDD Section 12.2
□ All 13 pages have meta descriptions ≤ 155 characters
□ All 13 pages have canonical URLs
□ All 13 pages have OpenGraph title, description, image
□ All 13 pages have Twitter card metadata
□ /sitemap.xml returns 200 and lists all 13 pages
□ /robots.txt returns 200 and allows all except /api/
□ Organization JSON-LD present on Home and About pages
□ SoftwareApplication JSON-LD present on TapEat product page
AC-5.2 — Analytics
□ GA4 script loads on all pages (when NEXT_PUBLIC_GA_ID is set)
□ page_view fires on every route change
□ cta_click fires when any CTA button is clicked
□ demo_form_start fires on first field focus in demo form
□ demo_form_submit fires on successful demo submission
□ product_page_view fires on /products/tapeat page load
□ use_case_view fires on each /use-cases/[segment] page load
□ article_view fires on each /resources/[slug] page load
□ All 15 event types from SDD Section 13.2 verified in GA4 DebugView
AC-5.3 — Accessibility (full audit)
□ Lighthouse accessibility score ≥ 90 on all pages
□ axe-core: 0 critical violations on all pages
□ Skip-to-content link functional (Tab from browser URL bar)
□ Full keyboard navigation on every page without mouse
□ All images have alt text (verified by Lighthouse)
□ All form inputs have labels (verified by axe-core)
□ Focus rings visible on all interactive elements
□ aria-expanded on all dropdowns and mobile menu
AC-5.4 — Performance
□ Lighthouse Performance ≥ 85 on mobile for all pages
□ LCP < 2.5s on Home and TapEat product pages
□ CLS < 0.1 on all pages
□ First load JS < 150KB (gzipped)
AC-5.5 — Final build
bashnpx tsc --noEmit   # 0 errors
npm run build      # succeeds with 0 errors and 0 warnings
