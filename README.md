# cloud-me-pvt

Registry index for the private cloud-me family (Cloud-Me-Pvt) - same model as `CG`, `Fin-CM` and `cloud`. This repo is an INDEX, not a container: it holds `repos.json` (the registry, a subset of _git-repos-master/repos.json), `clone.sh` (pick which repos to have locally) and one committed relative symlink per member (`<member> -> ../<member>`); the actual clones live as siblings in `~/git/`.

## Members

- [cloud-me-pvt-vault](https://github.com/diegonmarcos/cloud-me-pvt-vault) - Secrets (sops/age). Every credential the fleet uses.
- [cloud-me-pvt-cgc](https://github.com/diegonmarcos/cloud-me-pvt-cgc) - The PRIVATE half of the cgc pipeline (pvt surface: the private repos -> cloud-cgc-pvt-mcp). A thin orchestrator rendered from cloud-u-containers_cgc at a pinned sha, so private-repo runs and logs stay private. Was cloud-u-containers_cgc-pvt; renamed 2026-10-10 into the private cloud-me family (split-outs are named <parent>_<name>; every cloud-u-* repo is public).
- [cloud-me-pvt-configs](https://github.com/diegonmarcos/cloud-me-pvt-configs) - Private configs (cloud-me family). Added 2026-10-15: it existed but was missing here, so clone.sh and --sync skipped it. (/home/user/cloud-vault is just a second clone of cloud-me-pvt-vault, not a separate repo.)
- [cloud-me-pvt-data](https://github.com/diegonmarcos/cloud-me-pvt-data) - Generated fleet config consumed by cloud's services.
- [cloud-me-pvt-my-ai](https://github.com/diegonmarcos/cloud-me-pvt-my-ai) - Claude Code's durable state and the source it runs from. ~/.claude symlinks in, not out: a_sessions/<instance>/ holds transcripts, file-history, shell-snapshots and history.jsonl; b_projects/ holds MEMORY.md and memory-entries; a_commits/ snapshots every commit object of every repo here.
- [cloud-me-pvt-notes](https://github.com/diegonmarcos/cloud-me-pvt-notes) - Personal notes (Obsidian vault).
- [cloud-me-pvt-containers](https://github.com/diegonmarcos/cloud-me-pvt-containers) - The owner's own (cloud-me) containers. Created 2026-10-21 (private).

## Usage

```
./clone.sh                list what exists and what does not
./clone.sh <name>...      clone those, then link them
./clone.sh --all          clone every member
./clone.sh --link         relink whatever is already cloned
./clone.sh --relink       rewrite every link from the registry
./check-repos-sot.sh      verify repos.json against _git-repos-master
```

`repos.json` is a SUBSET of `~/git/_git-repos-master/repos.json` (the superset index of every repo this account owns): identical name/url/private/doc fields, checked by `./check-repos-sot.sh`.
