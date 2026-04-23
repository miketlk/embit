# Package Content Policy

This project publishes source-only Python artifacts.

## Allowed in published artifacts

- Python source files required at runtime (`src/embit/**/*.py`)
- Build metadata and license files

## Forbidden in published artifacts

- `.pth` files
- `sitecustomize.py` and `usercustomize.py`
- Bundled native binaries (`*.so`, `*.dylib`, `*.dll`) in any package path
- Nested distributions (`*.whl`, `*.tar.gz`, `*.egg`) embedded inside sdist/wheel payloads
- Nested package metadata payloads (`*.egg-info`, `*.dist-info`) from other distributions
- Prebuilt native artifacts under `src/embit/util/prebuilt/`
- Install-time execution hooks (for example custom setup/install commands or hidden startup injection paths)

## Packaging controls

- `MANIFEST.in` is the source of truth for sdist include/prune behavior.
- Setuptools package data must not include native artifacts.
- Artifact verification must confirm forbidden payloads are absent before release.
