# EasyShare Leads — PWA

This app is now fully wired to a live Supabase database (project: easyshare-crm).
It has real login, role-based access (admin vs team lead), and live leads/messages data.

## What's already done
- Supabase project created (Mumbai region, free tier)
- Tables created: `leads`, `messages`, `profiles`
- Row-level security: admins see everything, team leads see only leads assigned to them
- 3 user profiles set up: Nandhini (admin), Farooq (tl), Raju (tl)
- The app (`index.html`) is already pointed at this Supabase project — no code changes needed

## Step 1 — Deploy to Vercel (free, ~5 minutes)
1. Go to vercel.com and sign up (GitHub login is fastest)
2. "Add New Project" → drag-and-drop this whole `pwa` folder
3. Click Deploy
4. You'll get a live URL like `easyshare-leads.vercel.app`
5. (Optional) Point a custom domain like `app.easyshareservices.com` at it in Vercel's project settings

## Step 2 — Turn it into an APK (free, ~2 minutes)
1. Go to pwabuilder.com
2. Paste your Vercel URL
3. "Package for Stores" → "Android" → download the `.apk`
4. Install it on your Android phone (enable "install from unknown sources" if prompted)

## Step 3 — Log in
Each team member logs in with the email + password set up for their Supabase account.
- **Nandhini** sees ALL leads, with a "Viewing: All / Farooq / Raju" dropdown to filter by team lead
- **Farooq** and **Raju** each see only leads assigned to them

## Adding more users later
1. In Supabase: Authentication → Users → Add User (email + password)
2. Copy their User UID
3. Ask Claude to insert their profile row with the right name + role (admin or tl)

## Assigning leads to team leads
Leads currently have no one assigned by default. Ask Claude to either:
- Manually assign specific leads to specific TLs, or
- Set up automatic round-robin assignment in the n8n workflow for new leads

## Connecting n8n to this same database
Your WhatsApp automation (n8n) currently still writes to Google Sheets. To make
the app show real, live leads, ask Claude to swap the Google Sheets nodes in your
n8n workflow for Supabase nodes pointing at this same project — then both the
automation and this app share one live source of truth.
