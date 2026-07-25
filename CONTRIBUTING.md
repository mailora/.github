# Contributing

These notes apply to every repository in the Mailora org — Send, Trap, Temp and Mail. They are all
built the same way.

## Before you start

Open an issue first for anything larger than a bug fix. A short description of the problem beats a
large unexpected pull request, and it saves you writing code that gets turned down on shape rather
than quality.

## Setting up

You need **Go 1.26**, **Node 22** and **pnpm**.

```sh
make dev     # run the server locally
make test    # go test ./... plus a frontend typecheck
make build   # build web/dist, embed it, produce the binary
```

The frontend lives in `web/` and is built by Vite, then embedded into the binary via `go:embed`.
For frontend work run the Vite dev server alongside `make dev`:

```sh
cd web && pnpm install && pnpm run dev
```

## What has to be green

Before anything lands:

```sh
go build ./... && go vet ./... && go test ./...
```

And in `web/`:

```sh
pnpm run build     # runs tsc --noEmit before the Vite build; it must typecheck clean
```

If any of those fail, the change is not ready. There is no separate lint step to remember.

## Tests

Non-trivial logic gets **one runnable check** — the smallest test that fails if the logic breaks.
Not a suite, not a fixture harness, not a test per function.

- stdlib `testing` only. No test frameworks, no mocking libraries.
- In-package, table-driven or scenario style, `got`/`want` phrasing.
- Prefer the real thing over a mock: real SQLite in `t.TempDir()`, a real `httptest` server over the
  real handler, a real SMTP listener on `:0`.

Trivial one-liners do not need a test.

## Code

- `CGO_ENABLED=0` throughout. Nothing may pull in cgo — that includes the SQLite driver.
- Standard library first. `http.ServeMux` with method+pattern routes; no web framework, no router
  library, no DI container.
- One package owns the database. Nothing else touches it.
- Comments explain **why**, not what. A `// ponytail:` comment marks a deliberate simplification and
  names its ceiling and its upgrade path.
- Logging is `log/slog` with a `TextHandler`.
- Frontend state is TanStack Query. No Redux, no context store.
- New dependencies are a last resort. Say why in the pull request.

## Commit messages

**Prose imperative.** Write the sentence that completes "this commit will…":

```
Add the release workflow
Fix the retention janitor purging scheduled mail
Stop parsing MIME at ingest
```

Not conventional commits. No `feat:`, no `fix:`, no `chore(deps):`, no scopes, no emoji. Capital
first letter, no trailing full stop, body in plain prose if the subject needs backing up — explain
why the change was needed, not what the diff already says.

## Pull requests

Keep them small and on one subject. Fill in the template: what changed, why, and how you checked it.
Say plainly if something is untested or a known corner is cut.

## Licence

Contributions are MIT, same as the projects.
