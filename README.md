# github-workflows

## Cloudflare deployment workflow

This repository exposes a reusable GitHub Actions workflow at `.github/workflows/cloudflare-deploy.yml`.

It is intended to be called from another repository through `workflow_call` and expects the caller to provide the repository secrets named `CLOUDFLARE_API_TOKEN` and `CLOUDFLARE_ACCOUNT_ID`.

### Required secrets

The consuming repository must define the following secrets in GitHub:

- `CLOUDFLARE_API_TOKEN`
- `CLOUDFLARE_ACCOUNT_ID`

### Reusable workflow behavior

When called, the workflow:

- uses Node.js `24.22.0`
- runs `npm ci`
- executes `npm run deploy:vinext`
- passes the token and account ID as environment variables named `CLOUDFLARE_API_TOKEN` and `CLOUDFLARE_ACCOUNT_ID`

### Example caller

```yaml
jobs:
  deploy:
    uses: ToubaLabs/github-workflows/.github/workflows/cloudflare-deploy.yml@main
    secrets:
      CLOUDFLARE_API_TOKEN: ${{ secrets.CLOUDFLARE_API_TOKEN }}
      CLOUDFLARE_ACCOUNT_ID: ${{ secrets.CLOUDFLARE_ACCOUNT_ID }}
```

This repository does not store the Cloudflare values itself; the secrets remain in the calling repository's GitHub Actions secrets configuration.
