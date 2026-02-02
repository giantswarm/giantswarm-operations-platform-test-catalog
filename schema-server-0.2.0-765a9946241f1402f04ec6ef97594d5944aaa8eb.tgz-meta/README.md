[![CircleCI](https://dl.circleci.com/status-badge/img/gh/giantswarm/schema-server/tree/main.svg?style=svg)](https://dl.circleci.com/status-badge/redirect/gh/giantswarm/schema-server/tree/main)

# Schema server

This is an HTTP server for JSON schema. At Giant Swarm we use it to serve schema from https://github.com/giantswarm/schema under our own domain and with slightly different URLs. So this server is basically a proxy for https://raw.githubusercontent.com/giantswarm/schema.

This is all wrapped as a Giant Swarm app, to be deployed in a workload cluster using the app platform.

## Details

The proxy is configured to serve URLs in the form of

    https://schema.giantswarm.io/NAME/VERSION

from the source

    https://giantswarm.github.io/schema/main/NAME/VERSION.json

This serves mainly three purposes:

1. Apply content type `application/schema+json`
2. Use our own domain
3. Remove the file name suffix `.json` from URLs
