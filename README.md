# Vice City Explorer

Vice City Explorer is an unofficial fan-made web platform for discovering and browsing Vice City-inspired locations through an interactive map and a neon, synthwave interface.

> This is an independent fan project. It is not affiliated with, endorsed by, or connected to Rockstar Games.

## Features

- Cinematic, skippable intro with reduced-motion support
- Responsive neon/synthwave design
- Interactive Leaflet map with OpenStreetMap data
- Live location cards and district/category details
- Supabase email/password authentication
- Protected member dashboard
- Role-based admin tools
- Admin location creation with server-side Zod validation
- Row Level Security for protected profiles, locations, and favourites
- Clear setup and database connection states

## Tech Stack

- Next.js 15
- React 19
- Tailwind CSS 4
- Leaflet and React Leaflet
- Supabase Auth and Supabase Database
- Zod

## Prerequisites

- Node.js 18.18 or newer
- npm
- A Supabase project

## Local Setup

1. Install dependencies:

   ```bash
   npm install
   ```

2. Create a Supabase project at [supabase.com](https://supabase.com).

3. Open the Supabase SQL Editor and run the complete contents of [`supabase/schema.sql`](./supabase/schema.sql).

4. Create `.env.local` from the example file:

   ```bash
   cp .env.example .env.local
   ```

   Windows PowerShell:

   ```powershell
   Copy-Item .env.example .env.local
   ```

5. Add the project URL and anonymous key from **Supabase Project Settings > API**:

   ```env
   NEXT_PUBLIC_SUPABASE_URL=https://YOUR-PROJECT.supabase.co
   NEXT_PUBLIC_SUPABASE_ANON_KEY=your-anon-key
   ```

6. Start the development server:

   ```bash
   npm run dev
   ```

7. Open [http://localhost:3000](http://localhost:3000).

## Creating an Admin Account

1. Open `/login` and sign up.
2. In the Supabase SQL Editor, promote the account:

   ```sql
   update public.profiles
   set role = 'admin'
   where id = (
     select id
     from auth.users
     where email = 'you@example.com'
   );
   ```

3. Return to `/dashboard`. The admin location form will now be available.

## Available Scripts

| Command | Description |
| --- | --- |
| `npm run dev` | Start the local development server |
| `npm run build` | Create an optimized production build |
| `npm run start` | Run the production build |
| `npm run lint` | Run ESLint |

## Pages

- `/` — homepage, introduction, featured locations, and platform highlights
- `/locations` — location catalogue with live database results
- `/map` — interactive city map
- `/login` — email/password sign-up and sign-in
- `/dashboard` — protected account area and admin location tools
