# 4th and Bailey — BIMI Record Assets

**Brand Indicators for Message Identification (BIMI)** for [4thandbailey.com](https://4thandbailey.com)

This repository hosts the publicly accessible brand logo asset used by the BIMI standard to display the 4th and Bailey logo directly inside supporting email inboxes (Gmail, Yahoo! Mail, Apple Mail, and others), helping recipients visually identify and trust email sent from our domain.

---

## What Is BIMI?

BIMI (Brand Indicators for Message Identification) is an email authentication standard that enables organizations to display their official brand logo next to authenticated email messages in the recipient's inbox. It builds on top of DMARC, SPF, and DKIM to provide a verified visual trust signal — reducing phishing risk and increasing brand recognition at the point of delivery.

---

## Repository Contents

| File | Description |
|---|---|
| `logo.svg` | 4th and Bailey brand logo in SVG Tiny P/S format (256×256px), served via GitHub Pages for BIMI logo display |

---

## BIMI DNS Record

The following TXT record is published in DNS for `4thandbailey.com`:

```
Host:  default._bimi.4thandbailey.com
Type:  TXT
TTL:   3600
Value: v=BIMI1; l=https://4thandbailey.github.io/bimi/logo.svg;
```

> **Note:** A Verified Mark Certificate (VMC) (`a=` tag) is not currently implemented. Adding a VMC in the future will enable the blue verified checkmark in Gmail.

---

## Email Authentication Stack

BIMI requires a fully enforced DMARC policy. The current authentication configuration for `4thandbailey.com` is:

### DMARC
```
v=DMARC1; p=reject; sp=reject; rua=mailto:postmaster@4thandbailey.com;
ruf=mailto:postmaster@4thandbailey.com; rf=afrf; pct=100; ri=86400; fo=1;
```

| Tag | Value | Meaning |
|---|---|---|
| `p=reject` | reject | Unauthorized mail is rejected outright |
| `sp=reject` | reject | Subdomains are equally protected |
| `pct=100` | 100% | Policy applies to all mail |
| `rua` | postmaster@ | Aggregate reports sent daily |
| `ruf` | postmaster@ | Forensic failure reports enabled |
| `fo=1` | Any failure | Reports generated on any SPF or DKIM failure |

### DMARC Aggregate Report — Google (May 8, 2026)

The most recent DMARC aggregate report from Google (`Report-ID: 6956618357060108219`) covering the period **May 8, 2026** confirms the following results across 7 message records:

| Source IP | Count | DKIM | SPF | Disposition | Sending Infrastructure |
|---|---|---|---|---|---|
| `2a01:111:f403:c100::f` | 1 | ✅ pass | ✅ pass | none | Microsoft 365 (selector1) |
| `209.85.220.41` | 2 | ✅ pass | ⚠️ fail* | none | Google (fd selector) |
| `44.192.35.151` | 1 | ✅ pass | ✅ pass | none | AWS / fddkim subdomain |
| `2a01:111:f403:c101::7` | 1 | ✅ pass | ✅ pass | none | Microsoft 365 (selector1) |
| `2a01:111:f403:c112::5` | 1 | ✅ pass | ✅ pass | none | Microsoft 365 (selector1) |
| `44.192.35.9` | 1 | ✅ pass | ✅ pass | none | AWS / fddkim subdomain |
| `2a01:111:f403:c005::5` | 1 | ✅ pass | ✅ pass | none | Microsoft 365 (selector1) |

> **\* SPF note:** The 2 messages from `209.85.220.41` (Google infrastructure) show SPF failing alignment because the RFC5321 `MAIL FROM` domain was `gmail.com` rather than `4thandbailey.com`. However, **DKIM passed** on those messages, so DMARC evaluated as **pass** (DMARC requires either SPF *or* DKIM to pass alignment — not both). No action required; this is expected behavior for mail relayed through Google Workspace or forwarding services.

**Overall:** All 7 records passed DMARC. Zero messages were quarantined or rejected. The domain is clean and ready for `p=reject` enforcement.

---

## Email Service Provider

| Provider | Record |
|---|---|
| **Microsoft 365** | `4thandbailey-com.mail.protection.outlook.com` |
| **DKIM Selectors in use** | `selector1` (M365), `fd` (third-party/forwarding) |

---

## Logo Specifications

| Property | Value |
|---|---|
| Format | SVG Tiny 1.2 (Portable/Secure profile) |
| Dimensions | 256 × 256 px (square canvas) |
| Background | Solid `#f2f2f2` (light gray) |
| Primary brand color | `#0088cc` (blue) |
| Text color | `#666666` (dark gray) |
| Transparency | None (required for BIMI compliance) |

---

## GitHub Pages Hosting

This repository uses **GitHub Pages** to serve `logo.svg` over HTTPS with the correct `Content-Type: image/svg+xml` header required by BIMI validators.

**Live logo URL:**
```
https://4thandbailey.github.io/bimi/logo.svg
```

> ⚠️ Do not use raw GitHub URLs (`raw.githubusercontent.com`) — these do not reliably serve the correct MIME type required by BIMI.

---

## Validation

After publishing the DNS record, validate your BIMI setup at:

- 🔗 [MXToolbox BIMI Checker](https://mxtoolbox.com/bimi.aspx)
- 🔗 [BIMI Group Inspector](https://bimigroup.org/bimi-generator/)

---

## Future Enhancements

- [ ] Obtain a **Verified Mark Certificate (VMC)** from Entrust or DigiCert to enable the Gmail blue verified checkmark
- [ ] Ensure logo trademark registration is complete prior to VMC application
- [ ] Re-validate BIMI record after website relaunch

---

## About 4th and Bailey

**4th and Bailey** is an Information Technology Consulting firm. Our email infrastructure runs on Microsoft 365, with DMARC, DKIM, and SPF fully implemented and enforced across all sending sources.

🌐 [4thandbailey.com](https://4thandbailey.com) · 🐙 [github.com/4thandbailey](https://github.com/4thandbailey)
