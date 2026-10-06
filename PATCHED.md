# patched branch

Upstream `dev` plus the fix branches, built by `.github/workflows/ghcr.yml` into
`ghcr.io/marck/aerofoil` (`latest` and `sha-<commit>`, amd64 and arm64). Every push to
`patched` runs the test suite, then builds and pushes.

| Branch | Upstream PR |
|---|---|
| fix/control-nca-header-only | luketanti/AeroFoil#176 |
| fix/identify-commit-per-file | luketanti/AeroFoil#177 |
| fix/duplicate-delete-active-download | luketanti/AeroFoil#178 |
| fix/import-identify-with-titledb | luketanti/AeroFoil#179 |

Pick up upstream changes or a new fix:

```bash
git fetch upstream
git checkout patched
git merge upstream/dev            # or: git merge origin/fix/<name>
python -m unittest discover -s tests
git push origin patched
```

Build locally (podman): `podman build --build-arg AEROFOIL_VERSION=local -t aerofoil:local .`
