<picture>
  <source media="(prefers-color-scheme: dark)" srcset="logo-dark.png" />
  <img src="logo-light.png" alt="Mailora" width="96" />
</picture>

# Mailora

Four self-hosted email tools. Each one is a single Go binary with the UI embedded in it — no runtime, no services to wire up, no SaaS account.

| | What it does | Docs | Repo | Run it |
|---|---|---|---|---|
| **Mailora Send** | Email sending platform — Resend-style `/v1` API, templates, audiences, broadcasts, DKIM, webhooks, SMTP relay on `:587` | [send.mailora.app](https://send.mailora.app) | [mailora/send](https://github.com/mailora/send) | `docker run ghcr.io/mailora/send` |
| **Mailora Trap** | Development mail catcher — captures everything your app sends, delivers nothing. SMTP, POP3, IMAP, live SSE web UI | [trap.mailora.app](https://trap.mailora.app) | [mailora/trap](https://github.com/mailora/trap) | `docker run -p 1025:1025 -p 8025:8025 ghcr.io/mailora/trap` |
| **Mailora Temp** | Disposable email — TTL-scoped inboxes, live push, DKIM-signed replies, multi-domain, scoped REST API | [temp.mailora.app](https://temp.mailora.app) | [mailora/temp](https://github.com/mailora/temp) | `docker run ghcr.io/mailora/temp` |
| **Mailora Mail** | Full mail server — inbound SMTP, IMAP, submission on `:587`, outbound queue with DKIM, automatic TLS, webmail | [mail.mailora.app](https://mail.mailora.app) | [mailora/mail](https://github.com/mailora/mail) | `docker run ghcr.io/mailora/mail` |

## What they have in common

- **One static binary.** `CGO_ENABLED=0`, the React UI compiled in via `go:embed`. Copy it to a box and run it.
- **SQLite by default.** Pure-Go driver, no cgo. Send and Temp will also talk to Postgres if you want that.
- **No SaaS.** No hosted control plane, no phone-home, no seat pricing. Your mail stays on your machine.
- **MIT licensed.**
- **Multi-arch images.** `linux/arm64` and `linux/amd64`, distroless, on `ghcr.io/mailora/<name>`.
- **Same shape throughout.** Go 1.26, stdlib `http.ServeMux`, React 19 + MUI 9 + TanStack Query.

---

Built by [Sumanta](https://sumanta.ai).
