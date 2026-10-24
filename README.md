# MixVault 254 — Online MP3 / MP4 Download Website

This is a deployable web app starter for **MixVault 254**. It includes:
- Email/password account registration and login using Supabase Auth
- Downloads gated behind sign-in
- Private cloud file storage with short-lived signed links
- Admin-only upload and delete area
- Search, audio/video listing, responsive dark DJ-style UI

## What you need
- A free Supabase project (database, auth and private storage)
- A static website host such as Netlify, Vercel, or Cloudflare Pages

## Step 1 — Create the Supabase backend
1. Create a project at https://supabase.com/
2. In the Supabase dashboard, open **SQL Editor** and run the full `supabase/setup.sql` script.
3. Go to **Storage**, create a bucket named `mixes`, and make sure it is **Private** (not public).
4. In **Project Settings → API** (or the API keys section), copy the Project URL and the anon/publishable key. Never use the `service_role` / secret key in frontend code.

## Step 2 — Configure the website
1. Open `index.html` in a text editor.
2. Replace:
   - `PASTE_SUPABASE_PROJECT_URL_HERE` with your Supabase Project URL
   - `PASTE_SUPABASE_ANON_OR_PUBLISHABLE_KEY_HERE` with your anon/publishable key
3. Save the file.

## Step 3 — Create your admin account
1. Deploy the website (Step 4), then open it and sign up with your own email.
2. In Supabase Dashboard → SQL Editor, run this query, replacing the email:
   ```sql
   update public.profiles set role = 'admin' where email = 'YOUR_EMAIL';
   ```
3. Sign out and sign back in. The **Add a mix or video** admin panel will appear.

## Step 4 — Publish online
For Netlify:
1. Create an account at https://www.netlify.com/
2. Drag the folder containing `index.html` to Netlify's manual deploy area, or connect a Git repository containing the file.
3. Netlify will give you a public website URL. You can connect a custom domain later.

You can also use Vercel or Cloudflare Pages to host this static app.

## Security and behaviour
- Visitors can browse the public mix listings, but must sign in to preview or download files.
- Download links are signed and expire after 2 minutes. Preview links expire after 15 minutes.
- Storage is private. The database and storage policies only allow admins to upload/delete.
- Use Supabase Auth email confirmation settings as desired.
- This starter has no payment/subscription system and no automated moderation.
- Upload limit in this front end is 250 MB; your Supabase storage plan and project upload settings may impose lower limits.
- You must configure Supabase and deploy it; this ZIP does not create a hosting account or publish itself automatically.
- Only distribute media you own or have permission to share.

## Files
- `index.html` — responsive website
- `supabase/setup.sql` — database, account profile and private storage policies
