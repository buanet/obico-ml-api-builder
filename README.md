# obico-ml-api-builder
Builds Docker image for ml-api from obico project

The `Build and publish ml_api` workflow checks the `release` branch of
`TheSpaghettiDetective/obico-server` once a day and can also be run manually.
When its latest commit differs from `.github/dependencies/.commit-id`, it
builds only the `ml_api` service from that revision and publishes
`ghcr.io/<owner>/obico-ml-api` with both the source commit SHA and `latest`
tags. The recorded commit is updated only after both image tags were pushed.

The workflow requires the repository's Actions setting **Workflow permissions**
to allow read and write access, so its token can publish to GHCR and commit the
updated `.commit-id`. GHCR package visibility can be changed in the package
settings after its first successful publication.
