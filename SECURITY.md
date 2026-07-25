# Security Policy

## Reporting a vulnerability

**Do not open a public issue.** These are mail servers — a public report is an exploit notice for
every running instance.

Report privately, either way:

1. **GitHub private vulnerability reporting** — go to the affected repository, open the **Security**
   tab, and click **Report a vulnerability**. This is preferred.
2. **Email** — [mailorahq@gmail.com](mailto:mailorahq@gmail.com), subject line starting
   `SECURITY:`.

Useful things to include: the affected project and version, what an attacker gets, and the smallest
reproduction you can manage.

## What happens next

You will get an acknowledgement within **72 hours** and an assessment within **7 days**. Fixes ship
as soon as they are ready; you will be told when a patched release is out. Credit in the release
notes if you want it — say so, and say what name to use.

Please give a reasonable window to ship a fix before disclosing publicly.

## Supported versions

All projects are pre-1.0. Only the latest release of each gets security fixes. Upgrade before
reporting against an older tag.

## Scope

In scope: anything in these repositories — SMTP, IMAP and POP3 handling, MIME parsing,
authentication and session handling, API key and token verification, DKIM signing and verification,
the embedded web UI, and the published container images.

Out of scope: findings that depend on a deliberately insecure configuration documented as such
(open relays, `-relay-insecure`, self-signed development certificates, `SKIP_DNS_VERIFY`), missing
hardening headers with no demonstrated impact, and automated scanner output with no working
reproduction.
