# driver-packager — Codex executors

Executors here follow /home/agent/codeman-cases/Sam/agents/executor.md and their brief; Sam orchestrates.

## What this is

Builds Control4 `.c4z` driver packages from source dirs + manifest.
Use `dp3` for Python 3 (only `dp3` is maintained); `dp` is Python 2 legacy.
Also usable as GitHub Action `control4/drivers-driverpackager@v1`.

## Layout

- `Documentation/` — architecture graph (`architecture/codebase-graph.json`).
- `createc4z/` — legacy `CreateC4Z.py` builder.
- `dp/` — Python 2 packager (`driverpackager.py`, `build_c4z.py`, `encrypt_c4z.py`).
- `dp3/` — Python 3 packager (maintained; same three scripts; Docker uses this).
- `dplite/`, `dplite3/` — Lite packagers (Py2 / Py3).
- `generator/` — codebase-graph generator (`project_graph.py`).
- `gosquish/` — Go squish helper.
- Root: `Dockerfile`, `action.yml`, `entrypoint.sh`, `manifest.schema.json`.

## Commands (as documented)

- Build: `python3 dp3/driverpackager.py [-h] [-v] [-u] [-ae] srcdir dstdir [manifest]`
- Squish/zip: `python3 dp3/build_c4z.py [-h] [-v] [-x | -c] c4z dir`
- Encrypt: `python3 dp3/encrypt_c4z.py input_path output_path`
- Legacy: `python CreateC4Z.py c4zprojfile srcdir dstdir [-d] [-e]`
- Action: `uses: control4/drivers-driverpackager@v1` with `projectDir`, `c4zproj`, `outputDir`, `version`, `updateModified`, `allowexecute`
- Graph check: `bash .github/tests/test-graph-freshness.sh` (from repo root)
- Unit tests: none documented.

## Graph

- `S=/home/agent/codeman-cases/Sam/scripts/sam-graph.sh`
- `$S find <term> --project driver-packager`
- `$S impact <paths> --project driver-packager`

## Safety

- Secrets: names only; never print values.
- Never push to the default branch (`master`); use `task/agents-md` + PR.
