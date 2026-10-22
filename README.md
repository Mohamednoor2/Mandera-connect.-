# ManderaConnect — installable marketplace PWA

ManderaConnect is a Progressive Web App (PWA): one codebase that works as an online website and can be installed from a browser on Android. It is not a native APK. You do not need to pay an app-store fee to test it.

## What is included
- Responsive marketplace UI for mobile and desktop
- Search and category filtering
- Listing detail view with WhatsApp and phone contact
- Post-listing form
- Local device-only mode for immediate testing
- Optional shared online listings using a free Supabase project
- PWA manifest and service worker for installation/offline shell
- SQL schema and setup guide

## Important demo warning
The initial sample listings are examples, not verified real businesses. In device-only mode, posts are stored only in that browser on that device and are not shared with other people. To make posts visible to everyone, connect Supabase and deploy the site over HTTPS.

## Option A — try it on a computer
Serve this folder from a local web server (service workers/PWA install generally require HTTPS or localhost). For example, if Python is installed:
`python -m http.server 8000`
Then visit `http://localhost:8000`.

Opening `index.html` directly with `file://` lets you inspect some UI but does not enable PWA installation or service-worker caching.

## Option B — free online deployment with GitHub Pages
1. Create/sign in to a GitHub account.
2. Create a new public repository, e.g. `manderaconnect`.
3. Upload all files and the `icons` folder from this project. Keep the folder structure.
4. In the repository, open **Settings → Pages**.
5. Under build/deployment, choose **Deploy from a branch**, select `main` and `/ (root)`, then Save.
6. Wait for GitHub Pages to publish the site. It will show a URL similar to `https://YOUR-USERNAME.github.io/manderaconnect/`.
7. Open the URL on your Android phone in Chrome.

## Install on Android
1. Open the deployed HTTPS site in Chrome.
2. Open Chrome's three-dot menu.
3. Tap **Install app** or **Add to Home screen** (the wording varies).
4. Confirm. ManderaConnect will appear as an icon on your home screen.
5. Open it and test search, categories, details, and posting.

## Option C — make listings shared online for free (Supabase)
This is required for different people to see each other's listings.

1. Create a free project at https://supabase.com/ .
2. In the Supabase dashboard, open **SQL Editor → New query**.
3. Copy the contents of `supabase-schema.sql` into the editor and run it.
4. Open **Project Settings → API** (or API Keys, depending on dashboard version). Copy the Project URL and the public `anon` / publishable key. Never copy a `service_role` or secret key into a public website.
5. Edit `config.js`:
   ```js
   window.MANDERACONNECT_CONFIG = {
     supabaseUrl: "https://YOUR-PROJECT-REF.supabase.co",
     supabaseAnonKey: "YOUR_PUBLIC_ANON_OR_PUBLISHABLE_KEY"
   };
   ```
6. Upload the updated `config.js` to GitHub, replacing the old file. Wait for the site to redeploy, then reload the site on your phone.
7. Test with two browsers/devices: publish a listing on one, then check that it appears on the other.

The public schema permits anyone to read published listings and create new ones. This is an intentionally simple MVP and can be spammed. Do not collect sensitive information. Before public promotion, add moderation, abuse reporting, spam protection and ideally accounts. A public anon key is designed to be exposed in a frontend; a service-role key is not.

## Testing checklist
- [ ] Site opens on Android Chrome and desktop browser
- [ ] Search and category filters work
- [ ] A listing detail opens
- [ ] WhatsApp link opens with a prefilled message (test with a real number only)
- [ ] Local post works in device-only mode
- [ ] After Supabase setup, a listing posted from one device appears on another
- [ ] App can be installed from Chrome
- [ ] Reload works; cached app shell opens after the first successful visit

## Limitations of this version
- No native APK or Play Store listing
- No sign-in, payment processing, chat inbox, image uploads, seller verification, moderation dashboard or reporting workflow
- No guarantee of revenue: the app is a tool; income requires attracting real users and choosing a transparent business model
- Supabase/GitHub may change their free-tier terms. Check their current terms before relying on them for a business.

## Suggested first launch
Start with a small verified pilot: 10–20 real sellers and service providers in Mandera. Ask permission before posting their contact details. Keep job and property posts carefully checked. Consider later earning a disclosed fee for optional featured listings, but don't promise customers sales or charge people for fake job offers.
