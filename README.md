# Ken Digital Studio — Website

A static, no-build-step website for Ken Digital Studio (Malakpet, Hyderabad).
Open `index.html` in a browser, or open the folder in VS Code and use the
"Live Server" extension for auto-reload while editing.

## What's in here

```
index.html       Home
services.html    Service list + prices (placeholder prices — update these)
portfolio.html   Contact-sheet style gallery (placeholder frames — add real photos)
book.html        Booking request form -> hands off to WhatsApp
about.html       Studio story + map
contact.html     Contact details + map + enquiry form -> hands off to email
css/styles.css   All styling (colours/fonts are CSS variables at the top)
js/main.js       Mobile nav, IndexedDB storage + form handling
admin.html        Local studio desk for saved bookings and enquiries
```

## Before you publish, do these 4 things

1. **Studio email** — the site is configured with
   `kenstudio.malakpet@gmail.com` in `js/main.js`.
2. **Real photos** — in `portfolio.html`, replace the `.frame-shot` divs with
   actual `<img>` tags (see the HTML comment above the gallery). Add your
   images to the `images/` folder.
3. **Real prices** — `services.html` has placeholder prices marked with a
   note; update them to match what you actually charge.
4. **Double-check the phone number** — the WhatsApp number is pulled from
   the studio's public Google Maps listing (+91 99630 83437). Confirm it's
   the number you want customers messaging before going live.

## Database

The site can use Supabase for shared booking and enquiry submissions, with IndexedDB as a local fallback. To enable it:

1. Create or open the Supabase project for `dlzgznqriheiydkbiriv`.
2. Run `supabase/schema.sql` in the Supabase SQL Editor.
3. Copy the project's publishable/anon key into `js/supabase-config.js` as `anonKey`.
4. Serve the folder through Live Server or another HTTP server and submit a test booking.

The public forms only use the publishable key and the schema permits inserts for anonymous visitors. Reads and status updates are intentionally not public; `admin.html` continues to show local records until an authenticated admin flow is added. Do not put a service-role key in this website.

## Why there's no live booking calendar yet

The form still does not auto-confirm availability. It saves the request locally, then builds a pre-filled WhatsApp message to the studio's number. The studio should confirm the exact time manually.

### If/when you want a real booking calendar + payments

That needs an actual backend + database, which is a separate project:
- A simple version: a small Node/Express (or similar) API + a database
  (Postgres/SQLite) storing bookings, with an admin view to confirm/reject
  requests.
- Payments (UPI/cards) only make sense once that backend exists, since a
  payment status should never be trusted from the browser alone.

Happy to help build that as a phase 2 whenever you're ready — it's a
meaningfully bigger project than this static site, so it's worth doing as
its own step rather than bolting on halfway.

## Deploying

Since it's plain HTML/CSS/JS, you can host it for free on:
- Netlify (drag-and-drop the folder)
- Vercel
- GitHub Pages

No build step needed — just upload the folder as-is.
