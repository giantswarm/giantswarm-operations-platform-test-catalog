[![CircleCI](https://circleci.com/gh/giantswarm/schema-server.svg?style=shield)](https://circleci.com/gh/giantswarm/schema-server)

# Schema server

This is an HTTP server for JSON schema. At Giant Swarm we use it to serve schema from https://github.com/giantswarm/schema under our own domain and with slightly different URLs. So this server is basically a proxy for https://raw.githubusercontent.com/giantswarm/schema.

This is all wrapped as a Giant Swarm app, to be deployed in a workload cluster using the app platform.
