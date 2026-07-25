## What this changes

<!-- One or two sentences. -->

## Why

<!-- The problem it solves. Link the issue if there is one: Fixes #123 -->

## How it was checked

<!-- The command you ran and what you saw. If a corner is cut or a case is untested, say so here. -->

## Checklist

- [ ] `go build ./... && go vet ./... && go test ./...` is green
- [ ] `pnpm run build` in `web/` is clean, if the frontend changed
- [ ] Non-trivial logic has one runnable check
- [ ] Commit messages are prose imperative ("Add the release workflow"), not conventional commits
- [ ] Docs and `.env.example` updated, if behaviour or configuration changed
