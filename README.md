# Dangerzone Security Dashboard

A nightly vulnerability scanner for the [Dangerzone](https://github.com/freedomofpress/dangerzone) container image, published to GitHub Pages.

## What it does

Each night, a GitHub Actions workflow:

1. Installs [grype](https://github.com/anchore/grype) – an open-source vulnerability scanner.
2. Scans the latest `ghcr.io/freedomofpress/dangerzone/v1` container image.
3. Applies the same CVE ignore/filter list maintained by the Dangerzone team (see [`.grype.yaml`](.grype.yaml)).
4. Renders the results using a hacker-themed HTML template (see [`templates/html.tmpl`](templates/html.tmpl)) for both stable and nightly scans.
5. Publishes the reports to GitHub Pages as `index.html` (stable) and `nightly.html` (latest untagged nightly).

## Files

| File | Description |
|---|---|
| `.grype.yaml` | Grype configuration: CVE ignore list mirrored from upstream Dangerzone |
| `templates/html.tmpl` | Custom hacker-themed HTML report template (based on grype's official template) |
| `.github/workflows/nightly.yml` | GitHub Actions workflow – runs nightly and deploys to GitHub Pages |

## Running locally

```bash
# Install grype
curl -sSfL https://raw.githubusercontent.com/anchore/grype/main/install.sh | sh -s -- -b /usr/local/bin

# Scan the Dangerzone image with the custom template
grype ghcr.io/freedomofpress/dangerzone/v1:latest \
  --config .grype.yaml \
  --output template \
  --template templates/html.tmpl \
  --file report.html

# Open the report
open report.html
```
