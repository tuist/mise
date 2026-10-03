# jdx/mise with Once

This is the default branch of tuist/mise. It only holds the experiment; `main` is
an unmodified mirror of [jdx/mise](https://github.com/jdx/mise).

- `.github/workflows/sync.yml` fast-forwards `main` from jdx/mise every hour and,
  when it moved, builds and tests the new commit with Once.
- `.github/workflows/once.yml` checks out a jdx/mise commit, adds
  `overlay/once.toml`, and runs `once build` and `once test` on the same
  GitHub-hosted runners jdx/mise uses for Renovate PRs. The shared cache and run
  reporting go to the [tuist/mise](https://tuist.dev/tuist/mise) Tuist project.
  Run it manually with a `ref` to replay any upstream commit, and with
  `remote_cache: false` for a cold baseline.

Upstream workflows are disabled in this fork so nothing from jdx/mise's release or
deploy automation runs here.
