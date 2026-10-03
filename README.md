# jdx/mise with Once

This is the default branch of tuist/mise. It only holds the experiment; `main` is
an unmodified mirror of [jdx/mise](https://github.com/jdx/mise).

- `.github/workflows/sync.yml` runs every four hours: it fast-forwards `main`
  from jdx/mise and builds and tests the latest upstream commit with Once. The
  fast-forward needs a `SYNC_TOKEN` secret (Contents and Workflows write) because
  `GITHUB_TOKEN` cannot push upstream workflow file changes.
- `.github/workflows/once.yml` checks out a jdx/mise commit, adds
  `overlay/once.toml`, and runs `once build` and `once test` on the same
  GitHub-hosted runners jdx/mise uses for Renovate PRs. The shared cache and run
  reporting go to the [tuist/mise](https://tuist.dev/tuist/mise) Tuist project.
  Run it manually with a `ref` to replay any upstream commit, and with
  `remote_cache: false` for a cold baseline.

- `.github/workflows/replay.yml` takes a jdx/mise commit, builds and tests its
  parent and then the commit in one workspace with only Once's local cache, and
  reports what the change invalidated. Use it on Renovate bumps.

Upstream workflows are disabled in this fork so nothing from jdx/mise's release or
deploy automation runs here.
