# Westshore Consulting Setup Tracker

## 🚀 Current Milestones

| Task                                                    | Owner | Status | Notes                                                               |
| ------------------------------------------------------- | ----- | ------ | ------------------------------------------------------------------- |
| Register domains                                        | Paul  | ✅      | `westshoreconsulting.co` and `westshore.consulting` acquired        |
| Select Workspace plan                                   | Paul  | ✅      | Business Standard chosen                                            |
| Create Google Workspace account                         | Paul  | ⬜      | Pending Google verification                                         |
| Verify domain with Google                               | Paul  | ⬜      | Add TXT record in Cloudflare                                        |
| Configure MX records                                    | Paul  | ⬜      | Point to Google mail servers                                        |
| Setup SPF/DKIM/DMARC                                    | Paul  | ⬜      | Harden email delivery and anti-spam                                 |
| Create email aliases                                    | Paul  | ⬜      | e.g., `admin@`, `info@`, `contact@`                                 |
| **Complete domain and email setup (pre-incorporation)** | Paul  | ⬜      | Grouped milestone; required before incorporation filing             |
| Build website                                           | Paul  | ⬜      | Hugo/Astro/static site structure TBD                                |
| Add `westshore-site` service to compose                 | Paul  | ⬜      | NGINX + volume mount for static HTML                                |
| Deploy static site                                      | Paul  | ⬜      | Drop build into `$DATA_DIR/westshore-site`                          |
| Create Cloudflare Tunnel                                | Paul  | ⬜      | Use `cloudflared tunnel create westshore`                           |
| Configure tunnel YAML                                   | Paul  | ⬜      | Define routing for all hostnames                                    |
| Deploy tunnel container                                 | Paul  | ⬜      | Mount config + creds.json in cloudflared                            |
| Set CNAMEs in Cloudflare                                | Paul  | ⬜      | Point all domains to tunnel ID                                      |
| Test DNS + TLS                                          | Paul  | ⬜      | Validate HTTPS and email on `.co` domain                            |
| Setup redirect from `.consulting`                       | Paul  | ⬜      | Use tunnel config to 301 redirect                                   |
| Add Flame dashboard entries                             | Paul  | ⬜      | For `westshore-site`, etc.                                          |
| File incorporation using NR 3357162                     | Paul  | ⬜      | Approved name: "Westshore Consulting Limited", expires Aug 20, 2025 |

## 🛠️ Optional Enhancements

| Feature                             | Status | Notes                                        |
| ----------------------------------- | ------ | -------------------------------------------- |
| Add CI/CD deploy via GitHub Actions | ⬜      | Auto-build + copy to NGINX volume            |
| Setup web analytics                 | ⬜      | Use self-hosted Plausible or Matomo          |
| Add SEO assets                      | ⬜      | `robots.txt`, `sitemap.xml`, `favicon.ico`   |
| Add uptime monitor                  | ⬜      | Uptime Kuma check for public domain          |
| Branding elements                   | ⬜      | Email signature, favicon, Open Graph banners |
