# Security — Image Verification

All OCI images published from this repository are signed with [cosign](https://docs.sigstore.dev/cosign/overview/) keyless signing via GitHub Actions OIDC. SBOM attestations are attached to every image.

## Prerequisites

```bash
brew install cosign
```

## Verify image signature

Replace `<org>`, `<repo>`, `<app>`, and `<tag>` with the actual values for this repository.

The `--certificate-identity` must exactly match the GitHub Actions workflow URL for the signing repository.

```bash
cosign verify \
  --certificate-identity=https://github.com/<org>/<repo>/.github/workflows/build.yml@refs/heads/main \
  --certificate-oidc-issuer=https://token.actions.githubusercontent.com \
  ghcr.io/<org>/<repo>/<app>:<tag>
```

Exit 0 means the signature is valid. Output is JSON containing the certificate details (workflow ref, commit SHA, build timestamp).

## Verify SBOM attestation

```bash
cosign verify-attestation \
  --type spdxjson \
  --certificate-identity=https://github.com/<org>/<repo>/.github/workflows/build.yml@refs/heads/main \
  --certificate-oidc-issuer=https://token.actions.githubusercontent.com \
  ghcr.io/<org>/<repo>/<app>:<tag> \
  | jq '.payload | @base64d | fromjson'
```

Output is the full SPDX document listing all packages and dependencies in the image.
