# Node.js install GitHub Action

This repository provides a reusable GitHub Action for installing the dependencies of a JavaScript project that uses Node.js.

## Usage

To use the action, add it to a workflow in your repository:

```yml
name: Build Node.js project

on:
  workflow_dispatch:
  pull_request:
  push:
    branches:
      - main

jobs:
  build-nodejs:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout repository
        uses: actions/checkout@v5

      - name: Install dependencies
        uses: minvws/action-nodejs-install@v1
        with:
          readonly-token: ${{ secrets.READONLY_TOKEN }}
          audit-level: <audit-level>
          node-version: '20.x'
          run-npm-audit: 'true'
```

Replace `<audit-level>` with the audit-level you want to use. For example `info|low|moderate|high|critical|none`.

In this basic example, the workflow is executed automatically on push to the `main` branch and on any pull request.
And thanks to the `workflow_dispatch` trigger it can also be executed manually from the repository's Actions tab.

### Configuration

The action has the following inputs:

- `registry-url` (optional): Registry URL to setup up for auth. Passed on to actions/setup-node. Default is empty.
- `audit-level` (optional): The npm audit level. Options: `info|low|moderate|high|critical|none`. Default is high.
- `node-version` (optional): Version Spec of the version to use. Examples: 12.x, 10.15.1, >=10.15.0.
- `node-version-file` (optional): File containing the version Spec of the version to use. Examples: package.json, .nvmrc, .node-version, .tool-versions.
- `readonly-token` (optional): Add a read-only Token for the GitHub Package Registry which will be used for fetching node and npm packages.
- `run-npm-audit` (optional): Run npm audit script. Options: true|false. Default is false.

Note: If `node-version` and `node-version-file` both are provided the action will use the version from `node-version`.

## Contributing

If you want to contribute a new pipeline, please check the reusable workflow guidelines in the
[GitHub documentation](https://docs.github.com/en/actions/using-workflows/reusing-workflows#creating-a-reusable-workflow).

## License

This repository is released under the EUPL 1.2 license. See [LICENSE](./LICENSE) for details.

## Part of iCore

This package is part of the iCore project.
