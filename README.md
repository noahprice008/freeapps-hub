# ELEVEX Apps hub (elevexapps.elevex.digital)

Static one-page site: `index.html` + `img/` + `v/`. Replaces the former FreeApps hub (freeapps.elevex.digital).
`v/` still holds the TikTok videos and covers that the n8n queues download, so the old hostname keeps serving them.

## Deploy (same Docker + Caddy + 2-minute cron pattern as before)
1. DNS (Hostinger): add an A record `elevexapps` -> the VPS IP. Keep the existing `freeapps` A record.
2. Caddy: serve both hostnames from the same container, and redirect only the old *pages*:

```
elevexapps.elevex.digital {
    reverse_proxy freeapps-hub:80
}
freeapps.elevex.digital {
    @pages not path /v/* /img/*
    redir @pages https://elevexapps.elevex.digital{uri} permanent
    reverse_proxy freeapps-hub:80
}
```

3. Reload Caddy, then check https://elevexapps.elevex.digital and https://elevexapps.elevex.digital/v/ru01_four.mp4 load.
4. Tester form posts to the n8n webhook `https://n8n.elevex.digital/webhook/elevexapps-testers`.
