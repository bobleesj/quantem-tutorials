# Install and run

Use clean checkouts of the QuantEM forks’ `oct-24-direct-iterative-api` branch
and editable installs. Use that same branch for the tutorials and both libraries.
This is a development setup, not an RC release. No TestPyPI step is needed.

`DirectPtycho` and `run()` require the paired source versions: GPU
`0.0.1rc18.dev0` and Widget `0.0.1rc44.dev0` or later. Earlier GPU `rc17`
installs do not provide this API. Update and install both libraries together;
these development versions do not imply a published package release.

## 1. Get the tutorials

Install [Miniforge](https://github.com/conda-forge/miniforge#install), then run:

```bash
git clone --branch oct-24-direct-iterative-api https://github.com/bobleesj/quantem-tutorials.git
cd quantem-tutorials/tutorials/widget
```

The published packages and `main` branches do not yet provide this paired API.
Do not substitute them for the branch used in this guide.

## 2. Choose your backend

Run **one** pair:

```bash
# Apple silicon Mac
conda env create -f setup/mps.yml
conda activate widget-mps
```

```bash
# NVIDIA GPU computer
conda env create -f setup/cuda.yml
conda activate widget-cuda
```

CUDA requires a CUDA 13-compatible NVIDIA driver (580 or newer).
For remote CUDA, install and run Jupyter on the GPU computer; keep your browser
on your laptop.

## 3. Install once

From `tutorials/widget`, create source folders outside the tutorial repository:

```bash
mkdir -p ../../../quantem-widget-sources
cd ../../../quantem-widget-sources
git clone --branch oct-24-direct-iterative-api https://github.com/bobleesj/quantem.gpu.git
git clone --branch oct-24-direct-iterative-api https://github.com/bobleesj/quantem.widget.git
```

Run **one** installation command:

```bash
# Apple silicon Mac
python -m pip install -e './quantem.gpu[mps,plot]' -e ./quantem.widget
```

```bash
# NVIDIA GPU computer
python -m pip install -e './quantem.gpu[cuda,plot]' -e ./quantem.widget
```

Then build the widget:

```bash
cd quantem.widget
npm ci
QUANTEM_GPU_SRC=../quantem.gpu/src PYTHON=python npm run build
python -m pip check
cd ../../quantem-tutorials/tutorials/widget
python -m jupyterlab
```

Open **Basic** for your backend. Set `source` to your local H5 master or QEM
file and choose `save_dir`. Keep H5 shards beside the master. Run cells in order
with Shift+Enter; check `qw.profile()` and calibration before fitting.
Use **Advanced** for rotation/defocus comparisons and optional controls.
No dataset is downloaded.

## Next time

Activate the same environment, return to `quantem-tutorials/tutorials/widget`,
and run `python -m jupyterlab`. No reinstall is needed.
Save with Ctrl+S or Cmd+S; stop Jupyter with Ctrl+C in its terminal.

## Update

From `quantem-widget-sources`, with the environment active:

```bash
git -C ../quantem-tutorials switch oct-24-direct-iterative-api
git -C ../quantem-tutorials pull --ff-only origin oct-24-direct-iterative-api
git -C quantem.gpu switch oct-24-direct-iterative-api
git -C quantem.gpu pull --ff-only origin oct-24-direct-iterative-api
git -C quantem.widget switch oct-24-direct-iterative-api
git -C quantem.widget pull --ff-only origin oct-24-direct-iterative-api
```

Repeat the backend installation command and widget build above. Restart the
notebook kernel and reload the browser. If Git reports local changes or a
diverged branch, preserve the work before updating; do not reset it.

## Troubleshooting

- Missing `DirectPtycho` or `run`: update both source checkouts together, then
  reinstall and restart the kernel using the Update steps above.
- Wrong environment: launch Jupyter after activating the matching environment.
- No GPU: check the NVIDIA driver or use Apple silicon for MPS.
- Blank/outdated widget: rebuild, restart the kernel, and reload the browser.
- Missing H5 data: keep the master and its shards together.

The revised recipe still needs clean-environment validation. Existing-environment
notebook checks do not establish fresh-install support.

## References

- [Widget documentation](https://electronmicroscopy.github.io/quantem.widget/)
- [GPU loading and IO](https://bobleesj.github.io/quantem.gpu/api/io.html)
- [Agent instructions](../AGENTS.md)
