# agentic-platform-ui

A Next.js prototype of a B2B management UI for an agentic platform. **The prototype IS the spec.** Reviewers (engineers, PO, friendly users) consume it via screensharing, screenshots, or — once deployed — a clickable per-branch URL.

## Viewing the prototype

### Easiest

Go to [apui.operations.awsprod.gigantic.io](https://apui.operations.awsprod.gigantic.io/branch/main/) and use the credentials found in 1Password.

### Local

```sh
# Install dependencies
npm install

# Start server
npm run dev
```

Then open [http://localhost:3000](http://localhost:3000).

## Prototyping workflow

A typical iteration for adding elements to the prototype looks like this:

1. Designer creates a model spec in `.grill/spec/model-*.md`, defining an entity the application deals with.
2. Designer initiates `/grill-me` session about the added spec file. Results will be logged.
3. Designer asks which views/pages are implied by the outcome, to be added to `.grill/spec/routes.md`.
4. Designer prompts to create new view(s), agent executes.
5. Designer previews and prompts corrections.

  - Consistency with existing views plays a particular role here. The designer should point out any aspects that require alignment across views.

6. While the context window still permits (e. g. 20% or more left before compaction), designer prompts `/improve-codebase`.

Design notes and rejected alternatives live under `.grill/`.

## Worktrees

Little cheat sheet for working on several things in parallel.

Create a new worktree and claude session:

```
export FEATURE=my-new-feature
git worktree add ../agentic-platform-ui-${FEATURE} -b ${FEATURE}
cd ../agentic-platform-ui-${FEATURE}
npm ci
npm run dev -- -p 3001 # some port that is unique to this worktree
```

Tear down worktree:

```
# From the main repo clone
export FEATURE=my-new-feature
git worktree remove ../agentic-platform-ui-${FEATURE}
git branch -d ${FEATURE} # if not auto-deleted by the merge
```

## Stack

- Next.js 16 (App Router) + shadcn/ui (base-nova, neutral) + Tailwind v4 + Base UI primitives + lucide-react.
- Stock shadcn defaults — no custom theming.

See `AGENTS.md` and `.claude/CLAUDE.md` for the working conventions agents follow when extending the prototype.

