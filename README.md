# diskstation-dashboard

A static, sanitized snapshot of a four-box DiskStation NAS fleet's storage health, published as a
GitHub Pages site. The page reports volumes, pools, rebuild and scrub progress, SMART status and
per-box findings. It is a read-only view: the snapshot is described as a "sanitized read-only API
snapshot" and the page footer states "Read-only NAS API probes. No writes to any box." The HTML is
rendered and committed by a publisher running outside this repository (see the comments in
`.github/workflows/pages.yml`); this repo holds the published output and the deploy workflow.

## How to run

There is no build or run script here — `site/index.html` is a single self-contained page (inline CSS,
no scripts), so it can be opened directly in a browser. Publication happens through GitHub Pages:
`.github/workflows/pages.yml` uploads the `site` directory and deploys it on every push to `main`,
and can also be run by hand with `workflow_dispatch`.

Refreshing the numbers needs the off-repo publisher that queries the boxes; it is not part of this
repository.

## Layout

- `site/` — the published site directory
- `site/index.html` — the dashboard page (self-contained, data embedded)
- `site/data.json` — machine-readable snapshot, schema `ds-public/1`
- `site/index.json` — per-volume task summary (render time, active tasks, ETAs)
- `.github/workflows/pages.yml` — Pages build and deploy workflow

## Not included

- No DSM credentials, hostnames, addresses or part numbers: the footer states identifiers are
  pseudonymous bay/drive ids, and the snapshot is sanitized.
- No collector or publisher source code — only its committed output is here.
- No historical snapshots: the repo tracks the current `site/` files, and each publisher commit
  replaces them in place.
