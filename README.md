# Agency Portfolio with Custom CMS

A full-featured portfolio and CMS starter built with Next.js, Sanity, and MongoDB. Designed as a customizable agency or freelancer portfolio with an integrated admin area, blog, services, portfolio items, and contact workflows.

## Key Features
- Next.js (App Router, server actions enabled)
- Sanity CMS integration for content (studio + front-end read/write via API)
- MongoDB for application data (auth, forms, admin seeding)
- Authentication utilities (Better Auth + custom helpers)
- Email sending via `nodemailer` for contact forms
- UI primitives from Radix, TailwindCSS utilities and Styled Components
- React Query for client data fetching and caching
- Rich text editing / Portable Text support

## Tech Stack
- Framework: Next.js 16 (App Router)
- Language: TypeScript
- CMS: Sanity
- Database: MongoDB
- Styling: TailwindCSS, Styled Components
- UI: Radix UI, Lucide icons
- Forms: react-hook-form, zod (validation)
- State & Data: @tanstack/react-query

## Quick Start
1. Install dependencies

```bash
npm install
# or
pnpm install
```

2. Copy environment variables

```bash
cp env-sample .env
# fill the values in .env
```

Required env vars (see `env-sample`):
- `BETTER_AUTH_SECRET`, `BETTER_AUTH_URL`
- `MONGODB_URI`
- `SMTP_USER`, `SMTP_PASS`
- `ADMIN_SEEDER_SECRET`
- `NODE_ENV`
- `NEXT_PUBLIC_BASE_URL`
- `NEXT_PUBLIC_SANITY_PROJECT_ID`, `NEXT_PUBLIC_SANITY_DATASET`, `NEXT_PUBLIC_SANITY_API_VERSION`, `NEXT_SANITY_API_TOKEN`

3. Run locally

```bash
npm run dev
```

Open http://localhost:3000

4. Build for production

```bash
npm run build
npm start
```

## Project Structure (high level)
- `app/` — Next.js app entry (layouts, pages, routing)
- `components/` — UI components and admin-specific components
- `sanity/` — Sanity studio / config and schemas
- `lib/` — helpers, clients (Sanity, MongoDB, auth, mail)
- `api/` — API routes (auth, forms, admin actions)
- `actions/` — server actions used by the app
- `types/` — TypeScript type definitions
- `helpers/` — business logic and content helpers
- `provider/` — global providers and CSS

## Sanity
This project uses Sanity as the headless CMS. Configure Sanity credentials in your `.env` using the `NEXT_PUBLIC_SANITY_*` and `NEXT_SANITY_API_TOKEN` variables. The frontend uses `@sanity/client` and `next-sanity` to fetch content.

If you need to run the Sanity studio (if present), consult the `sanity/` folder for studio commands — the exact command may depend on your local setup.

## Database & Auth
- MongoDB connection string goes to `MONGODB_URI`.
- The app contains helpers for admin seeding and session management. Protect the `ADMIN_SEEDER_SECRET` and auth secrets.

## Scripts
- `npm run dev` — runs Next.js in development
- `npm run build` — build for production
- `npm start` — start the production server
- `npm run lint` — run ESLint

## Environment & Deployment
- Recommended deployment: Vercel (Next.js-ready). Set all `.env` variables in your deployment platform.
- Ensure `NEXT_PUBLIC_BASE_URL` is set to your deployed site URL.

## Contributing
- Create feature branches and open PRs.
- Follow existing code style (TypeScript, Tailwind + styled-components patterns).
- Run `npm run lint` before submitting PRs.

## Troubleshooting & Notes
- If images are served from Sanity or external providers, Next.js `remotePatterns` is preconfigured for `cdn.sanity.io` and `images.unsplash.com` in `next.config.ts`.
- Server Actions body limit has been increased to 10mb for uploads in `next.config.ts`.

## Localization (i18n)
This project includes built-in localization support for UI strings and translatable content.

- Supported locales: `en` (English), `es` (Spanish), `ur` (Urdu), `ar` (Arabic)
- UI translations live in the `i18n/` folder. See [i18n/index.ts](i18n/index.ts) for the `uiT()` helper used across the app.
- Content translations (portable fields with multiple locales) are resolved with the `t()` helper in [lib/translator.ts](lib/translator.ts).

Usage examples:

- Resolve a UI string by key:

```ts
import { uiT } from './i18n';
const label = uiT('es', 'nav.home'); // fetches the 'nav.home' string for Spanish
```

- Resolve a translatable content field (stored as object with locale keys):

```ts
import { t } from './lib/translator';
const title = t(post.title, 'ar');
```

Adding a new language:

1. Add a new file `i18n/xx.ts` exporting the dictionary (replace `xx` with your locale code).
2. Import and register the dictionary in [i18n/index.ts](i18n/index.ts).
3. Provide translated content in Sanity or in code where applicable.

Notes:
- The UI helper `uiT(lang, key, fallback)` will fall back to `en` by default.
- The content translator `t(field, lang, fallback)` will return `''` when no value is available.

## Where to look next
- App entry: `app/layout.tsx` and `app/page.tsx`
- API helpers: `lib/` and `api/`
- Sanity schema/types: `sanity/` and `schemas/`

## License
No license specified. Add a `LICENSE` file if you wish to make this project open source.

---

If you'd like, I can also:
- add badges (build, license, coverage)
- create a short troubleshooting / deployment section tailored for Vercel
- extract an environment checklist script

File: [README.md](README.md)
