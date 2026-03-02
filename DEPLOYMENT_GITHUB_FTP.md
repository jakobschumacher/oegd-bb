## GitHub SFTP Deploy Setup

This repository deploys automatically from GitHub Actions via `.github/workflows/publish.yml` using SFTP.

### 1) Store credentials in GitHub (important)

Use GitHub `Environment Secrets` in the `production` environment.

Path in GitHub:

`Settings -> Environments -> production -> Environment secrets`

Create these secrets:

- `FTP_HOST` (for example `ftp.example.com`)
- `FTP_PORT` (usually `22` for SFTP)
- `FTP_USERNAME`
- `FTP_PASSWORD`
- `FTP_REMOTE_DIR` (for example `/public_html/`)

Do not store credentials in source files, `.env` files, or commits.

### 2) Protect production deploys

In the same `production` environment:

- Set `Required reviewers` for manual release approval.
- Optionally add a wait timer.

This ensures a push to `main` does not deploy without approval.

### 3) How deployment runs

On `push` to `main` (or manual `workflow_dispatch`):

1. Build job renders the Quarto site (`quarto render`).
2. Deploy job uploads the built `_site/` output to your FTP target directory.

### 4) First run checklist

- Confirm all environment secrets are set.
- Run workflow manually once (`Actions -> Build and Deploy via FTP -> Run workflow`).
- Check uploaded files on server.
