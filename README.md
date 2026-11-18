# 🌸 Aiza Consulting Services — Website

A single-page, static website for **Aiza Consulting Services** — real estate,
residential mortgages, income tax filing, immigration forms, Indian passport
surrender, OCI & visa applications, and Pakistani passport renewal
(Machine-Readable Passports).

No build step. One self-contained file: `public/index.html` (inline CSS + JS,
Google Fonts only). Deploy as a Cloudflare Pages site with `wrangler.toml`
(`pages_build_output_dir = "public"`), or serve `public/` from any static host.

## What is on the site

- **Sticky header** with navigation + Book button; hero with a free
  30-minute consultation offer; "How it works" in 3 steps.
- **All 7 services** as cards, each with a Details view (steps, document
  list, and the note "timelines are set by the authorities").
- **Free tools:** Document Checklist Builder (service + situation, tickable
  with progress bar + print), OCI Eligibility Quiz (4 questions, with the
  disclaimer that only the Government of India decides), Mortgage Calculator
  (principal + interest, formula shown), and a Tax Season Checklist
  (personal vs business).
- **Appointment booking (client-side):** service dropdown (pre-filled from
  any service card's "Book" button), Physical / Virtual mode, date picker
  limited to the next 30 days with Sundays closed, and **different time
  slots on each date** — 30-minute slots from 9:00 AM to 4:30 PM generated
  deterministically from the date (seeded hash), with some shown as already
  booked and at least 6 bookable slots per open day.
- **On confirm:** booking reference like `AZA-2026-XXXX`, a full summary,
  Download calendar file (`.ics` generated in JS), Send via WhatsApp
  (`wa.me/?text=…` — no number is hardcoded, the user picks the contact),
  and Copy booking details.
- **My bookings:** saved in `localStorage` on the visitor's device, with a
  Cancel option. The page states bookings are saved on this device for this
  demo/temporary site and that Aiza will confirm by phone/WhatsApp.
- **FAQ accordion** (10 Q&As, including "Are you a government office / law
  firm?"), Why Choose Us values, official-links section
  (ociservices.gov.in, VFS Global, IRS, Canada Revenue Agency, Pakistan
  passport directorate), contact section, and footer disclaimer:
  *"Aiza Consulting Services is an independent private service. It is not a
  government agency, consulate, law firm, or authorized immigration
  representative."*

## Placeholders — Aiza to fill in before going live

No prices, testimonials, phone number, email or address were invented.
The contact section shows clearly editable placeholders:

- Phone: **"Add phone number"**
- Email: **"Add email address"**
- Office: **"Add office address"**

Search `public/index.html` for `Add phone number`, `Add email address`,
and `Add office address` to replace them. Service prices are intentionally
not listed — the site says prices are quoted after a free consultation.

To connect bookings to a real backend later, replace the `localStorage`
save in the booking submit handler (search for `aizaBookings`) with a
`fetch()` to Aiza's booking endpoint / form service, and add her WhatsApp
number to the `wa.me/` link in `sendWhatsApp()`.

## Deploy (Cloudflare Pages)

```bash
cd aiza-consulting
npx wrangler pages deploy public --project-name aiza-consulting
```

Or connect the GitHub repo to Cloudflare Pages with build output
directory `public` and no build command.
