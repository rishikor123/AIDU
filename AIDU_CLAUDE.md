# CLAUDE.md — AIDU (AI Education Platform)

This file gives Claude Code the full context for building AIDU. Read it before generating code.

## What we are building
AIDU is a mobile-first web app that helps people learn AI, discover the right AI tools, find AI-related jobs, and connect with others, all in one place. The core insight from our user research: people do not want to juggle many separate AI tools and scattered resources. They want a single, personalized hub that meets them at their skill level and field.

This build is for a working MVP, not the full feature set at once. Prioritize the core loop first (see MVP Scope).

## Validated user research (from 100+ survey responses)
These findings come from real survey data and should drive priorities:

1. Two distinct audiences. Respondents split into **Students** and **Professionals**. Students want AI education, career guidance, and mentorship. Professionals want workplace AI adoption, advanced tools, and networking. The app must segment by user type.
2. Skill varies widely. Familiarity ranged from beginner to expert, so learning content must adapt to a chosen skill level (Beginner, Intermediate, Expert).
3. Field-specific needs. A finance student and a marketing professional need different resources, so recommendations should reflect the user's field or specialization.
4. One place, not many. A recurring frustration was switching between different AI tools for different tasks. AIDU's value is consolidation and personalization.
5. Career reassurance. Many respondents worried about AI replacing jobs. The framing should position AI as career growth, not threat.

Validated demand was high: respondents said they would use a platform offering AI education, tool recommendations, and professional networking.

## Target users
- **Student:** education, structured learning paths, career guidance.
- **Professional:** workplace AI adoption, advanced tools, networking.
- Each user also picks a **skill level** (Beginner, Intermediate, Expert) and **interests** during onboarding.

## Screens (from the Figma frames in /design)
Build these to match the exported frames. The design is mobile-first, dark theme with a purple/lavender accent, with a bottom navigation bar (Home, Search, Pages, Profile).

1. **Create Account** (two steps): email, username, password fields.
2. **Reset Password**: new password and confirm.
3. **User Type Selection / Onboarding**: "Choose your Interests" (topic chips the user toggles) and "Choose your Skill Level" (Beginner, Intermediate, Expert), then Done.
4. **Home**: AIDU logo, hero, login entry point.
5. **Dashboard**: aggregated feed with sections for News, Marketplace, Jobs, and Learning Hub.
6. **Search**: recent searches and popular searches.
7. **News**: article cards (AI in the user's field, market trends).
8. **Learning Hub**: search, Recent Posts, Top Posts.
9. **Jobs**: searchable list of AI roles (e.g., AI Data Engineer, Data Scientist, Machine Learning Specialist) with filters.
10. **Marketplace**: directory of AI tools and services with ratings.
11. **Profile**: name, Edit Profile, Sign Out.
12. **Pages / New Page**: create a post or page with Title, Date/Time, and content.

## MVP Scope (build first)
Build the core loop end to end before anything else:
1. Create Account and auth.
2. Onboarding (interests + skill level + user type).
3. Dashboard / Home.
4. Learning Hub with one real AI feature (personalized learning recommendations or an AI tutor chat).

Defer to later phases: Marketplace, Jobs, News, Search, and Pages. Stub these as simple placeholder screens so navigation works, then fill them in.

## Tech stack
- **Frontend:** Next.js (App Router) + React + Tailwind CSS. Mobile-first.
- **Backend / auth / database:** Supabase (Postgres + Auth).
- **AI features:** Anthropic Claude API (no API key in client; route through a server action or API route).
- **Deployment:** Vercel.

## AI features (Claude API)
- **Personalized learning path:** given the user's interests, skill level, and field, generate a structured learning path with steps and recommended topics.
- **AI tutor chat:** answer the user's AI questions, adapted to their skill level.
- **Tool recommendations (later):** suggest AI tools from the marketplace matched to the user's field and goals.
Ground every AI response in the user's stored profile (type, skill, interests). Never put the API key in client code.

## Suggested data model (Supabase)
- `profiles`: id, user_type ('student' | 'professional'), skill_level, field, interests (array), display_name.
- `learning_paths`: id, user_id, title, steps (jsonb), created_at.
- `posts`: id, author_id, title, body, created_at (for Learning Hub / Pages).
- `tools`: id, name, category, description, rating (for Marketplace, later).
- `jobs`: id, title, company, description, tags (for Jobs, later).

## Conventions
- Server components by default; use client components only where interaction requires it.
- Keep all Claude API calls server-side (API route or server action).
- Use TypeScript.
- Match the dark theme and purple accent from the design frames.
- Commit often with clear messages.

## Commands (fill in once scaffolded)
- `npm run dev` — start dev server
- `npm run build` — production build
- `npm run lint` — lint

## Build order for Claude Code
1. Scaffold Next.js + Tailwind + Supabase; set up the dark theme and bottom nav shell.
2. Implement auth (Create Account, Reset Password) with Supabase.
3. Build onboarding (interests + skill level + user type) and save to `profiles`.
4. Build the Dashboard / Home shell with placeholder sections.
5. Build the Learning Hub and wire in the first Claude API feature (personalized path or tutor).
6. Deploy to Vercel.
7. Then iterate: Marketplace, Jobs, News, Search, Pages.

## Notes
- Design frames are in the `/design` folder. Feed them to Claude Code one screen at a time when building that screen.
- This is a portfolio and hackathon-origin project (Rice Design-a-thon 2025). Keep it clean and demo-ready.
