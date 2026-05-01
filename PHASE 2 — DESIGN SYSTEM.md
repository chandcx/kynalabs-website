PHASE 2 — DESIGN SYSTEM
Phase Objective
Implement the complete Kyna Labs design system from SDD Section 9 and Section 10. All UI components built and individually verifiable. No page content yet. Typography, color tokens, spacing, and all reusable components must be production-ready before Phase 3 uses them.

Original SDD Sections Covered in Phase 2
SectionWhat is implementedSection 4.2 — Visual identity (colors, fonts)Color tokens, Tailwind config, font loadingSection 9.1 — Color tokensAll brand and semantic colors in Tailwind configSection 9.2 — Typography scaleFont loading, Tailwind typography configSection 9.3 — Spacing scaleVerified Tailwind defaults, documented in configSection 9.4 — BreakpointsTailwind breakpoint config documentedSection 10.1 — Component file structureAll component files createdSection 10.2 — Button component specFull Button component, all variantsSection 10.3 — ProductCard component specProductCard component, all propsSection 11 — Responsive behavior (rules only)Rules applied to all componentsSection 16.4 — Content data patterncontent/products.ts, content/use-cases.ts, content/team.ts
Original SDD Sections Deferred from Phase 2
SectionDeferred ToSection 6.1–6.9 — All page section contentPhase 3Section 7.3 — Footer with column layout and iconsPhase 3Section 7.1–7.2 — Header with dropdowns and mobile menuPhase 3Section 12 — SEO metadataPhase 5Section 13 — Analytics event wiring to componentsPhase 5Section 15 — Full accessibility auditPhase 5Section 17 — Forms and API routesPhase 4Section 4.3 — Photography direction (actual images)Phase 3

Phase 2 — Explicit Exclusions
DO NOT BUILD IN PHASE 2:

❌ Any page content or section copy
❌ Complete header dropdown menus (links only — no interaction)
❌ Mobile hamburger menu logic (layout only)
❌ Any form elements (Input, Select, Textarea exist as components but
   contain no validation logic, no state, no submit handling)
❌ API routes
❌ Analytics event calls inside components
❌ generateMetadata on any page
❌ Actual images (use placeholder divs with background colors)
❌ JSON-LD structured data
❌ Sitemap or robots.txt
❌ The interactive TapEat demo placeholder div (Phase 3)
❌ Any useState or useEffect inside components
❌ All 'use client' directives (components are pure render, no state)

Phase 2 — Build Step 1: Tailwind Config and Tokens
Update tailwind.config.ts with all design tokens from SDD Section 9:
typescript// tailwind.config.ts
import type { Config } from 'tailwindcss';

const config: Config = {
  content: [
    './app/**/*.{ts,tsx}',
    './components/**/*.{ts,tsx}',
    './content/**/*.{ts,tsx}',
  ],
  theme: {
    extend: {
      colors: {
        brand: {
          purple:       '#3B0764',
          'purple-mid': '#6D28D9',
          'purple-light':'#EDE9FE',
          amber:        '#F59E0B',
          'amber-light':'#FEF3C7',
        },
        neutral: {
          slate:      '#1E293B',
          'slate-light': '#334155',
          gray:       '#64748B',
          'gray-light':'#94A3B8',
          border:     '#E2E8F0',
          bg:         '#FAFAF9',
          'bg-dark':  '#0F0F0F',
        },
        semantic: {
          success: '#16A34A',
          error:   '#DC2626',
          warning: '#F59E0B',
          info:    '#1D4ED8',
        },
      },
      fontFamily: {
        sans:    ['var(--font-inter)', 'system-ui', 'sans-serif'],
        heading: ['var(--font-sora)', 'system-ui', 'sans-serif'],
        mono:    ['var(--font-jetbrains)', 'monospace'],
      },
      fontSize: {
        'display': ['56px', { lineHeight: '1.1', fontWeight: '800' }],
        'h1':      ['40px', { lineHeight: '1.2', fontWeight: '700' }],
        'h2':      ['30px', { lineHeight: '1.3', fontWeight: '700' }],
        'h3':      ['22px', { lineHeight: '1.4', fontWeight: '600' }],
        'h4':      ['18px', { lineHeight: '1.4', fontWeight: '600' }],
        'body-lg': ['18px', { lineHeight: '1.6', fontWeight: '400' }],
        'body':    ['16px', { lineHeight: '1.6', fontWeight: '400' }],
        'small':   ['14px', { lineHeight: '1.5', fontWeight: '400' }],
        'caption': ['12px', { lineHeight: '1.4', fontWeight: '400' }],
        'label':   ['13px', { lineHeight: '1.4', fontWeight: '500',
                              letterSpacing: '0.05em' }],
      },
      borderRadius: {
        DEFAULT: '12px',
        card:    '20px',
        pill:    '999px',
      },
      boxShadow: {
        card: '0 2px 12px rgba(0,0,0,0.06)',
        lg:   '0 8px 32px rgba(0,0,0,0.10)',
      },
      maxWidth: {
        container: '1200px',
      },
    },
  },
  plugins: [],
};

export default config;

Phase 2 — Build Step 2: Font Loading
Update app/layout.tsx to load fonts. This is the ONLY change to layout.tsx in Phase 2:
typescript// app/layout.tsx — Phase 2 update (font loading only)
import { Sora, Inter } from 'next/font/google';
import { Header } from '@/components/layout/Header';
import { Footer } from '@/components/layout/Footer';
import './globals.css';

const sora = Sora({
  subsets: ['latin'],
  variable: '--font-sora',
  display: 'swap',
});

const inter = Inter({
  subsets: ['latin'],
  variable: '--font-inter',
  display: 'swap',
});

export default function RootLayout({
  children,
}: {
  children: React.ReactNode;
}) {
  return (
    <html lang="en" className={`${sora.variable} ${inter.variable}`}>
      <body className="font-sans bg-neutral-bg text-neutral-slate antialiased">
        <Header />
        <main>{children}</main>
        <Footer />
      </body>
    </html>
  );
}

Phase 2 — Build Step 3: Content Data Files
Create data files. These are static TypeScript objects. No API calls.
typescript// content/products.ts
export type ProductStatus = 'live' | 'coming-soon' | 'beta';

export type Product = {
  slug:        string;
  name:        string;
  tagline:     string;
  description: string;
  status:      ProductStatus;
  features:    string[];
  href:        string;
  category:    string;
};

export const products: Product[] = [
  {
    slug:        'tapeat',
    name:        'TapEat',
    tagline:     'QR-based browser ordering for restaurants and cafeterias',
    description: 'Customers scan, order, and pay in under 60 seconds. No app. No login. Works on any mobile browser.',
    status:      'live',
    category:    'Food Ordering',
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
    description: "We're working on our next product for the food and hospitality sector. Join the waitlist to be notified first.",
    status:      'coming-soon',
    category:    'TBD',
    features:    [],
    href:        '/contact',
  },
];
typescript// content/use-cases.ts
export type UseCase = {
  slug:        string;
  label:       string;
  headline:    string;
  description: string;
  href:        string;
};

export const useCases: UseCase[] = [
  {
    slug:        'restaurants',
    label:       'Restaurants & Cafés',
    headline:    'Turn every table into an ordering point',
    description: 'Reduce wait times, increase table turns, and accept UPI payments without a dedicated app.',
    href:        '/use-cases/restaurants',
  },
  {
    slug:        'cafeterias',
    label:       'Corporate Cafeterias',
    headline:    'Digitise your campus cafeteria in days',
    description: 'Counter pickup with token display. Works on any Android tablet. No infrastructure changes needed.',
    href:        '/use-cases/cafeterias',
  },
  {
    slug:        'food-courts',
    label:       'Food Courts & Malls',
    headline:    'One QR per stall. One dashboard per operator.',
    description: 'Each vendor manages their own menu and orders. Customers order from any stall without queuing.',
    href:        '/use-cases/food-courts',
  },
];
typescript// content/team.ts
export type TeamMember = {
  name:       string;
  title:      string;
  bio:        string;
  photoUrl:   string;
  linkedinUrl?: string;
};

export const team: TeamMember[] = [
  {
    name:       'Founder Name',
    title:      'Co-founder & CEO',
    bio:        'Previously built software for F&B operators across South India.',
    photoUrl:   '/images/team/placeholder.jpg',
    linkedinUrl:'https://linkedin.com',
  },
  // Add more team members here
];
typescript// content/articles/index.ts
export type Article = {
  slug:       string;
  title:      string;
  excerpt:    string;
  category:   'Industry' | 'Product' | 'How-To';
  author:     string;
  authorTitle:string;
  date:       string;
  readTime:   string;
  coverImage: string;
};

export const articles: Article[] = [
  {
    slug:        'qr-ordering-india',
    title:       'Why QR-based ordering is the right model for India',
    excerpt:     'Browser-native ordering removes the biggest conversion barrier in Indian restaurants: the app download.',
    category:    'Industry',
    author:      'Kyna Labs Team',
    authorTitle: 'Kyna Labs',
    date:        '2025-04-01',
    readTime:    '5 min read',
    coverImage:  '/images/articles/qr-ordering-india.jpg',
  },
  {
    slug:        'reduce-wait-times-restaurant',
    title:       '5 ways to reduce wait times in your restaurant without hiring more staff',
    excerpt:     'Practical changes you can make this week to serve more customers without adding headcount.',
    category:    'How-To',
    author:      'Kyna Labs Team',
    authorTitle: 'Kyna Labs',
    date:        '2025-04-15',
    readTime:    '7 min read',
    coverImage:  '/images/articles/reduce-wait-times.jpg',
  },
];

Phase 2 — Build Step 4: All UI Components
Create every component file from SDD Section 10.1. Each must be a pure render component — no state, no effects, no client-side logic.
components/ui/Button.tsx
typescript// components/ui/Button.tsx
// SDD Section 10.2 — full implementation
// All variants: primary, secondary, ghost, text
// All sizes: sm, md, lg
// Renders as <a> when href provided, <button> otherwise

import Link from 'next/link';

type ButtonVariant = 'primary' | 'secondary' | 'ghost' | 'text';
type ButtonSize    = 'sm' | 'md' | 'lg';

type ButtonProps = {
  variant?:  ButtonVariant;
  size?:     ButtonSize;
  href?:     string;
  disabled?: boolean;
  type?:     'button' | 'submit' | 'reset';
  children:  React.ReactNode;
  className?: string;
  // Note: onClick and loading added in Phase 4 when interactivity is needed
};

const variantClasses: Record<ButtonVariant, string> = {
  primary:   'bg-brand-purple text-white hover:bg-brand-purple-mid',
  secondary: 'border-2 border-brand-purple text-brand-purple hover:bg-brand-purple-light',
  ghost:     'bg-transparent text-brand-purple hover:underline underline-offset-4',
  text:      'text-brand-purple hover:underline underline-offset-4 p-0',
};

const sizeClasses: Record<ButtonSize, string> = {
  sm: 'px-4 py-2 text-sm',
  md: 'px-6 py-3 text-base',
  lg: 'px-8 py-4 text-lg',
};

export function Button({
  variant  = 'primary',
  size     = 'md',
  href,
  disabled = false,
  type     = 'button',
  children,
  className = '',
}: ButtonProps) {
  const base = 'inline-flex items-center justify-center font-semibold rounded-pill transition-colors duration-150 focus-visible:outline-none focus-visible:ring-2 focus-visible:ring-brand-purple focus-visible:ring-offset-2';
  const classes = [
    base,
    variant !== 'text' ? sizeClasses[size] : '',
    variantClasses[variant],
    disabled ? 'opacity-50 cursor-not-allowed pointer-events-none' : '',
    className,
  ].filter(Boolean).join(' ');

  if (href) {
    return <Link href={href} className={classes}>{children}</Link>;
  }

  return (
    <button type={type} disabled={disabled} className={classes}>
      {children}
    </button>
  );
}
components/ui/Badge.tsx
typescript// components/ui/Badge.tsx
// SDD Section 10.3 — status badge for product cards
// Variants match ProductStatus type from content/products.ts

type BadgeVariant = 'live' | 'coming-soon' | 'beta' | 'default';

type BadgeProps = {
  variant?:  BadgeVariant;
  children:  React.ReactNode;
  className?: string;
};

const variantClasses: Record<BadgeVariant, string> = {
  live:         'bg-semantic-success/10 text-semantic-success',
  'coming-soon':'bg-brand-amber-light text-brand-amber',
  beta:         'bg-semantic-info/10 text-semantic-info',
  default:      'bg-neutral-border text-neutral-gray',
};

export function Badge({ variant = 'default', children, className = '' }: BadgeProps) {
  return (
    <span className={`inline-flex items-center px-3 py-1 rounded-pill text-label font-semibold ${variantClasses[variant]} ${className}`}>
      {children}
    </span>
  );
}
components/ui/Card.tsx
typescript// components/ui/Card.tsx
// Generic card wrapper. Content provided via children.
// Used by ProductCard, ArticleCard, TeamCard, etc.

type CardProps = {
  children:  React.ReactNode;
  className?: string;
  as?:       'div' | 'article' | 'section';
};

export function Card({ children, className = '', as: Tag = 'div' }: CardProps) {
  return (
    <Tag className={`bg-white rounded-card shadow-card p-6 ${className}`}>
      {children}
    </Tag>
  );
}
components/ui/Icon.tsx
typescript// components/ui/Icon.tsx
// Lucide icon wrapper with size and color props
// All icons come from lucide-react only

import type { LucideIcon } from 'lucide-react';

type IconProps = {
  icon:      LucideIcon;
  size?:     number;
  color?:    string;
  className?: string;
  ariaLabel?: string;
};

export function Icon({
  icon:  IconComponent,
  size  = 24,
  color = 'currentColor',
  className = '',
  ariaLabel,
}: IconProps) {
  return (
    <IconComponent
      size={size}
      color={color}
      className={className}
      aria-label={ariaLabel}
      aria-hidden={!ariaLabel}
    />
  );
}
components/ui/Input.tsx, components/ui/Select.tsx, components/ui/Textarea.tsx, components/forms/FormField.tsx
typescript// components/ui/Input.tsx
// Phase 2: Static render only. No onChange, no validation.
// Interaction and validation wired in Phase 4.

type InputProps = {
  id:          string;
  name:        string;
  type?:       string;
  placeholder?: string;
  required?:   boolean;
  disabled?:   boolean;
  className?:  string;
};

export function Input({
  id, name, type = 'text', placeholder, required, disabled, className = ''
}: InputProps) {
  return (
    <input
      id={id}
      name={name}
      type={type}
      placeholder={placeholder}
      required={required}
      disabled={disabled}
      className={`w-full border border-neutral-border rounded-DEFAULT px-4 py-3 text-body text-neutral-slate placeholder:text-neutral-gray focus:outline-none focus:ring-2 focus:ring-brand-purple focus:border-transparent disabled:opacity-50 ${className}`}
    />
  );
}
typescript// components/ui/Select.tsx
type SelectOption = { value: string; label: string };

type SelectProps = {
  id:       string;
  name:     string;
  options:  SelectOption[];
  placeholder?: string;
  required?: boolean;
  className?: string;
};

export function Select({ id, name, options, placeholder, required, className = '' }: SelectProps) {
  return (
    <select
      id={id}
      name={name}
      required={required}
      defaultValue=""
      className={`w-full border border-neutral-border rounded-DEFAULT px-4 py-3 text-body text-neutral-slate focus:outline-none focus:ring-2 focus:ring-brand-purple focus:border-transparent ${className}`}
    >
      {placeholder && <option value="" disabled>{placeholder}</option>}
      {options.map(opt => (
        <option key={opt.value} value={opt.value}>{opt.label}</option>
      ))}
    </select>
  );
}
typescript// components/ui/Textarea.tsx
type TextareaProps = {
  id:          string;
  name:        string;
  placeholder?: string;
  rows?:        number;
  required?:    boolean;
  className?:   string;
};

export function Textarea({ id, name, placeholder, rows = 4, required, className = '' }: TextareaProps) {
  return (
    <textarea
      id={id}
      name={name}
      placeholder={placeholder}
      rows={rows}
      required={required}
      className={`w-full border border-neutral-border rounded-DEFAULT px-4 py-3 text-body text-neutral-slate placeholder:text-neutral-gray focus:outline-none focus:ring-2 focus:ring-brand-purple focus:border-transparent resize-vertical ${className}`}
    />
  );
}
typescript// components/forms/FormField.tsx
// Label + input + error message wrapper.
// Error message rendering wired in Phase 4.

type FormFieldProps = {
  label:    string;
  htmlFor:  string;
  required?: boolean;
  children: React.ReactNode;
  className?: string;
};

export function FormField({ label, htmlFor, required, children, className = '' }: FormFieldProps) {
  return (
    <div className={`flex flex-col gap-1.5 ${className}`}>
      <label
        htmlFor={htmlFor}
        className="text-label text-neutral-slate font-medium"
      >
        {label}
        {required && <span className="text-semantic-error ml-1" aria-hidden="true">*</span>}
      </label>
      {children}
      {/* Error message slot — wired in Phase 4 */}
    </div>
  );
}
components/layout/Container.tsx and components/layout/Section.tsx
typescript// components/layout/Container.tsx
type ContainerProps = {
  children:  React.ReactNode;
  className?: string;
};

export function Container({ children, className = '' }: ContainerProps) {
  return (
    <div className={`mx-auto max-w-container px-6 ${className}`}>
      {children}
    </div>
  );
}
typescript// components/layout/Section.tsx
type SectionProps = {
  children:    React.ReactNode;
  className?:  string;
  background?: 'white' | 'light' | 'dark' | 'purple';
  id?:         string;
};

const bgClasses = {
  white:  'bg-white',
  light:  'bg-neutral-bg',
  dark:   'bg-neutral-slate text-white',
  purple: 'bg-brand-purple text-white',
};

export function Section({ children, className = '', background = 'white', id }: SectionProps) {
  return (
    <section
      id={id}
      className={`py-12 md:py-16 lg:py-20 ${bgClasses[background]} ${className}`}
    >
      {children}
    </section>
  );
}
All Section Components (structure only — no content)
typescript// components/sections/HeroSection.tsx
// SDD Section 10.1 — accepts props, renders layout structure
// Content filled in Phase 3

type HeroSectionProps = {
  eyebrow?:        string;
  headline:        string;
  subheadline:     string;
  primaryCta:      { label: string; href: string };
  secondaryCta?:   { label: string; href: string };
  badges?:         string[];
  visual?:         React.ReactNode;
};

import { Button }    from '@/components/ui/Button';
import { Container } from '@/components/layout/Container';
import { Section }   from '@/components/layout/Section';

export function HeroSection({
  eyebrow, headline, subheadline,
  primaryCta, secondaryCta, badges, visual
}: HeroSectionProps) {
  return (
    <Section background="light">
      <Container>
        <div className="flex flex-col lg:flex-row gap-8 lg:gap-16 items-center">
          <div className="flex-1">
            {eyebrow && (
              <p className="text-label text-brand-purple uppercase mb-3">{eyebrow}</p>
            )}
            <h1 className="text-display font-heading text-neutral-slate mb-4">
              {headline}
            </h1>
            <p className="text-body-lg text-neutral-gray mb-8">{subheadline}</p>
            <div className="flex flex-wrap gap-4">
              <Button href={primaryCta.href} variant="primary" size="lg">
                {primaryCta.label}
              </Button>
              {secondaryCta && (
                <Button href={secondaryCta.href} variant="secondary" size="lg">
                  {secondaryCta.label}
                </Button>
              )}
            </div>
            {badges && badges.length > 0 && (
              <div className="flex flex-wrap gap-2 mt-6">
                {badges.map(b => (
                  <Badge key={b} variant="default">{b}</Badge>
                ))}
              </div>
            )}
          </div>
          {visual && (
            <div className="flex-1 w-full">{visual}</div>
          )}
        </div>
      </Container>
    </Section>
  );
}
Create the following remaining section components as structural shells — correct props interface, correct layout structure, but content populated in Phase 3:
components/sections/
├── FeatureGrid.tsx        Props: headline, subheadline, features[]
├── StepProcess.tsx        Props: headline, steps[]
├── CTABanner.tsx          Props: headline, subheadline, cta
├── StatsRow.tsx           Props: stats[]
├── ProductCard.tsx        Props: per SDD Section 10.3
├── UseCaseTile.tsx        Props: useCase (UseCase type)
└── TestimonialCard.tsx    Props: quote, author, company

components/blog/
├── ArticleCard.tsx        Props: article (Article type)
└── ArticleLayout.tsx      Props: article, children (content)

components/navigation/
├── Dropdown.tsx           Props: label, items[] — structure only, no interaction
└── MobileMenu.tsx         Props: isOpen, links[] — structure only

Phase 2 — Build Step 5: Updated Header and Footer with Styling
Update Header.tsx and Footer.tsx with full styling per SDD Sections 7.1 and 7.3. Navigation interaction (dropdowns, hamburger) is NOT yet wired — links only.

Phase 2 — Acceptance Criteria
AC-2.1 — Compile and type check
bashnpx tsc --noEmit   # 0 errors
npm run build      # succeeds
AC-2.2 — Design token verification
□ Deep purple #3B0764 visible as a background or text color on at least one element
□ Amber #F59E0B visible as a background or accent on at least one element
□ Sora font loads and applies to heading elements
□ Inter font loads and applies to body text
□ No residual default Next.js styling (remove globals.css defaults)
AC-2.3 — Component rendering
Each component must render without errors in isolation:
□ Button — all 4 variants render (primary, secondary, ghost, text)
□ Button — all 3 sizes render (sm, md, lg)
□ Button — renders as <a> when href provided
□ Badge — all 4 variants render (live, coming-soon, beta, default)
□ Card — renders children correctly
□ Icon — renders a Lucide icon
□ Input — renders with label via FormField
□ Select — renders with options
□ Textarea — renders with placeholder
□ Container — constrains width to max-w-container
□ Section — renders each background variant
□ HeroSection — renders with required props
AC-2.4 — No Phase 3+ content
□ No page sections have real copy (only prop-driven content)
□ No onClick handlers on any component
□ No useState in any component file
□ No form submission logic
□ No analytics calls
AC-2.5 — Responsive
□ All components tested at 375px — no horizontal scroll
□ Button wraps correctly on small screens
□ Container respects 24px horizontal padding on mobile
