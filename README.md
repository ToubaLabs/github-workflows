# github-workflows

## Cloudflare deployment workflow

This repository exposes a reusable GitHub Actions workflow at `.github/workflows/cloudflare-deploy.yml`.

It is intended to be called from another repository through `workflow_call` and expects the caller to provide a repository secret named `CLOUDFLARE_API_TOKEN`.

### Required secret

The consuming repository must define the following secret in GitHub:

- `CLOUDFLARE_API_TOKEN`

### Reusable workflow behavior

When called, the workflow:

- uses Node.js `24.22.0`
- runs `npm ci`
- executes `npm run deploy:vinext`
- passes the token as an environment variable named `CLOUDFLARE_API_TOKEN`

### Example caller

```yaml
jobs:
  deploy:
    uses: ToubaLabs/github-workflows/.github/workflows/cloudflare-deploy.yml@main
    secrets:
      CLOUDFLARE_API_TOKEN: ${{ secrets.CLOUDFLARE_API_TOKEN }}
```

This repository does not store the Cloudflare token itself; the secret remains in the calling repository's GitHub Actions secrets configuration.
