# ZIO Renovate Config

This repository contains a shared Renovate configuration for ZIO ecosystem projects. It is intended to be used by projects that are part of the ZIO ecosystem.

By using this shared configuration, projects will automatically receive updates to their dependencies as new versions of their dependencies are released.

This will help ensure that projects are always using the latest versions of their dependencies, and not using any dependencies that have been deprecated or are no longer maintained.

For more information about Renovate, see the [Renovate documentation](https://docs.renovatebot.com/).

## Noisiness

We tried to make Renovate less noisy by enabling "automerge" for all patch and minor updates. We also changed the automerge type to "branch", which means that Renovate will automatically create a branch (instead of creating a PR) and wait for the CI to pass. If the CI passes, the branch will be merged into the default branch. If the CI fails, Renovate will create a PR for the branch and wait for manual intervention.

## Usage

To use this shared configuration, add the following line to your `renovate.json`:

```json
{
  "extends": ["github>zio/zio-renovate-config:renovate"]
}
```

To make sure that the CI is always run when a new branch is created, you need to enable "create" events in your Github workflow, e.g. `.github/workflows/ci.yml`:

```diff
 'on':
   workflow_dispatch: {}
   release:
     types:
     - published
   push:
     branches:
     - main 
   pull_request: {}
+  create: {}
```

