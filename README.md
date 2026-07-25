# gh-workflows

Reusable GitHub Actions workflows for Jordan's portfolio repos. Public so it can be
called cross-account (`jordanlawson1988` and `jordanlawsoncfa`).

## Workflows

### `node-ci.yml`

Reusable Node.js CI: `npm ci` → optional `tsc --noEmit` → optional `npm run build`
(with `SKIP_ENV_VALIDATION=1`) → `npm test --if-present`.

```yaml
name: CI
on:
  pull_request:
  push: {branches: [main, master, develop]}
jobs:
  ci:
    uses: jordanlawson1988/gh-workflows/.github/workflows/node-ci.yml@main
    with:
      node-version: '22'
      run-typecheck: true
      run-build: true
```

Inputs:

| Input            | Type    | Default | Notes                                  |
|-------------------|---------|---------|-----------------------------------------|
| `node-version`     | string  | `'22'`  | Node version for `actions/setup-node`   |
| `run-typecheck`    | boolean | `true`  | Set `false` for repos with no `tsconfig.json` |
| `run-build`        | boolean | `true`  | Set `false` for repos with no build script |
| `working-directory` | string | `'.'`   | Set when the Node app lives in a subdirectory (e.g. `web`) |
