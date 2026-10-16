# podcast-generator

Generate podcast feeds from a YAML file using a GitHub Action.

This repository contains a small action that reads a YAML feed description and emits an RSS/Atom podcast feed (and optional episode files). The Marketplace listing shows this README, so please edit the examples and wording below to match how you want it presented.

## Features
- Create podcast RSS feeds from a declarative YAML file
- Runs in Docker (self-contained)
- Inputs: committer name and email (used for commits if the action writes files)

## Inputs
- `email` (required) — The committer's email address. Default: `${{ github.actor }}@localhost`
- `name` (required) — The committer's name. Default: `${{ github.actor }}`

These inputs are declared in `action.yml`.

## Example usage
Create a workflow in .github/workflows/generate-feed.yml that runs this action and points it at your feed YAML file:

```yaml
name: Generate podcast feed
on:
  push:
    paths:
      - 'feed.yml'

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - name: Generate feed
        uses: aliefe9/podcast-generator@main
        with:
          name: 'GitHub Actions'
          email: 'actions@example.com'
```

Replace `feed.yml` and the input values with your real content. If your action writes the feed back to the repo you may need to set up an SSH deploy key or a PAT — the action currently uses the committer name/email inputs for commits.

## Files of interest
- `action.yml` — Action metadata (name, description, inputs)
- `Dockerfile` — Container image used by the action
- `README.md` — This file (displayed on the Marketplace listing)

## License
MIT — see the LICENSE file.
