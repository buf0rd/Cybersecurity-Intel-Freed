# 🛡️ Cybersecurity Intel Free'd

<p align="center">
  <strong>Self-hosted cybersecurity news and intelligence aggregation without the subscription wall.</strong>
</p>

<p align="center">
  Aggregate cybersecurity reporting, advisories, research, RSS/Atom feeds, CVEs, and security-focused news into your own searchable intelligence platform.
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Release-v3.0.0-7cff8a" alt="Release">
  <img src="https://img.shields.io/badge/PHP-8.x-777BB4?logo=php&logoColor=white" alt="PHP">
  <img src="https://img.shields.io/badge/MariaDB-10.x-003545?logo=mariadb&logoColor=white" alt="MariaDB">
  <img src="https://img.shields.io/badge/Apache-2.4-D22128?logo=apache&logoColor=white" alt="Apache">
  <img src="https://img.shields.io/badge/Ubuntu-Server-E95420?logo=ubuntu&logoColor=white" alt="Ubuntu">
  <img src="https://img.shields.io/badge/RSS-Atom-FF6600?logo=rss&logoColor=white" alt="RSS">
  <img src="https://img.shields.io/badge/Self--Hosted-Yes-7cff8a" alt="Self Hosted">
</p>

<p align="center">
  <a href="#overview">Overview</a> •
  <a href="#features">Features</a> •
  <a href="#installation">Installation</a> •
  <a href="#source-management">Sources</a> •
  <a href="#customizing-the-branding">Branding</a> •
  <a href="#security">Security</a> •
  <a href="#troubleshooting">Troubleshooting</a>
</p>

---

## Overview

**Cybersecurity Intel Free'd** is a lightweight, self-hosted cybersecurity news and intelligence aggregation platform designed for defenders who want direct control over the security information they consume.

Cybersecurity reporting is scattered across:

* Government advisories
* Security journalism
* Vendor research
* Independent researchers
* Threat intelligence teams
* DFIR publications
* Malware research
* Vulnerability disclosures
* Ransomware reporting
* Cloud security blogs
* Network security advisories
* Security community resources

Cybersecurity Intel Free'd polls public **RSS and Atom feeds**, normalizes the information, stores it in MariaDB, extracts CVE references, categorizes articles, applies lightweight priority scoring, and presents everything through a searchable web interface.

The application also republishes the normalized intelligence through its own:

* RSS feed
* High-priority RSS feed
* Category RSS feeds
* JSON API
* CVE index

The goal is simple:

> **Security intelligence should be accessible, searchable, customizable, self-hostable, and free from unnecessary platform lock-in.**

---

# Why "Cybersecurity Intel Free'd"?

The name represents three goals.

### Intel freed from fragmentation

Cybersecurity information is distributed across dozens or hundreds of independent sources.

Cybersecurity Intel Free'd brings those sources together.

### Intel freed from platform dependency

The application runs on a standard LAMP stack and does not require a commercial intelligence platform or RSS service.

### Intel freed for reuse

The collected information can be consumed through:

```text
Web UI
RSS
JSON
CVE searches
Category feeds
High-priority feeds
Custom integrations
```

---

# Architecture

```text
                  CYBERSECURITY SOURCES
                           │
          ┌────────────────┼────────────────┐
          │                │                │
          ▼                ▼                ▼
         RSS              Atom         Website URL
                                           │
                                    Feed Auto-Discovery
          │                │                │
          └────────────────┴────────────────┘
                           │
                           ▼
                  SECURE PHP POLLER
                           │
          ┌────────────────┼────────────────┐
          │                │                │
          ▼                ▼                ▼
      Redirects        HTTP Cache          SSRF
    301/302/303       ETag / 304        Protection
      307/308        Last-Modified
          │                │                │
          └────────────────┴────────────────┘
                           │
                           ▼
                  FEED NORMALIZATION
                           │
         ┌─────────────────┼─────────────────┐
         │                 │                 │
         ▼                 ▼                 ▼
   Deduplication        CVE Extraction   Classification
         │                 │                 │
         └─────────────────┼─────────────────┘
                           │
                           ▼
                    PRIORITY SCORING
                           │
                           ▼
                        MariaDB
                           │
        ┌──────────┬───────┼───────┬──────────┐
        │          │       │       │          │
        ▼          ▼       ▼       ▼          ▼
      Web UI     Search   CVEs     RSS      JSON API
```

---

# Benefits

Cybersecurity Intel Free'd provides:

* Centralized cybersecurity reporting
* Self-hosted infrastructure
* No commercial RSS aggregation subscription
* Full control of data and sources
* Per-source polling intervals
* Article deduplication
* CVE extraction
* Topic classification
* Priority scoring
* Searchable historical reporting
* Source filtering
* Category filtering
* RSS output
* JSON API
* Easy branding
* Straightforward SQL access
* Low infrastructure overhead

---

# Features

## Feed Ingestion

* RSS support
* Atom support
* Website feed auto-discovery
* Common feed-path discovery
* Feed validation before saving
* Automatic scheduled polling
* Manual feed polling
* Forced unconditional polling
* Per-source polling intervals
* Source editing
* Source enable/disable
* Source deletion
* HTTP cache reset

---

## HTTP Support

Cybersecurity Intel Free'd understands:

```text
200-299    Successful response
301        Redirect
302        Redirect
303        Redirect
304        Not Modified
307        Redirect
308        Redirect
```

The application supports:

* ETag
* Last-Modified
* If-None-Match
* If-Modified-Since
* Relative redirects
* Redirect validation
* TLS validation
* Request timeouts
* Connection timeouts
* Response size limits
* Maximum redirect limits

---

## Article Processing

Each article may receive:

* Normalized URL
* URL hash
* Publisher
* Author
* Summary
* Publication timestamp
* Discovery timestamp
* CVE references
* Categories
* Priority score
* Last-seen timestamp

---

# Cybersecurity Categories

The default classifier includes:

```text
Vulnerabilities
Ransomware
Malware
Threat Actors
APT / Nation-State
Phishing
Cloud Security
Microsoft
Linux
Apple
Network Security
Data Breaches
Cybercrime
Law Enforcement
DFIR
Threat Intelligence
Security Research
AI Security
ICS / OT
Mobile Security
```

Classification is rule-based by default.

That makes it:

* Fast
* Explainable
* Offline
* Low-resource
* Independent of external AI services

AI enrichment can be added later without making AI a dependency of the ingestion process.

---

# Priority Scoring

Articles receive an internal security priority score.

Signals include phrases such as:

```text
Known Exploited Vulnerability
CISA KEV
Zero-Day
0-Day
Actively Exploited
Exploited in Attacks
Mass Exploitation
Remote Code Execution
RCE
Ransomware
Wormable
Critical Vulnerability
Authentication Bypass
Privilege Escalation
Security Update
Patch Now
CVE
```

Scores are displayed as:

```text
P0
P10
P25
P40
P75
P100
```

The platform provides both:

```text
LATEST
```

and:

```text
HIGH PRIORITY
```

views.

Priority scoring is intended as a **triage aid**, not a replacement for vulnerability management or analyst judgment.

---

# CVE Extraction

Cybersecurity Intel Free'd automatically extracts CVE identifiers from article titles and summaries.

Example:

```text
CVE-2026-12345
```

Conceptually:

```regex
\bCVE-\d{4}-\d{4,7}\b
```

The CVE index is available at:

```text
https://YOUR-DOMAIN/cves.php
```

Example:

```text
https://YOUR-DOMAIN/cves.php?cve=CVE-2026-12345
```

This makes it possible to view multiple articles discussing the same vulnerability.

---

# Publication Date vs Discovery Date

The application tracks both:

```text
published_at
```

and:

```text
discovered_at
```

### `published_at`

The date supplied by the publisher.

### `discovered_at`

The date Cybersecurity Intel Free'd first indexed the article.

The Latest view uses publication-first ordering:

```sql
ORDER BY
    COALESCE(a.published_at, a.discovered_at) DESC,
    a.discovered_at DESC
```

This prevents an old article discovered today from appearing above genuinely new reporting.

Example:

```text
published_at   2026-05-14
discovered_at  2026-08-15
```

The article remains a **May 14 article**.

The discovery timestamp is preserved separately.

---

# Requirements

Recommended environment:

| Component  | Recommended         |
| ---------- | ------------------- |
| OS         | Ubuntu Server       |
| Web Server | Apache 2.4+         |
| PHP        | PHP 8.x             |
| Database   | MariaDB             |
| Scheduler  | cron                |
| TLS        | Let's Encrypt       |
| DNS        | Public hostname     |
| Network    | Outbound HTTP/HTTPS |

---

# Installation

Clone the repository:

```bash
git clone https://github.com/YOUR-USERNAME/YOUR-REPOSITORY.git
cd YOUR-REPOSITORY
```

Make the installer executable:

```bash
chmod +x install_cybernews_v3.sh
```

Run:

```bash
sudo ./install_cybernews_v3.sh
```

The installer will request:

```text
Administrator username
Administrator password
Let's Encrypt email
```

The installer configures:

```text
Apache
PHP
MariaDB
cron
Database schema
Admin interface
Feed polling
Feed auto-discovery
Logging
Log rotation
Security headers
Optional HTTPS
```

---

# Default Application Layout

The reference installation uses:

```text
/var/www/html/
```

Structure:

```text
/var/www/html/
├── index.php
├── cves.php
├── sources.php
├── about.php
├── feed.php
├── health.php
├── robots.txt
│
├── admin/
│   ├── index.php
│   ├── login.php
│   ├── logout.php
│   └── sources.php
│
├── api/
│   └── latest.php
│
├── assets/
│   ├── style.css
│   └── app.js
│
├── includes/
│   ├── bootstrap.php
│   ├── functions.php
│   ├── feed_engine.php
│   ├── header.php
│   └── footer.php
│
└── cron/
    ├── poll-feeds.php
    └── self-test.php
```

Configuration:

```text
/etc/cybernews/config.php
```

Poll logs:

```text
/var/log/cybernews/poller.log
```

Cron:

```text
/etc/cron.d/cybernews
```

Backups:

```text
/var/backups/cybernews/
```

---

# Internal Name vs Public Name

The public project name is:

```text
Cybersecurity Intel Free'd
```

The current application retains the legacy/internal technical name:

```text
CyberNews
cybernews
```

in some paths and identifiers.

Examples:

```text
/etc/cybernews/
/var/log/cybernews/
/etc/cron.d/cybernews
cybernews database
cybernews database user
cybernews_admin session
```

This is intentional for compatibility.

You do **not** need to rename those internal identifiers in order to rebrand the application.

---

# Source Management

Admin interface:

```text
https://YOUR-DOMAIN/admin/
```

Source management:

```text
https://YOUR-DOMAIN/admin/sources.php
```

Each source contains:

```text
Name
Website URL
Feed URL
Source Group
Polling Interval
Enabled State
HTTP State
Health Information
```

---

# Adding an RSS / Atom Feed

Example:

```text
Name:
Example Security Research

Website:
https://security.example.com/

Feed:
https://security.example.com/feed.xml

Group:
Independent Research

Polling Interval:
900
```

Click:

```text
ADD / AUTO-DISCOVER
```

The feed is validated before being added.

---

# Adding a Website Using Auto-Discovery

If you know the website but not the RSS feed:

```text
Name:
Example Security Site

Website:
https://security.example.com/

Feed:
LEAVE BLANK
```

Cybersecurity Intel Free'd will inspect the website for declarations such as:

```html
<link
    rel="alternate"
    type="application/rss+xml"
    href="/feed.xml">
```

or:

```html
<link
    rel="alternate"
    type="application/atom+xml"
    href="/atom.xml">
```

The discovery engine may also check common feed locations.

Candidate URLs are validated as RSS/Atom XML before being stored.

> Cybersecurity Intel Free'd does not currently scrape arbitrary website articles when no feed is available.

---

# Source Groups

Default groups include:

```text
Government
Vendor Research
Independent Research
Security Journalism
Community
Other
```

These help distinguish the nature of the information source.

---

# Source Controls

## EDIT

Edit:

* Name
* Website URL
* Feed URL
* Source group
* Polling interval

Saving resets relevant feed cache state.

---

## POLL

Immediately performs a fresh poll of the selected source.

Manual polling performs an unconditional request.

Use it when:

* Adding a source
* Testing a feed
* Troubleshooting
* Checking for new articles
* Verifying an edited URL

---

## RESET CACHE

Clears stored HTTP validator state.

This includes items such as:

```text
ETag
Last-Modified
last_polled
last_full_fetch
consecutive_304
error state
```

This is useful when a publisher or CDN appears to be returning stale cache responses.

---

## TOGGLE

Disables or enables polling without deleting the source.

Use this when:

* A feed is temporarily broken
* A publisher is unavailable
* You want to preserve historical articles
* You may re-enable the source later

---

## DELETE

Deletes the source.

> **Warning:** Articles associated with that source are also deleted because of the database's cascading relationships.

If you only want to stop polling:

```text
TOGGLE
```

instead.

---

# Poll Intervals

Poll intervals are stored in seconds.

| Seconds | Interval   |
| ------: | ---------- |
|   `300` | 5 minutes  |
|   `600` | 10 minutes |
|   `900` | 15 minutes |
|  `1800` | 30 minutes |
|  `3600` | 1 hour     |

The default minimum is:

```text
300 seconds
```

---

# Automatic Polling

Cron configuration:

```text
/etc/cron.d/cybernews
```

Default:

```cron
*/5 * * * * www-data /usr/bin/php /var/www/html/cron/poll-feeds.php >> /var/log/cybernews/poller.log 2>&1
```

Cron wakes every five minutes.

Each source is only downloaded when its own configured polling interval is due.

---

# HTTP 304 Handling

`304 Not Modified` is **not an error and not a redirect**.

It is a conditional-cache response.

Cybersecurity Intel Free'd treats these independently:

```text
200-299    Successful response
301        Redirect
302        Redirect
303        Redirect
304        Not Modified
307        Redirect
308        Redirect
```

The application stores:

```text
ETag
Last-Modified
last_full_fetch
consecutive_304
final_url
last_http_status
```

Scheduled polling may send:

```http
If-None-Match: ...
If-Modified-Since: ...
```

If the publisher returns:

```text
304 Not Modified
```

Cybersecurity Intel Free'd records a successful poll without attempting to parse an empty response.

---

# Protection Against Stale 304 Loops

Some CDNs or feed servers can incorrectly remain in a stale conditional-cache state.

Cybersecurity Intel Free'd automatically forces a complete request after approximately:

```text
6 hours without a full feed response
```

or:

```text
12 consecutive 304 responses
```

Manual `POLL` and:

```bash
--force
```

requests bypass conditional caching.

---

# Redirect Handling

Supported redirects:

```text
301
302
303
307
308
```

Redirects are validated manually.

For every redirect:

```text
Read Location
     │
     ▼
Resolve relative URL
     │
     ▼
Validate scheme/port
     │
     ▼
Resolve destination
     │
     ▼
Check SSRF restrictions
     │
     ▼
Connect
```

This prevents a public feed URL from blindly redirecting the application to an internal resource.

---

# Manual Polling

Poll feeds currently due:

```bash
sudo -u www-data php /var/www/html/cron/poll-feeds.php
```

Poll all enabled feeds:

```bash
sudo -u www-data php /var/www/html/cron/poll-feeds.php --all
```

Force all feeds to perform a full unconditional request:

```bash
sudo -u www-data php /var/www/html/cron/poll-feeds.php --all --force
```

Expected output resembles:

```text
The Hacker News HTTP=200 seen=50 new=3 updated=1 unchanged=46 invalid=0 newest=2026-08-15 13:00:00 OK
```

---

# Poller Output

| Field       | Meaning                                  |
| ----------- | ---------------------------------------- |
| `HTTP`      | Final HTTP status                        |
| `seen`      | Feed entries parsed                      |
| `new`       | New articles                             |
| `updated`   | Existing articles whose metadata changed |
| `unchanged` | Existing records with no changes         |
| `invalid`   | Feed entries missing usable fields       |
| `newest`    | Newest usable publication date           |

This makes it easier to identify whether a problem exists with:

```text
Publisher
HTTP cache
Feed parser
Database
Article normalization
Frontend
```

---

# Public Endpoints

Replace:

```text
YOUR-DOMAIN
```

with your hostname.

## Homepage

```text
https://YOUR-DOMAIN/
```

## High Priority

```text
https://YOUR-DOMAIN/?priority=1
```

## CVE Index

```text
https://YOUR-DOMAIN/cves.php
```

## Sources

```text
https://YOUR-DOMAIN/sources.php
```

## RSS

```text
https://YOUR-DOMAIN/feed.php
```

## High-Priority RSS

```text
https://YOUR-DOMAIN/feed.php?priority=1
```

## Category RSS

```text
https://YOUR-DOMAIN/feed.php?category=ransomware
```

## JSON API

```text
https://YOUR-DOMAIN/api/latest.php
```

## Health

```text
https://YOUR-DOMAIN/health.php
```

---

# Using Cybersecurity Intel Free'd as an RSS Source

The application consumes RSS but also publishes RSS.

Example:

```text
Security Vendors
Government Advisories
Security Journalism
Independent Researchers
        │
        ▼
Cybersecurity Intel Free'd
        │
        ├── Web UI
        ├── Main RSS
        ├── High Priority RSS
        ├── Category RSS
        └── JSON API
```

This makes Cybersecurity Intel Free'd useful as an aggregation layer for other systems.

---

# JSON API

Latest:

```text
https://YOUR-DOMAIN/api/latest.php
```

Limit:

```text
https://YOUR-DOMAIN/api/latest.php?limit=20
```

High priority:

```text
https://YOUR-DOMAIN/api/latest.php?priority=1
```

Potential integrations include:

```text
Microsoft Sentinel
Splunk
Elastic
OpenSearch
Open-WebUI
Home Assistant
Slack
Microsoft Teams
Discord
Python
PowerShell
SOAR
Custom dashboards
```

---

# Customizing the Branding

Cybersecurity Intel Free'd is designed to be forked and customized.

You can turn it into:

```text
ACME Security Intel
SOC Intelligence Feed
Blue Team Daily
Threat Research Dashboard
Security Operations News
Company Cyber Intelligence
```

---

## Important: Customize the Installer

The installer generates the PHP application files.

If you only edit:

```text
/var/www/html/
```

and later rerun the installer, your changes may be overwritten.

For a permanent fork:

1. Modify the installer templates.
2. Commit the changes.
3. Test the installer.
4. Deploy from the customized installer.

---

# Find Existing Branding

Run:

```bash
grep -nEi \
'news\.buf0rd\.com|buf0rd|CyberNews|CYBERSECURITY INTELLIGENCE FEED|Cybersecurity Intelligence Feed' \
install_cybernews_v3.sh
```

Review each match.

---

# Change the Domain

At the beginning of the installer:

```bash
DOMAIN="news.buf0rd.com"
```

Change it:

```bash
DOMAIN="intel.example.com"
```

Also search the installer for any literal reference-domain strings.

---

# Change the Site Name

Configuration:

```text
/etc/cybernews/config.php
```

Example:

```php
'site' => [
    'name' => "Cybersecurity Intel Free'd",
    'domain' => 'intel.example.com',
    'base_url' => 'https://intel.example.com',
    'timezone' => 'UTC',
],
```

---

# Change the Header

Installed file:

```text
/var/www/html/includes/header.php
```

Example:

```html
<div class="brand">
    <a href="/">CYBERSECURITY INTEL FREE'D</a>
    <small>YOUR ORGANIZATION</small>
</div>
```

For a permanent fork, change the matching installer template too.

---

# Change the Footer

Installed file:

```text
/var/www/html/includes/footer.php
```

Example:

```html
<footer>
    <span>intel.example.com</span>
    <span>Original reporting remains with the cited publisher.</span>
    <span>
        <a href="/feed.php">RSS</a> ·
        <a href="/api/latest.php">JSON API</a>
    </span>
</footer>
```

---

# Change the About Page

Installed file:

```text
/var/www/html/about.php
```

Customize:

* Project name
* Organization
* Domain
* Description
* User-Agent
* Contact information

---

# Change the Poller User-Agent

Example:

```php
'user_agent' => "Cybersecurity Intel Free'd/3.0 (+https://intel.example.com/about.php)",
```

Organizations may prefer:

```php
'user_agent' => 'ACME-Cyber-Intel/3.0 (+https://intel.example.com/about.php)',
```

Use a descriptive user-agent so publishers can identify legitimate polling traffic.

---

# Styling

Main stylesheet:

```text
/var/www/html/assets/style.css
```

The default interface uses CSS variables.

Example:

```css
:root {
    --bg: #070b0d;
    --panel: #0d1417;
    --panel2: #111b20;
    --fg: #d8e7df;
    --muted: #789087;
    --green: #7cff8a;
    --cyan: #59d7ff;
    --red: #ff6b6b;
    --border: #23332d;
}
```

---

## Blue SOC Theme

```css
:root {
    --bg: #05080d;
    --panel: #0a111c;
    --panel2: #101b2b;
    --fg: #dcecff;
    --muted: #7f96ae;
    --green: #5db8ff;
    --cyan: #00e5ff;
    --red: #ff6464;
    --border: #203650;
}
```

---

## Terminal Theme

```css
:root {
    --bg: #000000;
    --panel: #050505;
    --panel2: #090909;
    --fg: #d0ffd0;
    --muted: #669966;
    --green: #00ff41;
    --cyan: #00ffaa;
    --red: #ff4444;
    --border: #174d27;
}
```

---

# Security

Because Cybersecurity Intel Free'd downloads administrator-configured URLs, remote fetching represents a potential SSRF attack surface.

The feed client therefore applies restrictions.

---

## URL Restrictions

Remote retrieval is limited to:

```text
HTTP
HTTPS
TCP 80
TCP 443
Public IPv4 addresses
```

The client rejects:

* URL-embedded credentials
* unsupported protocols
* unsupported ports
* private IPv4 addresses
* reserved IPv4 addresses

Examples of blocked address ranges include:

```text
127.0.0.0/8
10.0.0.0/8
172.16.0.0/12
192.168.0.0/16
169.254.0.0/16
```

---

# SSRF Protection

A feed URL is validated before connection.

Redirect targets are validated again.

Conceptually:

```text
Requested URL
     │
     ▼
Parse URL
     │
     ▼
HTTP/HTTPS?
     │
     ▼
Port 80/443?
     │
     ▼
Resolve hostname
     │
     ▼
Public destination?
     │
     ▼
Pin connection
     │
     ▼
Request
```

---

# TLS

The feed client performs:

```text
TLS certificate verification
TLS hostname verification
```

Do not disable TLS verification simply to accommodate a poorly configured source.

---

# Other Security Controls

The application includes controls such as:

* PDO prepared statements
* CSRF protection
* Password hashing
* HttpOnly cookies
* SameSite cookies
* Session regeneration
* HTML escaping
* XML external network access disabled
* Admin no-cache behavior
* Admin noindex behavior
* Apache security headers
* `/includes` blocked from HTTP
* `/cron` blocked from HTTP
* Secrets outside the web root

---

# Deployment Recommendations

For public deployments:

* Keep Ubuntu patched.
* Keep Apache patched.
* Keep PHP patched.
* Keep MariaDB patched.
* Use HTTPS.
* Use a strong administrator password.
* Do not expose MariaDB publicly.
* Monitor feed errors.
* Review every source added.
* Back up the database.
* Consider restricting `/admin/` using firewall, VPN, reverse proxy, or additional authentication.
* Do not disable SSRF protection to accommodate a feed.

---

# Self Tests

Run:

```bash
sudo -u www-data php /var/www/html/cron/self-test.php
```

Live feed testing:

```bash
sudo -u www-data php /var/www/html/cron/self-test.php --live
```

Tests include checks for:

```text
Database connectivity
URL normalization
CVE extraction
Classification
Priority scoring
RSS parsing
Atom parsing
Publication date parsing
Future-date rejection
SSRF localhost rejection
Non-HTTP URL rejection
Required database columns
Latest ordering
```

---

# Logs

Poller:

```bash
sudo tail -f /var/log/cybernews/poller.log
```

Recent events:

```bash
sudo tail -100 /var/log/cybernews/poller.log
```

Errors:

```bash
sudo grep -i 'ERROR' /var/log/cybernews/poller.log
```

Cron:

```bash
sudo journalctl -u cron --since "30 minutes ago" --no-pager
```

Apache:

```bash
sudo tail -f /var/log/apache2/YOUR-DOMAIN-error.log
```

---

# Database Operations

List sources:

```bash
sudo mariadb cybernews -e "
SELECT
    id,
    name,
    enabled,
    feed_url,
    final_url,
    last_http_status,
    last_success,
    consecutive_304,
    error_count,
    last_error
FROM sources
ORDER BY name;
"
```

Disable source ID `3`:

```bash
sudo mariadb cybernews -e "
UPDATE sources
SET enabled=0
WHERE id=3;
"
```

Enable source ID `3`:

```bash
sudo mariadb cybernews -e "
UPDATE sources
SET enabled=1
WHERE id=3;
"
```

Reset HTTP state:

```bash
sudo mariadb cybernews -e "
UPDATE sources
SET
    etag=NULL,
    last_modified=NULL,
    last_polled=NULL,
    last_full_fetch=NULL,
    consecutive_304=0,
    error_count=0,
    last_error=NULL
WHERE id=3;
"
```

Delete source:

```bash
sudo mariadb cybernews -e "
DELETE FROM sources
WHERE id=3;
"
```

Remember:

> Deleting a source also deletes articles associated with that source.

---

# Verify Current Article Dates

```bash
sudo mariadb cybernews -e "
SELECT
    s.name AS source,
    a.title,
    a.published_at,
    a.discovered_at
FROM articles a
JOIN sources s
    ON s.id=a.source_id
WHERE a.active=1
ORDER BY
    COALESCE(a.published_at,a.discovered_at) DESC,
    a.discovered_at DESC
LIMIT 20;
"
```

Check maximum dates:

```bash
sudo mariadb cybernews -e "
SELECT
    MAX(published_at) AS newest_published,
    MAX(discovered_at) AS newest_indexed,
    MAX(COALESCE(published_at,discovered_at)) AS newest_effective
FROM articles;
"
```

---

# Backups

Database:

```bash
sudo mariadb-dump \
  --single-transaction \
  cybernews \
  > /root/cybernews-$(date +%Y%m%d-%H%M%S).sql
```

Webroot:

```bash
sudo tar -czf \
  /root/cybernews-web-$(date +%Y%m%d-%H%M%S).tar.gz \
  /var/www/html
```

Configuration:

```bash
sudo cp -a \
  /etc/cybernews \
  /root/cybernews-config-backup
```

---

# Upgrade / Repair

The v3 installer can detect an existing compatible installation.

Before replacing application code, it can create a backup beneath:

```text
/var/backups/cybernews/YYYYMMDD-HHMMSS/
```

Possible contents:

```text
webroot.tar.gz
config.php
cybernews.sql
```

During an upgrade, leaving the admin password blank preserves the existing password hash.

---

# Troubleshooting

## No new articles

Force a complete refresh:

```bash
sudo -u www-data php /var/www/html/cron/poll-feeds.php --all --force
```

Then inspect:

```bash
sudo tail -100 /var/log/cybernews/poller.log
```

---

## Feed stuck on 304

Use:

```text
Admin → Sources → RESET CACHE
```

or:

```bash
sudo mariadb cybernews -e "
UPDATE sources
SET
    etag=NULL,
    last_modified=NULL,
    last_polled=NULL,
    last_full_fetch=NULL,
    consecutive_304=0
WHERE id=3;
"
```

Then:

```bash
sudo -u www-data php /var/www/html/cron/poll-feeds.php --all --force
```

---

## Feed returns HTTP 403

Possible causes:

* Publisher blocks automated requests
* Bot/CDN protection
* Incorrect feed endpoint
* Feed was made private
* User-Agent policy

Do not attempt to circumvent publisher access controls.

Use another officially available feed or disable the source.

---

## Feed returns HTTP 404

The feed may have moved.

Edit the source or try website auto-discovery again.

---

## Website auto-discovery fails

The publisher may not expose a feed.

Look for:

```html
<link rel="alternate" type="application/rss+xml" href="...">
```

or:

```html
<link rel="alternate" type="application/atom+xml" href="...">
```

Cybersecurity Intel Free'd does not scrape arbitrary article HTML.

---

## Cron not running

Check:

```bash
sudo systemctl status cron --no-pager
```

Enable:

```bash
sudo systemctl enable --now cron
```

View executions:

```bash
sudo journalctl -u cron --since "30 minutes ago" --no-pager
```

---

## Apache configuration

```bash
sudo apache2ctl configtest
```

Expected:

```text
Syntax OK
```

---

## PHP Syntax

```bash
find /var/www/html -name '*.php' -print0 |
while IFS= read -r -d '' file; do
    php -l "$file" || exit 1
done
```

---

# Health Endpoint

```text
https://YOUR-DOMAIN/health.php
```

Example response:

```json
{
  "status": "ok",
  "time": "2026-08-15T20:00:00+00:00"
}
```

This can be used by:

* Uptime monitoring
* Reverse proxies
* Load balancers
* Monitoring systems

---

# Potential Uses

## Personal Cyber Intelligence Dashboard

Create a curated feed around your own technology stack.

Example:

```text
Microsoft
Linux
Cisco
Fortinet
Palo Alto
AWS
Azure
VMware
CISA
Mandiant
CrowdStrike
```

---

## SOC Dashboard

Provide analysts with a common feed of:

```text
Vulnerabilities
Active Exploitation
Ransomware
Threat Actors
Vendor Advisories
Security Research
```

---

## DFIR Research

Use the historical database to search for:

```text
CVE
malware
threat actor
campaign
vendor
exploit
incident
ransomware
```

---

## Threat Intelligence Foundation

Cybersecurity Intel Free'd can serve as the beginning of a lightweight CTI workflow.

Future enrichment could extract:

```text
IPs
Domains
URLs
Hashes
Malware Families
Threat Actors
Products
MITRE ATT&CK Techniques
```

---

## Security Lab Integration

Feed the platform into:

```text
SIEM
SOAR
Local LLMs
Dashboards
Scripts
Automation
Alerting tools
```

---

# Future Development

Possible roadmap:

* [ ] CISA KEV enrichment
* [ ] NVD CVSS enrichment
* [ ] FIRST EPSS enrichment
* [ ] MITRE ATT&CK mapping
* [ ] IOC extraction
* [ ] IP extraction
* [ ] Domain extraction
* [ ] URL extraction
* [ ] File hash extraction
* [ ] Malware family tagging
* [ ] Threat actor tagging
* [ ] Cross-source story clustering
* [ ] Duplicate-story correlation
* [ ] Local LLM summarization
* [ ] Local LLM classification
* [ ] User-defined priority scoring
* [ ] User-defined categories
* [ ] Email alerts
* [ ] Slack notifications
* [ ] Teams notifications
* [ ] Webhooks
* [ ] OPML import/export
* [ ] API authentication
* [ ] API keys
* [ ] Rate limiting
* [ ] Source reputation scoring
* [ ] Per-source retention
* [ ] Dark/light mode
* [ ] Docker installation option
* [ ] Domain prompt in installer
* [ ] Branding prompts
* [ ] Multiple admin accounts
* [ ] RBAC
* [ ] Saved searches
* [ ] Watchlists
* [ ] Prometheus metrics

---

# AI Enrichment

AI should remain optional rather than part of the critical ingestion path.

Recommended design:

```text
RSS / Atom
     │
     ▼
Normalize
     │
     ▼
Store
     │
     ▼
Optional Enrichment Queue
     │
     ▼
Local / Remote LLM
```

Possible enrichment output:

```json
{
  "summary": "Analyst-focused summary",
  "category": "Vulnerability",
  "severity": "high",
  "products": [
    "Example Product"
  ],
  "cves": [
    "CVE-2026-12345"
  ],
  "threat_actor": null
}
```

If AI is unavailable, feed ingestion should continue normally.

---

# Contributing

Contributions are welcome.

Useful areas include:

* Feed parsing
* RSS compatibility
* Atom compatibility
* HTTP handling
* Redirect handling
* Security hardening
* Classification rules
* Priority scoring
* Threat intelligence enrichment
* Database performance
* UI improvements
* API improvements
* Documentation
* Testing

Suggested workflow:

```bash
git checkout -b feature/my-improvement
```

Test installer syntax:

```bash
bash -n install_cybernews_v3.sh
```

Test installed PHP:

```bash
find /var/www/html -name '*.php' -print0 |
while IFS= read -r -d '' file; do
    php -l "$file" || exit 1
done
```

Run application tests:

```bash
sudo -u www-data php /var/www/html/cron/self-test.php
```

Live feed tests:

```bash
sudo -u www-data php /var/www/html/cron/self-test.php --live
```

Pull requests should document:

* What changed
* Why it changed
* How it was tested
* Database impact
* Security impact
* Compatibility impact

---

# Responsible Source Usage

Operators should:

* Respect publisher feed availability
* Use reasonable polling intervals
* Identify their User-Agent
* Use HTTP caching
* Link users back to original publishers
* Respect publisher access restrictions
* Avoid copying full articles without authorization
* Disable sources that prohibit automated access

Cybersecurity Intel Free'd is intended to be an **index and discovery platform**, not a republication engine.

---

# License

Choose the license appropriate for your fork.

Common options:

```text
MIT License
```

or:

```text
Apache License 2.0
```

Once selected, add:

```text
LICENSE
```

to the repository and update this README.

Example:

```markdown
## License

Licensed under the MIT License. See [LICENSE](LICENSE).
```

---

# Disclaimer

Cybersecurity Intel Free'd provides aggregation, indexing, classification, and prioritization of public third-party cybersecurity information.

It is not a replacement for:

* Authoritative vendor advisories
* Vulnerability management systems
* Threat intelligence validation
* Incident response judgment
* Patch management decisions
* Legal or compliance review

Automated categories and priority scores should be treated as analyst aids.

Always review original publisher information before making security decisions.

---

# Acknowledgements

Cybersecurity Intel Free'd exists because security researchers, defenders, journalists, vendors, government organizations, incident responders, and community members continue to publish useful information through open web standards.

This project indexes and organizes that information.

**Original reporting remains with the original publisher.**

---

# Quick Reference

### Admin

```text
https://YOUR-DOMAIN/admin/
```

### Manage Sources

```text
https://YOUR-DOMAIN/admin/sources.php
```

### Latest

```text
https://YOUR-DOMAIN/
```

### High Priority

```text
https://YOUR-DOMAIN/?priority=1
```

### CVEs

```text
https://YOUR-DOMAIN/cves.php
```

### RSS

```text
https://YOUR-DOMAIN/feed.php
```

### High-Priority RSS

```text
https://YOUR-DOMAIN/feed.php?priority=1
```

### JSON

```text
https://YOUR-DOMAIN/api/latest.php
```

### Force Poll

```bash
sudo -u www-data php /var/www/html/cron/poll-feeds.php --all --force
```

### Self-Test

```bash
sudo -u www-data php /var/www/html/cron/self-test.php
```

### Live Self-Test

```bash
sudo -u www-data php /var/www/html/cron/self-test.php --live
```

### Poll Log

```bash
sudo tail -f /var/log/cybernews/poller.log
```

### Database Backup

```bash
sudo mariadb-dump --single-transaction cybernews > cybernews.sql
```

---

<p align="center">
  <strong>🛡️ Cybersecurity Intel Free'd</strong>
</p>

<p align="center">
  <strong>Open feeds. Operator control. No unnecessary platform lock-in. by:buf0rd&friends </strong>
</p>
