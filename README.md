# FreeApps hub (freeapps.elevex.digital)
Static one-page site: index.html + img/ + v/ (the 22 TikTok videos and covers, referenced by the n8n queue).

## Deploy
1. Push this folder to a GitHub repo (e.g. elevex-digital/freeapps-hub).
2. Same setup as travelplay.fun: Docker (`Dockerfile` = nginx:alpine) behind the project's Caddy, with the 2-minute cron auto-deploy.
3. Caddy block: `freeapps.elevex.digital { reverse_proxy freeapps-hub:80 }`
4. DNS: A record `freeapps` -> your server IP.
5. Check https://freeapps.elevex.digital/v/ru01_four.mp4 loads (n8n downloads videos from there).

Before posting: nothing here needs changing except optionally adding a GA4 ID. Store badges are text pills; swap in official Google Play / App Store badge artwork only once the listings are live.
