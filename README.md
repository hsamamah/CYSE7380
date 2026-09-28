# CYSE 7380

Python workspace for CYSE 7380, managed with [uv](https://docs.astral.sh/uv/).

## Layout

```
CYSE7380/
├── notebooks/     # Jupyter notebooks for assignments and labs
├── data/          # Datasets (git-ignored; keep it local)
├── pyproject.toml # Dependencies and project metadata
├── uv.lock        # Pinned, reproducible dependency versions
└── .venv/         # Virtualenv — never edit by hand, never commit
```

## Setup

Already done. To rebuild the environment from the lockfile on a new machine:

```bash
uv sync
```

## Daily use

Run everything through `uv` so the project environment is picked up automatically.
Do not `pip install` or `activate` anything by hand.

```bash
uv run jupyter lab --notebook-dir=notebooks   # open notebooks
uv run python script.py                       # run a script
uv add <package>                              # add a dependency
uv remove <package>                           # remove a dependency
uv run pytest                                 # run tests (if a test suite exists)
```

## Notebooks

Store assignments in `notebooks/`. One notebook per assignment, named by week, e.g.
`notebooks/week01_hw1.ipynb`.

Launch with `--notebook-dir=notebooks` as shown above. That makes `notebooks/` the
working directory, so a relative path like `../data/whatever.csv` resolves to
`data/whatever.csv` and behaves identically inside a notebook and a script.

## Notes

- Python is pinned to 3.14 in `.python-version`; the environment is created from it.
- PyTorch is installed from the CPU-only index (see `pyproject.toml`). This machine
  has Intel Arc graphics and no NVIDIA GPU, so the default CUDA build would be a
  ~3 GB download that cannot be used.
- If you later move this project to a machine with an NVIDIA GPU, drop the
  `[tool.uv.index]` block from `pyproject.toml` and re-run `uv sync`.
