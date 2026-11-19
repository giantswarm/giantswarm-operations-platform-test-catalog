# Redirect service for what used to be our website

This chart redirects requests to `https://giantswarm.io/` to new locations, mainly `https://www.giantswarm.io/`. It renders a single Gateway API `HTTPRoute` whose rules answer with redirects, so Envoy Gateway serves them without a backend.

The redirects are listed in [`values.yaml`](helm/giantswarmio-nginx-app/values.yaml).
