# Redirect service for the Giant Swarm blog

This repository contains a web server that only redirects all requests to `http(s)://www.giantswarm.io/blog/*`.

## Where is our blog content?

It is maintained in [HubSpot](https://app.hubspot.com/website/430224/blog/posts).

## Deployment

Releases of this app are pushed to the [giantswarm-operations-platform-catalog](https://github.com/giantswarm/giantswarm-operations-platform-catalog)
and deployed via [workload-clusters-fleet](https://github.com/giantswarm/workload-clusters-fleet/tree/main/management-clusters/gollum/organizations/giantswarm/workload-clusters/c68pn/mapi/apps/blog).
