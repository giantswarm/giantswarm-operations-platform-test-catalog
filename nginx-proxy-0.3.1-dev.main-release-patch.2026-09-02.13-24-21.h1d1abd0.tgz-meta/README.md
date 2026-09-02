[![CircleCI](https://dl.circleci.com/status-badge/img/gh/giantswarm/nginx-proxy/tree/master.svg?style=svg&circle-token=6accf13c448bb39347ac47a2cf70e888fb4a9838)](https://dl.circleci.com/status-badge/redirect/gh/giantswarm/nginx-proxy/tree/master)

# nginx-proxy chart

This repository contains a helm chart containing Kubernetes resources to enable proxying HTTP requests between
the atlas operations cluster (`gorilla/zj88t`) `grafana-cloud.operations.giantswarm.io` and `prometheus-us-central1.grafana.net`.

**What is this app?**

This app is a configuration for Ingress NGINX Controller.

**Why did we add it?**

We added it because we need an HTTP proxy to bypass the GFW to be able to send data from chinese installation to Grafana cloud.

**Who can use it?**

Giantswarm staff can use it.

## Installing

There are 3 ways to install this app onto a workload cluster.

1. [Using our web interface](https://docs.giantswarm.io/ui-api/web/app-platform/#installing-an-app)
2. [Using our API](https://docs.giantswarm.io/api/#operation/createClusterAppV5)
3. Directly creating the [App custom resource](https://docs.giantswarm.io/ui-api/management-api/crd/apps.application.giantswarm.io/) on the management cluster.

### Sample App CR and ConfigMap for the management cluster
If you have access to the Kubernetes API on the management cluster, you could create
the App CR and ConfigMap directly.

Here is an example that would install the app to
workload cluster `abc12`:

```
# appCR.yaml

```

See our [full reference page on how to configure applications](https://docs.giantswarm.io/app-platform/app-configuration/) for more details.

## Compatibility

This app has been tested to work with the following workload cluster release versions:

* 14.1.1

## Limitations

Some apps have restrictions on how they can be deployed.
Not following these limitations will most likely result in a broken deployment.

* This app requires ingress-nginx and cert-manager.
