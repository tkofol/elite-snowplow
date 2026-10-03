# Elite Snow Services

Static site for [elitesnowservices.com](https://elitesnowservices.com), hosted on GitHub Pages with DNS on Cloudflare.

```
index.html            page markup
assets/css/style.css  all styling
assets/images/        logo and photos
CNAME                 custom domain for GitHub Pages
.nojekyll             serve files as-is (no Jekyll build)
```

Preview locally: `python3 -m http.server` then open http://localhost:8000.

## Deploy to GitHub Pages

1. Push this folder to a GitHub repo (e.g. `elite-snowplow`) on the `main` branch.
2. Repo **Settings → Pages**: Source = *Deploy from a branch*, Branch = `main`, folder = `/ (root)`.
3. Under **Custom domain**, enter `elitesnowservices.com` (matches the `CNAME` file) and save.
4. Once DNS is verified and the certificate is issued, tick **Enforce HTTPS**.

## Cloudflare DNS

In Cloudflare → the `elitesnowservices.com` zone → **DNS → Records**, add:

| Type  | Name  | Content                   | Proxy     |
|-------|-------|---------------------------|-----------|
| A     | `@`   | `185.199.108.153`         | DNS only  |
| A     | `@`   | `185.199.109.153`         | DNS only  |
| A     | `@`   | `185.199.110.153`         | DNS only  |
| A     | `@`   | `185.199.111.153`         | DNS only  |
| AAAA  | `@`   | `2606:50c0:8000::153`     | DNS only  |
| AAAA  | `@`   | `2606:50c0:8001::153`     | DNS only  |
| AAAA  | `@`   | `2606:50c0:8002::153`     | DNS only  |
| AAAA  | `@`   | `2606:50c0:8003::153`     | DNS only  |
| CNAME | `www` | `<github-username>.github.io` | DNS only  |

Remove any existing A/AAAA/CNAME records for `@` and `www` that point elsewhere.

Leave the records **DNS only (grey cloud)** until GitHub shows the domain as verified and HTTPS is enforced. After that you can switch them to **Proxied (orange cloud)** if you want Cloudflare caching; if you do, set **SSL/TLS → Overview** to **Full (strict)** to avoid redirect loops.

Optional: verify the domain under GitHub **Settings → Pages → Verified domains** (adds a TXT record) to stop anyone else claiming it on GitHub Pages.
