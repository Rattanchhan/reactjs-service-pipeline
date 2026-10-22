# ReactJS Service Pipeline Deployment

This directory is intended to be published as the application repository.
The same React source is promoted through two protected branches:

- `dev` publishes an immutable image and proposes its digest to
  `environments/dev` in the GitOps repository.
- `prod` publishes an immutable image and proposes its digest to
  `environments/prod`.

The workflow runs install, lint, test, application build, container build,
registry push, registry pull verification, image scanning, and GitOps pull
request creation. It never receives Kubernetes or Argo CD credentials.

Configure this GitHub repository with:

- variable `GITOPS_REPOSITORY`: `OWNER/argocd-gitops-repository`
- secret `GITOPS_TOKEN`: fine-grained token with Contents read/write and Pull
  requests read/write on only the GitOps repository

Protect `dev` and `prod`, require the `quality` job, and require review for
GitOps promotion pull requests.
