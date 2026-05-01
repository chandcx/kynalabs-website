PHASE 4 — FORMS AND APIs
Phase Objective
Add interactivity to all forms. Implement API routes. Wire form validation using React Hook Form and Zod. Handle loading states, success states, and error states. No analytics yet.

Original SDD Sections Covered in Phase 4
SectionWhat is implementedSection 6.8 — Contact pageForm submission, validation, success/error statesSection 6.9 — Book Demo pageForm submission, validation, success/error statesSection 6.5 — Future product waitlistWaitlist form on coming-soon pageSection 16.5 — Form API routes/api/contact, /api/book-demo, /api/waitlistSection 10.2 — Button loading stateAdd loading prop to Button componentSection 10.1 — Form components with validationConnect React Hook Form to Input, Select, TextareaSection 13 — Analytics events (form events only)demo_form_start, demo_form_submit, demo_form_error, contact_form_submit, waitlist_signup
Original SDD Sections Deferred from Phase 4
SectionDeferred ToSection 12 — SEO metadataPhase 5Section 13 — Non-form analytics events (page_view, cta_click, nav_click, etc.)Phase 5Section 15 — Full accessibility auditPhase 5Section 16.6 — Article markdown rendering (mdx-remote)Optional Phase 5 enhancement

Phase 4 — Explicit Exclusions
DO NOT BUILD IN PHASE 4:

❌ generateMetadata on any page
❌ Non-form analytics events (page views, CTA clicks, nav clicks)
❌ Structured data / JSON-LD
❌ Sitemap or robots.txt
❌ Performance optimisation
❌ Any new pages or page sections not already built in Phase 3
❌ Changes to Phase 3 page content

Phase 4 — Build Step 1: Install Required Packages
bashnpm install react-hook-form @hookform/resolvers zod
npm install resend    # or: keep as optional, use console.log in dev

Phase 4 — Build Step 2: Validation Schemas
typescript// lib/validations.ts
import { z } from 'zod';

export const ContactSchema = z.object({
  name:    z.string().min(2, 'Name must be at least 2 characters'),
  email:   z.string().email('Please enter a valid email address'),
  company: z.string().optional(),
  subject: z.enum([
    'general',
    'partnership',
    'press',
    'product-feedback',
    'waitlist',
  ], { required_error: 'Please select a subject' }),
  message: z.string().min(20, 'Message must be at least 20 characters'),
});

export const DemoSchema = z.object({
  name:          z.string().min(2, 'Full name required'),
  email:         z.string().email('Valid email required'),
  phone:         z.string()
                   .min(10, 'Enter a valid Indian mobile number')
                   .max(13),
  businessName:  z.string().min(2, 'Business name required'),
  businessType:  z.enum([
    'restaurant', 'cafeteria', 'food-court', 'hotel', 'other'
  ], { required_error: 'Select your business type' }),
  locations:     z.enum(['1', '2-5', '6+'], {
                   required_error: 'Select number of locations'
                 }),
  hearAboutUs:   z.string().optional(),
  preferredTime: z.string().optional(),
});

export const WaitlistSchema = z.object({
  email: z.string().email('Valid email required'),
});

export type ContactInput  = z.infer<typeof ContactSchema>;
export type DemoInput     = z.infer<typeof DemoSchema>;
export type WaitlistInput = z.infer<typeof WaitlistSchema>;

Phase 4 — Build Step 3: API Routes
typescript// app/api/contact/route.ts
import { NextRequest, NextResponse } from 'next/server';
import { ContactSchema } from '@/lib/validations';

export async function POST(req: NextRequest) {
  try {
    const body = await req.json();
    const result = ContactSchema.safeParse(body);

    if (!result.success) {
      return NextResponse.json(
        { error: 'Invalid form data', issues: result.error.issues },
        { status: 400 }
      );
    }

    // Development: log to console
    if (process.env.NODE_ENV === 'development') {
      console.log('[Contact form]', result.data);
    }

    // Production: send via Resend if API key present
    if (process.env.RESEND_API_KEY) {
      // Resend integration here
      // const resend = new Resend(process.env.RESEND_API_KEY);
      // await resend.emails.send({ ... });
    }

    return NextResponse.json({ success: true });
  } catch {
    return NextResponse.json(
      { error: 'Something went wrong. Please try again.', code: 'SERVER_ERROR' },
      { status: 500 }
    );
  }
}
typescript// app/api/book-demo/route.ts
// Same pattern as contact — DemoSchema validation
// Log in dev, send via Resend in prod if key present
typescript// app/api/waitlist/route.ts
// Same pattern — WaitlistSchema validation

Phase 4 — Build Step 4: Form Components with Validation
Convert components/forms/ContactForm.tsx and components/forms/DemoBookingForm.tsx to client components with full React Hook Form integration.
typescript// components/forms/DemoBookingForm.tsx
'use client';

import { useForm } from 'react-hook-form';
import { zodResolver } from '@hookform/resolvers/zod';
import { useState } from 'react';
import { DemoSchema, type DemoInput } from '@/lib/validations';
import { Button }    from '@/components/ui/Button';
import { FormField } from '@/components/forms/FormField';
import { Input }     from '@/components/ui/Input';
import { Select }    from '@/components/ui/Select';

export function DemoBookingForm() {
  const [status, setStatus] = useState<'idle' | 'loading' | 'success' | 'error'>('idle');

  const {
    register,
    handleSubmit,
    formState: { errors },
  } = useForm<DemoInput>({ resolver: zodResolver(DemoSchema) });

  const onSubmit = async (data: DemoInput) => {
    setStatus('loading');
    try {
      const res = await fetch('/api/book-demo', {
        method:  'POST',
        headers: { 'Content-Type': 'application/json' },
        body:    JSON.stringify(data),
      });
      if (!res.ok) throw new Error('Submission failed');
      setStatus('success');
    } catch {
      setStatus('error');
    }
  };

  if (status === 'success') {
    return (
      <div role="alert" aria-live="polite">
        <h2>Request received!</h2>
        <p>We've received your request. Expect a WhatsApp or email
           from us within 4 business hours.</p>
      </div>
    );
  }

  return (
    <form onSubmit={handleSubmit(onSubmit)} noValidate>
      <FormField label="Full name" htmlFor="name" required>
        <Input id="name" {...register('name')} />
        {errors.name && (
          <p role="alert" className="text-semantic-error text-small">
            {errors.name.message}
          </p>
        )}
      </FormField>

      {/* All remaining fields per SDD Section 6.9 */}

      <Button
        type="submit"
        variant="primary"
        size="lg"
        disabled={status === 'loading'}
      >
        {status === 'loading' ? 'Sending...' : 'Request Demo'}
      </Button>

      {status === 'error' && (
        <p role="alert" className="text-semantic-error text-small mt-2">
          Something went wrong. Please try again.
        </p>
      )}
    </form>
  );
}

Phase 4 — Build Step 5: FormField Error Message Slot
Update FormField.tsx to accept and render an error prop:
typescript// Update components/forms/FormField.tsx
type FormFieldProps = {
  label:     string;
  htmlFor:   string;
  required?: boolean;
  error?:    string;           // wired in Phase 4
  children:  React.ReactNode;
  className?: string;
};

// Render error if present:
{error && (
  <p id={`${htmlFor}-error`} role="alert"
     className="text-semantic-error text-small mt-1">
    {error}
  </p>
)}

Phase 4 — Build Step 6: Button Loading State
Update Button.tsx to handle loading prop:
typescript// Add to ButtonProps:
loading?: boolean;

// In render:
const isDisabled = disabled || loading;
// In children render:
{loading ? (
  <>
    <svg className="animate-spin h-4 w-4 mr-2" .../>
    Loading...
  </>
) : children}

Phase 4 — Build Step 7: Form Analytics Events (Form Events Only)
Add analytics calls inside form components. Use the trackEvent helper from lib/analytics.ts — create it now even though the full analytics setup is Phase 5.
typescript// lib/analytics.ts — Phase 4 stub
// Full gtag wiring added in Phase 5.
// This file exists now so form components can import it safely.

export function trackEvent(
  eventName: string,
  params?: Record<string, string | number>
) {
  if (typeof window === 'undefined') return;
  // Phase 5 will add: if (!window.gtag) return; window.gtag('event', ...);
  if (process.env.NODE_ENV === 'development') {
    console.log('[Analytics event]', eventName, params);
  }
}
Wire these events in form components per SDD Section 13.2:

demo_form_start — on first interaction with demo form
demo_form_submit — on successful demo form submission
demo_form_error — on demo form error
contact_form_submit — on successful contact form submission
waitlist_signup — on waitlist form submission


Phase 4 — Acceptance Criteria
AC-4.1 — Form validation
□ Contact form: submit with empty fields → inline errors per field
□ Contact form: invalid email format → "Please enter a valid email address"
□ Contact form: message < 20 chars → error shown
□ Demo form: all required fields validated on submit
□ Demo form: Indian phone number validated (10-13 digits)
□ Waitlist form: invalid email → error shown
□ No page reload on any form submit
AC-4.2 — Form submission
□ Demo form: submits to /api/book-demo, receives 200
□ Contact form: submits to /api/contact, receives 200
□ Waitlist form: submits to /api/waitlist, receives 200
□ All API routes return 400 for invalid data with error details
□ All API routes return 500 for server errors with generic message
AC-4.3 — State management
□ Demo form: success state replaces form (not added above it)
□ Contact form: success state replaces form
□ Submit button disabled while loading
□ Submit button re-enabled on error (allows retry)
□ Error state shows without page reload
AC-4.4 — Accessibility (forms)
□ All form inputs have associated <label> elements
□ Error messages have role="alert"
□ Error messages linked to inputs via aria-describedby
□ Required fields have aria-required="true"
□ Form keyboard-navigable (Tab through all fields, Enter to submit)
AC-4.5 — Analytics (development mode)
□ demo_form_start logs to console on first field interaction
□ demo_form_submit logs to console on success
□ demo_form_error logs to console on error
□ contact_form_submit logs to console on success
AC-4.6 — Build verification
bashnpx tsc --noEmit   # 0 errors
npm run build      # succeeds
