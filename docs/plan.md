# Westshore Consulting: Self-Hosted Website + Google Workspace + Cloudflare Plan

## 1. Goals

This plan supports the foundational setup of **Westshore Consulting Limited**, including infrastructure, email, DNS, and incorporation preparation.

### Summary

* **Incorporation NR:** NR 3357162 (Approved, expires Aug 20, 2025)
* **Primary Domain:** [westshoreconsulting.co](https://westshoreconsulting.co)
* **Alias Domain:** [westshore.consulting](https://westshore.consulting)

### Objectives

* Use `westshoreconsulting.co` for primary domain (email + website)
* Use `westshore.consulting` as redirect alias
* Self-host website on personal infrastructure using Docker
* Use `cloudflared` for tunneling with Cloudflare DNS
* Host a static site (Hugo, Astro, or plain HTML)
* Complete Google Workspace setup to begin incorporation

---

## 2. Google Workspace Setup

### Primary Domain: `westshoreconsulting.co`

* Signup at: [https://workspace.google.com/](https://workspace.google.com/)
* Plan: Business Standard (\$14.40 CAD/mo)
* Email accounts: `paul@westshoreconsulting.co`, aliases like `admin@`, `info@`
* Setup DNS in Cloudflare:

  * MX records for Gmail
  * TXT for SPF/DKIM/DMARC
  * `google-site-verification` TXT

---

## 3. Cloudflare DNS Setup

### For `westshoreconsulting.co`

* `CNAME @` → `your-tunnel-id.cfargotunnel.com`
* `CNAME www` → `your-tunnel-id.cfargotunnel.com`

### For `westshore.consulting`

* `CNAME @` → `your-tunnel-id.cfargotunnel.com`
* Page Rule or Tunnel redirect to `https://westshoreconsulting.co`

---

## 4. Self-Hosted Docker Setup

### New Service: `westshore-site`

Add to `storage-compose.yml`:

```yaml
  westshore-site:
    <<: *net-restart-sec
    container_name: westshore-site
    hostname: westshore-site
    image: nginx:alpine
    volumes:
      - $DATA_DIR/westshore-site:/usr/share/nginx/html:ro
    environment:
      <<: *default-env
    labels:
      - flame.type=app
      - flame.name=westshore
      - flame.url=https://westshoreconsulting.co
      - flame.icon=web
    healthcheck:
      test: ["CMD", "wget", "--spider", "-q", "http://localhost"]
      interval: 30s
      timeout: 10s
      retries: 3
```

Put built site files (Hugo/Astro/static HTML) in `$DATA_DIR/westshore-site`

---

## 5. Cloudflared Setup

### Tunnel Config Example:

```yaml
# $DATA_DIR/cloudflared/config.yml

 tunnel: westshore-tunnel-id
 credentials-file: /etc/cloudflared/creds.json

 ingress:
   - hostname: westshoreconsulting.co
     service: http://westshore-site:80
   - hostname: www.westshoreconsulting.co
     service: http://westshore-site:80
   - hostname: westshore.consulting
     service: https://westshoreconsulting.co
   - service: http_status:404
```

Mount into container:

```yaml
    volumes:
      - $DATA_DIR/cloudflared/config.yml:/etc/cloudflared/config.yml
      - $DATA_DIR/cloudflared/creds.json:/etc/cloudflared/creds.json
```

---

## 6. Action Steps

* [ ] Signup and verify Google Workspace
* [ ] Add required DNS records to Cloudflare
* [ ] Set up email aliases
* [ ] **Complete domain and email setup (required to begin incorporation)**
* [ ] Create Hugo/Astro/static site
* [ ] Add `westshore-site` service to compose file
* [ ] Create Cloudflare Tunnel + config
* [ ] Deploy tunnel via `cloudflared tunnel run westshore`
* [ ] Test email delivery and TLS on both domains
* [ ] File incorporation using NR 3357162 before August 20, 2025

---

## 7. Optional Enhancements

* Create branded `robots.txt`, `favicon.ico`, and social image
* Setup Uptime Kuma monitoring for site health
* Add Gitea Pages or GitHub Actions for automated static site deploys
* Use `analytics.giff.ca` (self-hosted Plausible or Matomo) for web stats
