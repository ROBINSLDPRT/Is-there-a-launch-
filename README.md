#Is There A Launch?

Built for the Stardance hackathon. Pulls upcoming rocket launches — date, site, vehicle, mission summary — and lets you search through them.

Single static page. No framework, no build step. Everything lives in index.html: markup, styles, and the fetch logic.

Data:

-Launches come from the Launch Library 2 API (thespacedevs.com), called client-side on page load:

GET https://ll.thespacedevs.com/2.2.0/launch/upcoming/?limit=30&mode=detailed

-No API key required for this tier. It is rate-limited — I couldn't find an exact published number, so treat repeated hard refreshes during testing with some caution. A 429 is handled (the UI shows an error state instead of failing silently), but you'll notice it if you hammer the endpoint.

-"Load more" walks the next field the API returns rather than tracking offsets manually.

-Running it locally

-Nothing to install. Serve the folder with any static server:

python3 -m http.server

-Opening index.html directly via file:// mostly works too, but fetch() behaves more reliably over http://, so use a local server if the launch list doesn't populate.

Deployment:

-Static hosting on GitHub Pages, index.html at the repo root. No CI, no build output to manage — push and Pages serves it as-is.

Known limitations:
-Search is client-side and only filters what's already loaded (30 launches by default). A match that only exists on a later page won't show up until "Load more" is clicked first.
-No caching. Every page load re-fetches from the API.
-The hero image is a stock NASA photo pulled from Wikimedia Commons (Falcon 9 / CRS-10, Kennedy Space Center), used as a placeholder until there's a real image to swap in.
-No dependencies, intentionally. Kept it vanilla JS to avoid dealing with a bundler under a hackathon deadline — worth revisiting if the project grows past one file.
Credits:

Launch data: The Space Devs — Launch Library 2. Hero image: NASA, via Wikimedia Commons.
