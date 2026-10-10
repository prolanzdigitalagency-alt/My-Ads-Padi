# My Ads Padi

Front end for the My Ads Padi AI Ads Agent. One static file (`index.html`), no build step, logo embedded.

## Deploy
1. Replace `index.html` in the GitHub repo (prolanzdigitalagency-alt/My-Ads-Padi-2) with this one.
2. Vercel redeploys on push. No settings change needed.

## Login
Everyone logs in with email and password. The first account ever created becomes the admin and needs no invite code. After that, new accounts need the invite code the admin sets under the gear icon (Account). Sessions last 30 days. Each account only ever sees its own campaigns, brand assets, flyers and pages; the backend works out the account from the login token on every call.

## Service endpoints
All in the `API` object at the top of the script. Every call except login and register sends the login token. A 401 from any endpoint sends the user back to the login screen.

| Feature | Path | Live |
|---|---|---|
| Log in, create account, me, log out, invite code | `/ads-padi/auth/login`, `/register`, `/me`, `/logout`, `/invite` | yes |
| Spy on Competitors, search | `/ads-padi/spy/search` | yes |
| Spy on Competitors, use picked ads in a campaign | `/ads-padi/spy/use` | yes |
| Campaign Research, list everything | `/ads-padi/campaign/list` | yes |
| Campaign Research, review status and performance | `/ads-padi/campaign/status` | yes |
| Campaign Research, review link (create, new link, switch off) | `/ads-padi/review/create` | yes |
| Public read-only review page | `GET /ads-padi/review?t=<token>` | yes |
| New Campaign, steps 1 and 2 | `/ads-padi/campaign/save` | yes |
| New Campaign, step 3 write and pick offers | `/ads-padi/offers/generate`, `/offers/select` | yes |
| New Campaign, step 4 and Short Form Videos | `/ads-padi/campaign/generate` | yes |
| Brand Assets, upload, list, delete | `/ads-padi/brand/upload`, `/list`, `/delete` | yes |
| AI Graphics | `/ads-padi/graphics/design` | yes |
| Landing Pages, build and revise | `/ads-padi/landing/build` | yes |
| Landing Pages, publish | `/ads-padi/landing/publish` | yes |
| AI Videos, and turning short form scripts into videos | `/ads-padi/video/generate`, `/video/status` | not yet (needs the video tool) |

## Screens
- Spy on Competitors: search a niche or look up a brand on Facebook and Instagram, TikTok or LinkedIn, by country. Shows what is working (hooks, offers, angles, formats) and the live ads, longest running first. Tick ads and use them in a campaign; Generate Copy models their structure. Results are saved for 6 hours; "Get fresh results" pulls them again. TikTok only publishes top ads for the UK, US, Canada and the UAE, so African countries get the UK top ads, and the page says so.
- Campaign Research: every campaign from the backend with its offer, copy, flyers, pages, the niche research and the competitor ads picked. Set the review status by hand (Draft, Sent for approval, Approved, Sent to client, Client approved), the performance and notes on what is working. Make a read-only review link to send yourself; make a new link or switch it off any time. There are no approve buttons in the tool. Parts that still have blanks are flagged.
- New Campaign: four steps. Offers mark the details the agent does not know as blanks ([number], [gift]); you fill them in on the card before you can pick the offer, so no blank reaches your ads.
- Brand Assets: upload files or links (10 MB per file). The agent reads each one and builds brand intelligence (who you are, colours, voice, customer words, results, objections, winning angles, numbers, what to avoid). The panel shows "Updating" while it learns.
- Short Form Videos: skits, reels and POVs for the campaign you pick, 1 to 5 at a time. Works before an offer is chosen. Turning a script into a video switches on when the video tool is connected.
- AI Videos: waiting for the video tool.
- AI Graphics: a flyer from the campaign's flyer copy (or typed copy), portrait 4:5 or square, with your logo, colours, product photo and contact line. With no product photo, it uses your first product image from Brand Assets, or makes an AI photo.
- Landing Pages: build from the campaign or a typed brief, with the WhatsApp number leads go to and your reviews (photos and videos upload to Brand Assets first). Review on desktop or phone, tell the agent what to change, publish. A page with blanks cannot be published until the blanks are filled.

## Long jobs
The server cuts a request at 180 seconds. Copy, pages and flyers keep going on the backend when that happens, so the page waits and shows the result the moment it is saved.
