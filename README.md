# liken-dev-cluster

The fleet repository for liken's GitOps lab: the
[`gitops-cluster/`](https://github.com/liken-sh/liken/tree/main/gitops-cluster)
deployment in [liken-sh/liken](https://github.com/liken-sh/liken).
That lab boots a small QEMU fleet whose declared state is stored here,
so this repository's history is the drill log: each commit is an
edit the fleet applied, or one it refused on purpose.

The cluster syncs this repository's root through
[Flux](https://fluxcd.io), laid out the single-cluster way that
[the GitOps guide](https://liken.sh/docs/guides/gitops/) describes:

* `flux-system/` contains the engine, `gotk-components.yaml`. This
  repository owns the engine: upgrade Flux by committing a new
  rendering, and add components beyond the floor the same way. The
  cluster applies a pinned seed copy only when the engine is absent.
* `liken/` contains the fleet's declared state: the Cluster document
  and one Machine document for each machine. The dev cluster's
  documents
  ([`dev-cluster/`](https://github.com/liken-sh/liken/tree/main/dev-cluster)
  in the main repository) teach what every field means. The
  documents here record only what this lab chooses differently.

Do not add the sync objects (`GitRepository`, `Kustomization`) here.
liken renders them from the Cluster document's flux declaration
([`init/features.go`](https://github.com/liken-sh/liken/blob/main/init/features.go)
in the main repository), and a copy in git would conflict with that
rendering.
