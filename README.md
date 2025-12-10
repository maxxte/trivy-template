# Docker Security Scan Template

A GitHub template repository with automated security scanning using Trivy.

## What It Does

- Builds your Docker image on every push/PR
- Scans the image for vulnerabilities using [Trivy](https://github.com/aquasecurity/trivy)
- Reports findings to GitHub's Security tab (Code Scanning alerts)
- Runs weekly scheduled scans to catch newly discovered CVEs

## Using This Template

1. Click "Use this template" on GitHub
2. Replace the `Dockerfile` with your application
3. Push to `main` or open a PR

## Viewing Security Findings

After the workflow runs, view results at:

**Repository > Security > Code scanning alerts**

Findings appear alongside Dependabot alerts for a unified security view.

## Customization

### Fail on vulnerabilities

To block PRs when vulnerabilities are found, add `exit-code: '1'` and `severity`:

```yaml
- name: Run Trivy vulnerability scanner
  uses: aquasecurity/trivy-action@0.33.1
  with:
    image-ref: 'app:${{ github.sha }}'
    format: 'sarif'
    output: 'trivy-results.sarif'
    exit-code: '1'
    severity: 'CRITICAL,HIGH'
```

### Ignore specific CVEs

Create `.trivyignore` in the repo root:

```
CVE-2023-12345
CVE-2023-67890
```

## Requirements

- GitHub Code Scanning must be enabled (free for public repos)
- For private repos: requires GitHub Advanced Security or Code Security features
