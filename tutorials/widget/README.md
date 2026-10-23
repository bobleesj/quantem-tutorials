# Widget tutorials

Load your local H5/QEM data, browse with **Show4DSTEM**, then review SSB with
**ShowPtycho**. Choose one notebook:

| Calibration | CUDA | MPS |
| --- | --- | --- |
| Metadata-first | [Basic](showptycho_cuda_metadata.ipynb) · [Advanced](showptycho_cuda_metadata_advanced.ipynb) | [Basic](showptycho_mps_metadata.ipynb) · [Advanced](showptycho_mps_metadata_advanced.ipynb) |
| Manual | [Basic](showptycho_cuda.ipynb) · [Advanced](showptycho_cuda_advanced.ipynb) | [Basic](showptycho_mps.ipynb) · [Advanced](showptycho_mps_advanced.ipynb) |

**Metadata-first:** retain recorded sampling; estimate a missing semiangle from the disk only when angular detector sampling is known.
**Manual:** enter your voltage, convergence semiangle and scan step, then fit detector sampling. Example values must be replaced.

**Basic:** load, inspect calibration, view and export BF/DF/ADF and mean diffraction images, fit automatically, review and save.
**Advanced:** the same automatic workflow, with a four-case rotation/defocus comparison,
matched phase images and histograms, regional fits, depth/tilt landscapes,
and a compact reconstructed focus gallery. Search ranges and known higher-order corrections are optional.

## Install

Follow [setup/README.md](setup/README.md): Conda environments for MPS and CUDA,
with editable library installs from `origin/main`. The setup guide records validation limitations.
Agents should read [AGENTS.md](AGENTS.md) and the linked Widget/GPU API docs.

## Run

1. CUDA notebooks use `device="cuda:0"`, the first visible GPU; change the index if needed.
2. Set `source` to your local H5 master or QEM file. Keep H5 shards beside the master.
3. Set `save_dir` to a separate results folder for that acquisition.
4. Run cells in order; check calibration and detector geometry before fitting.
5. Review the widget, wait for any regional fits, then save.

Display galleries use `size="medium"` for each panel and `columns` for images
across, or `rows` for images down. Detector-fit plots and static SSB views
share `size`, `cmap` and `save`; interactive focus views also accept `cmap`.
`save` exports a figure; `save_dir` stores calibration. These options do not
change scientific arrays.

No dataset is downloaded and no aberration values are required. CUDA starts
with `search="broad"`; use `"standard"` for primary optics plus tilt/depth.
MPS uses `"standard"` while broad remains CUDA-only. Broad fits terms through
fifth order; it does not certify that those coefficients are physical probe aberrations.
Advanced notebooks expose an optional trial budget, standard-search bounds,
rotation diagnostics and regional review.

**Development checkpoint:** these calls require the search-modes GPU candidate.
They are not yet available in the tested `origin/main` installation. Do not use
this tutorial revision on an acquisition machine until integration is complete.

Keep experimental data, saved calibrations and private notebook outputs out
of Git. Phase-polarity evidence is not an independent rotation measurement;
SSB depth spread is not a direct thickness measurement.
