# Working on liken-dev-cluster

This repository is the fleet repository for the GitOps lab in
[`liken`](https://github.com/liken-sh/liken). The lab's QEMU fleet syncs
this repository's root through Flux, so each commit here is an edit the
fleet applies. `README.md` describes the layout.

Do not add the Flux sync objects (`GitRepository`, `Kustomization`).
`liken` renders them from the Cluster document, and a copy in git
conflicts with that rendering.
