PHASE 1 — FOUNDATION
Phase Objective
Establish a compilable, deployable Next.js project with correct routing, root layout, global navigation shell, footer shell, and static page stubs. Every route must resolve. No content, no styling beyond defaults, no forms, no analytics.

Original SDD Sections Covered in Phase 1
SectionWhat is implementedSection 16.2 — File structureFull folder and file scaffold created as stubsSection 5.1 — Site mapAll routes created and resolvingSection 7 — Navigation model (structure only)Header and footer shells, link structureSection 16.1 — Tech stackProject initialised with correct packagesSection 16.3 — Environment variables.env.local and .env.example created
Original SDD Sections Deferred from Phase 1
SectionDeferred ToSection 9 — Design system (colors, typography, tokens)Phase 2Section 10 — Reusable component libraryPhase 2Section 6.1–6.9 — All page content and sectionsPhase 3Section 7 — Dropdown menus, mobile hamburger interactionPhase 3Section 12 — SEO metadataPhase 5Section 13 — Analytics eventsPhase 5Section 14 — CTA strategy (content and wiring)Phase 3Section 15 — Accessibility (full audit)Phase 5Section 17 — Forms and API routesPhase 4Section 4 — Brand voice copyPhase 3

Phase 1 Scope
What you are building:
A compilable Next.js 14 App Router project with TypeScript strict mode, Tailwind CSS, correct folder structure, root layout with placeholder header and footer, and stub pages for every route defined in the site map.
What "stub page" means:
A page file that exports a default React component returning a single <main> element with an <h1> containing the page name. No other content. No styling beyond what Tailwind base reset applies automatically.

Phase 1 — Explicit Exclusions
DO NOT BUILD IN PHASE 1:

❌ Color tokens or design system files
❌ Any reusable UI components (Button, Card, Badge, etc.)
❌ Page content (no hero sections, no copy, no images)
❌ Dropdown menus or mobile hamburger menu logic
❌ Any form elements or form validation
❌ API routes
❌ Analytics or tracking scripts
❌ SEO metadata (no generateMetadata calls)
❌ Structured data / JSON-LD
❌ Font loading (beyond Tailwind defaults)
❌ Open Graph images
❌ Sitemap or robots.txt generation
❌ Content data files (products.ts, use-cases.ts, etc.)
❌ Any useState, useEffect, or client-side interactivity
❌ Environment variable validation logic
❌ Any 'use client' directives (all pages are server components at this stage)

Phase 1 — Package Setup
Install exactly these packages. No others.
bashnpx create-next-app@latest kynalabs-website \
  --typescript \
  --tailwind \
  --eslint \
  --app \
  --src-dir=false \
  --import-alias="@/*"

# After scaffold:
npm install lucide-react
npm install -D @types/node
Verify tsconfig.json has strict mode:
json{
  "compilerOptions": {
    "strict": true,
    "noUncheckedIndexedAccess": true
  }
}
Verify tailwind.config.ts exists and content array includes all app paths:
typescriptcontent: [
  './app/**/*.{ts,tsx}',
  './components/**/*.{ts,tsx}',
  './content/**/*.{ts,tsx}',
],

Phase 1 — Complete File Scaffold
Create every file listed below. Files marked [stub] contain only the minimal content described in the stub definition above.
kynalabs-website/
│
├── app/
│   ├── layout.tsx                     [ROOT LAYOUT — see spec below]
│   ├── page.tsx                       [stub: "Home"]
│   ├── not-found.tsx                  [stub: "Page Not Found"]
│   ├── about/
│   │   └── page.tsx                   [stub: "About"]
│   ├── products/
│   │   ├── page.tsx                   [stub: "Products"]
│   │   └── [slug]/
│   │       └── page.tsx               [stub: "Product: [slug]"]
│   ├── use-cases/
│   │   ├── page.tsx                   [stub: "Use Cases"]
│   │   ├── restaurants/
│   │   │   └── page.tsx               [stub: "Use Cases: Restaurants"]
│   │   ├── cafeterias/
│   │   │   └── page.tsx               [stub: "Use Cases: Cafeterias"]
│   │   └── food-courts/
│   │       └── page.tsx               [stub: "Use Cases: Food Courts"]
│   ├── resources/
│   │   ├── page.tsx                   [stub: "Resources"]
│   │   └── [slug]/
│   │       └── page.tsx               [stub: "Article: [slug]"]
│   ├── contact/
│   │   └── page.tsx                   [stub: "Contact"]
│   └── book-demo/
│       └── page.tsx                   [stub: "Book a Demo"]
│
├── components/
│   ├── layout/
│   │   ├── Header.tsx                 [shell — see spec below]
│   │   └── Footer.tsx                 [shell — see spec below]
│   └── navigation/
│       └── NavLink.tsx                [shell — see spec below]
│
├── public/
│   └── placeholder-logo.svg           [simple SVG text: "Kyna Labs"]
│
├── .env.local                         [see spec below]
├── .env.example                       [see spec below]
└── README.md                          [minimal: "Kyna Labs Website — see SDD"]

Phase 1 — Component Specifications
app/layout.tsx — Root Layout
typescript// app/layout.tsx
// Phase 1: Root layout with header and footer shells.
// No fonts, no custom colors, no analytics, no metadata.

import { Header } from '@/components/layout/Header';
import { Footer } from '@/components/layout/Footer';
import './globals.css';

export default function RootLayout({
  children,
}: {
  children: React.ReactNode;
}) {
  return (
    <html lang="en">
      <body>
        <Header />
        <main>{children}</main>
        <Footer />
      </body>
    </html>
  );
}
components/layout/Header.tsx — Header Shell
typescript// components/layout/Header.tsx
// Phase 1: Navigation link structure only.
// No dropdown logic, no mobile menu, no styling beyond defaults.
// All routes from SDD Section 5.1 must be linked here.

import Link from 'next/link';
import { NavLink } from '@/components/navigation/NavLink';

export function Header() {
  return (
    <header>
      <nav aria-label="Main navigation">
        <Link href="/">Kyna Labs</Link>
        <ul>
          <li><NavLink href="/products">Products</NavLink></li>
          <li><NavLink href="/use-cases">Use Cases</NavLink></li>
          <li><NavLink href="/resources">Resources</NavLink></li>
          <li><NavLink href="/about">About</NavLink></li>
          <li><NavLink href="/book-demo">Book a Demo</NavLink></li>
        </ul>
      </nav>
    </header>
  );
}
components/layout/Footer.tsx — Footer Shell
typescript// components/layout/Footer.tsx
// Phase 1: All footer links present per SDD Section 7.3.
// No column layout, no icons, no styling.

import Link from 'next/link';

export function Footer() {
  return (
    <footer>
      {/* Products column */}
      <Link href="/products">Products</Link>
      <Link href="/products/tapeat">TapEat</Link>

      {/* Company column */}
      <Link href="/about">About</Link>
      <Link href="/contact">Contact</Link>
      <Link href="/resources">Resources</Link>

      {/* Legal column */}
      <Link href="/privacy">Privacy Policy</Link>
      <Link href="/terms">Terms of Service</Link>

      {/* Use cases */}
      <Link href="/use-cases/restaurants">Restaurants</Link>
      <Link href="/use-cases/cafeterias">Cafeterias</Link>
      <Link href="/use-cases/food-courts">Food Courts</Link>

      <p>© 2025 Kyna Labs. All rights reserved.</p>
    </footer>
  );
}
components/navigation/NavLink.tsx — Nav Link
typescript// components/navigation/NavLink.tsx
// Phase 1: Basic link wrapper. No active state logic yet.

import Link from 'next/link';

type NavLinkProps = {
  href: string;
  children: React.ReactNode;
};

export function NavLink({ href, children }: NavLinkProps) {
  return <Link href={href}>{children}</Link>;
}
Stub Page Pattern (apply to all stub pages)
typescript// Example: app/about/page.tsx
// All stub pages follow this exact pattern.

export default function AboutPage() {
  return (
    <main>
      <h1>About</h1>
    </main>
  );
}
Dynamic Route Stubs
typescript// app/products/[slug]/page.tsx
type Props = { params: { slug: string } };

export default function ProductPage({ params }: Props) {
  return (
    <main>
      <h1>Product: {params.slug}</h1>
    </main>
  );
}
typescript// app/resources/[slug]/page.tsx
type Props = { params: { slug: string } };

export default function ArticlePage({ params }: Props) {
  return (
    <main>
      <h1>Article: {params.slug}</h1>
    </main>
  );
}

Phase 1 — Environment Files
bash# .env.local (gitignored)
NEXT_PUBLIC_SITE_URL=http://localhost:3000
NEXT_PUBLIC_GA_ID=
RESEND_API_KEY=
CONTACT_EMAIL=hello@kynalabs.in
bash# .env.example (committed)
NEXT_PUBLIC_SITE_URL=https://kynalabs.in
NEXT_PUBLIC_GA_ID=G-XXXXXXXXXX
RESEND_API_KEY=
CONTACT_EMAIL=hello@kynalabs.in

Phase 1 — Acceptance Criteria
Run all of these checks before declaring Phase 1 complete.
AC-1.1 — Build and compile
bashnpx tsc --noEmit        # Must: 0 errors
npm run build           # Must: succeeds with 0 errors
npm run dev             # Must: starts without errors
AC-1.2 — Route resolution
Open each URL in a browser at localhost:3000. Every route must return a 200 status with a rendered <h1>:
/ ...................... "Home"
/about ................. "About"
/products .............. "Products"
/products/tapeat ....... "Product: tapeat"
/products/anything ..... "Product: anything"
/use-cases ............. "Use Cases"
/use-cases/restaurants . "Use Cases: Restaurants"
/use-cases/cafeterias .. "Use Cases: Cafeterias"
/use-cases/food-courts . "Use Cases: Food Courts"
/resources ............. "Resources"
/resources/any-slug .... "Article: any-slug"
/contact ............... "Contact"
/book-demo ............. "Book a Demo"
/nonexistent-route ..... "Page Not Found" (from not-found.tsx)
AC-1.3 — Navigation link verification
□ All 5 header nav links present and clickable
□ All footer links present and clickable
□ No broken links (every href resolves to a known route or 404)
□ Logo link goes to /
AC-1.4 — TypeScript verification
□ npx tsc --noEmit returns 0 errors
□ No 'any' types exist in any file
□ All component props are typed
AC-1.5 — No Phase 2+ content exists
□ No color tokens or custom color classes
□ No UI component files beyond Header, Footer, NavLink
□ No form elements in any file
□ No useState or useEffect in any file
□ No 'use client' directives
□ No generateMetadata exports
□ No analytics scripts or imports
