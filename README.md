# liken-dev-cluster

The fleet repository for liken's GitOps lab (the `gitops-cluster/`
deployment in liken-sh/liken). The cluster syncs this repository's
root through Flux, laid out the single-cluster way:

* `flux-system/` holds the engine, `gotk-components.yaml`. This
  repository owns the engine: upgrade Flux by committing a new
  rendering, and add components beyond the floor the same way. The
  cluster only plants a pinned seed copy when the engine is absent.
* `liken/` holds the fleet's declared state: the Cluster document
  and one Machine document for each machine.

Do not add the sync objects (`GitRepository`, `Kustomization`) here.
liken renders them from the Cluster document's flux declaration, and
a copy in git would fight that rendering.
