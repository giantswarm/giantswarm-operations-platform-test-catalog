[![CircleCI](https://dl.circleci.com/status-badge/img/gh/giantswarm/agentic-platform-ui/tree/main.svg?style=svg)](https://dl.circleci.com/status-badge/redirect/gh/giantswarm/agentic-platform-ui/tree/main)

# agentic-platform-ui

A Next.js prototype of a B2B management UI for an agentic platform — users create agent groups, give them tasks, survey progress and results, and let agents self-improve. **The prototype IS the spec.** Reviewers (engineers, PO, friendly users) consume it via screensharing, screenshots, or — once deployed — a clickable per-branch URL.

## Stack

- Next.js 16 (App Router) + shadcn/ui (base-nova, neutral) + Tailwind v4 + Base UI primitives + lucide-react.
- Stock shadcn defaults — no custom theming.

See `AGENTS.md` and `.claude/CLAUDE.md` for the working conventions agents follow when extending the prototype.

## Local development

```sh
npm install
npm run dev
# open http://localhost:3000
```

## Per-branch deployment

Every push to a branch produces a container image tagged `<semver>-<sha>` and pushed to `gsociprivate.azurecr.io/giantswarm/agentic-platform-ui`. The image is a static `nginx-unprivileged` serving the Next.js export with `basePath=/branch/<slug>` baked in at build time.

A GitHub workflow opens PRs against [`giantswarm/workload-clusters-fleet`](https://github.com/giantswarm/workload-clusters-fleet) on the first push to a branch (to register the slug) and on PR close (to remove it). Subsequent image bumps are picked up by Flux Image Update Automation in the fleet repo — no CI write.

Each deployed branch is reachable at `https://<host>/branch/<slug>/` in the `operations` workload cluster on installation `gazelle`.

Design notes and rejected alternatives live under `.grill/`.

## Helm chart

The chart in `helm/agentic-platform-ui/` is consumed by the fleet repo. Only two values are accepted: `slug` (the branch identifier) and `imageTag` (`<semver>-<sha>`). Both are validated at render time against strict regexes; the registry and image repo are hardcoded so a compromised pipeline cannot redirect to an arbitrary image.

## Compatibility

This is a prototyping artifact for the `operations` workload cluster on installation `gazelle`. It is not intended to be installed as a generally available Giant Swarm App.
