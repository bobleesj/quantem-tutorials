# Widget tutorial boundaries

- Keep eight notebooks: Basic and Advanced for MPS and CUDA, each with metadata-first and manual calibration. Put installation
  instructions in `setup/README.md`, with dependencies in `setup/mps.yml` and
  `setup/cuda.yml`. Keep the folder README short.
- Consult [QuantEM Widget documentation](https://electronmicroscopy.github.io/quantem.widget/),
  especially [Show4DSTEM](https://electronmicroscopy.github.io/quantem.widget/api/show4dstem.html)
  and [ShowPtycho](https://electronmicroscopy.github.io/quantem.widget/api/showptycho.html).
  For loading, calibration and SSB computation, consult
  [QuantEM GPU documentation](https://bobleesj.github.io/quantem.gpu/) and its
  [IO API](https://bobleesj.github.io/quantem.gpu/api/io.html).
  Verify signatures against the user's installed version before changing calls.
- Use public `quantem.gpu` APIs for loading and computation; widgets own
  interaction and display. Reuse loaded acquisitions instead of loading twice.
  Use local H5/QEM paths supplied by the user; do not add dataset downloads.
- Keep both main workflows automatic; require no supplied aberrations. Expose
  the search budget and refinement method. Advanced keeps editable default
  ranges and known higher-order terms in optional recipes. Distinguish applying
  supplied higher orders from fitting them; verify defaults against the API.
- CUDA tutorials expose `device="cuda:0"` and pass it to `io.load(device=...)`.
  Preserve that device in later computation; backend-only arguments still take
  `"cuda"`. Keep comparison and plotting implementations in the library.
- Keep `qw.profile()` in the first configuration cell. Verify the selected
  kernel and MPS/CUDA device; never substitute CPU silently. Do not reduce data
  resolution, valid BF support or precision merely to pass a tutorial test.
- Render each widget/report once using the cell's final expression. Use
  `(row, col)` coordinates and explicit units. Keep Auto output sampling.
- Follow quantem.widget's `docs/maintainer/display-api.md` for display naming:
  named `size` presets, default `"medium"`, and plain `rows` / `columns` where
  implemented. Size describes each image panel. Do not make beginner notebooks
  calculate `axsize`, `figsize`, pixels or DPI. Verify installed signatures;
  retain legacy keywords until the owning library supports their replacement.
- Label rotation polarity as conditional evidence and depth spread as a model
  parameter. A manual reconstruction must not silently start an aberration fit.
- Test changed paths in a fresh kernel on the matching backend, then verify
  live widget interactions in the browser. Syntax checks and synthetic API
  smoke tests are not full experimental or fresh-install validation.
- Preserve private evidence outside this folder. Public notebooks must have
  no private paths, experimental data, outputs, execution counts, attachments
  or widget state. Keep validation limitations explicit in the setup guide.

## Publication privacy

- Keep unpublished acquisition identities, collaborator/company names, source
  paths, dataset-specific metadata/calibrations, and experimental images or
  results out of these public tutorials. Use a generic local path such as
  `scan_master.h5`; users load their own data locally.
- Anonymizing a filename does not make a private phase image, histogram,
  screenshot, or saved widget payload publishable. Keep validation evidence
  outside the public checkout; no private-data preview exports or uploads.
- Before pushing, inspect every notebook's source, outputs, attachments,
  execution counts, metadata and widget state, plus added files and outgoing
  commits. Public examples must use explicitly public or authorized data.
