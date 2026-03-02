# Dangerzone Security Dashboard

A nightly vulnerability scanner for the [Dangerzone](https://github.com/freedomofpress/dangerzone) container image, published to GitHub Pages.

Each night, a GitHub Actions workflow:

1. Installs [grype](https://github.com/anchore/grype) – an open-source vulnerability scanner.
2. Scans the latest and nightly `ghcr.io/freedomofpress/dangerzone/v1` container image.
3. Applies the same CVE ignore/filter list maintained by upstream DZ (see [`.grype.yaml`](.grype.yaml)).
4. Renders the results using a HTML template (see [`templates/html.tmpl`](templates/html.tmpl)).
5. Publishes the reports to GitHub Pages.

## Running locally

```bash
grype ghcr.io/freedomofpress/dangerzone/v1:latest \
  --config .grype.yaml \
  --output template \
  --template templates/html.tmpl \
  --file report.html
```
