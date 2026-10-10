# patched branch

Upstream `dev` plus any fix branches not merged upstream yet, built by
`.github/workflows/ghcr.yml` into `ghcr.io/marck/aerofoil` (`latest` and
`sha-<commit>`, amd64 and arm64). The original fixes (luketanti/AeroFoil#176 to #179)
are merged upstream, so for now this branch is upstream `dev` plus this CI.

## Update to the newest upstream dev

Actions, then **Build and push to GHCR**, then **Run workflow** (upstream branch `dev`).
It merges upstream into a copy of `patched`, runs the tests and publishes
`dev-<upstream commit>-<patched commit>`; the run summary names the tag. The branch
itself is not changed (GITHUB_TOKEN may not push upstream's workflow edits). A merge
conflict or a failing test stops the run before anything is published. Leave the
field empty to build `patched` as is (`sha-<commit>`).

## Add a fix

```bash
git fetch upstream
git checkout patched
git merge upstream/dev && git merge origin/fix/<name>
python -m unittest discover -s tests
git push origin patched     # every push to patched builds the image
```

Build locally (podman): `podman build --build-arg AEROFOIL_VERSION=local -t aerofoil:local .`
