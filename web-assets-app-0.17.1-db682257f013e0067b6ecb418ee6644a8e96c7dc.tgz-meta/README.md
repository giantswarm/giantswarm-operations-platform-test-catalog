# web-assets

Global static files used in several Giant Swarm web sites/applications

This repository is **private** as we want to prevent the public from being able to browse its entire content, for this reasons:
Since all this content is served statically without any rate limiting, we don't want anyone to use our server as a free CDN.

## Purpose

* To facilitate re-use of assets like JavaScript, CSS, Images
* Have a distinct place for assets which are used in several applications (and thus prevent the search for the right repository)
* Serve assets through it's own host name, to allow for faster download times


## Contents

### `assets`

The content of this folder (and only this folder) is published to the web under `https://s.giantswarm.io/`.

So, for example, the file `assets/jquery/3.3.1/1/jquery.min.js` is published
as `https://s.giantswarm.io/jquery/3.3.1/1/jquery.min.js`.

### `src`

This folder contains sources and scripts to generate certain assets, like JavaScript or CSS files which require a build process.

See the sub folders for details. There should be READMEs and Makefiles.

Note that not all assets have a src folder and a build process. For example, `assets/app-icons` has no according `src` folder.

#### highlightjs

Syntax highlighting we use especially in docs and blogs, from https://highlightjs.org/.

#### privacy

Script by Giant Swarm to handle user's data protection preferences throughout our sites.

#### auth0-logo

Logo files to use in Auth0 pages

## Deployment

After you've created a release, the version will be automatically updated in `workload-clusters-fleet` and deployed.
