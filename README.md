# HETDEX-LF MODELING
 Mathematica notebook for analyzing galaxy survey data from [HETDEX](https://hetdex.org/) (Hobby-Eberly Telescope Dark Energy Experiment). It imports HDF5 data files, applies signal-to-noise filtering, and computes and visualizes luminosity functions and completeness functions.

---

## Requirements

- [Wolfram Mathematica](https://www.wolfram.com/mathematica/) 14.2 or later
- HDF5 data files (`.h5`) from the HETDEX survey (e.g. `20240529008.h5`)

---

## Usage

1. Open `project_h5-clean.nb` in Mathematica.
2. In the **Data choice and import** cell, set the `file` variable to the path of your `.h5` data file:
   ```mathematica
   file = "path/to/your/file.h5"
   ```
3. Run all cells in order (Cell → Evaluate Notebook), or step through section by section.

---

## Notebook Structure

### Chapter 1: Definitions

Sets up all helper functions used throughout the notebook.

- **Data importing and selection** — reads dataset names and arrays from an HDF5 file; applies a signal-to-noise cut (`SNcut`) to define a *survived* galaxy sample alongside the full sample
- **Luminosity** — defines cosmological constants, computes the Hubble parameter, and builds interpolations for luminosity distance, angular diameter distance, and comoving volume element dV/dz
- **f50** — computes the flux sensitivity threshold (f50), the flux at which 50% of sources are detectable
- **Histograms** — utilities for 1D and multi-dimensional histograms: bin initialization, computation, and plotting
- **Luminosity function** — two approaches for comparing the observed and theoretical (Schechter) luminosity functions:
  - *Approach A*: discretizes the theoretical function onto histogram bins
  - *Approach B*: continuizes the experimental histogram for direct comparison
- **Completeness function** — safe histogram division and 1D completeness function r50

### Chapter 2: To-do List

In-progress notes and planned improvements.

### Chapter 3: Work

The main analysis section. Runs the full pipeline on one or more `.h5` files:

- Imports and filters data
- Produces 1D histogram plots (flux, redshift, luminosity, flux/f50 ratio) for all and survived galaxies
- Plots the completeness function
- Compares experimental and theoretical luminosity functions (both approaches)
- Runs multi-dimensional histogram analysis
- Aggregates results across multiple files

---

## Key Variables

| Variable | Description |
|---|---|
| `file` | Path to the input `.h5` data file |
| `SNcut` | Signal-to-noise threshold for the survived sample |
| `survivedQ` | Boolean list flagging galaxies that pass the S/N cut |
| `data[var]` / `data[var, all]` | Full dataset for variable `var` |
| `data[var, sur]` | Survived (S/N-filtered) subset |
| `fcut` | Minimum detectable flux |
| `skyfrac` | Fraction of sky accessible to HETDEX |

---

## Output

Running the Work chapter produces:

- Histograms of flux, wavelength, redshift, and luminosity for the full and survived samples
- Completeness function plots
- Observed vs. Schechter luminosity function comparisons
- Multi-dimensional flux–redshift histogram plots

---

## Notes

- The notebook was created with Wolfram 14.2; earlier versions may not be fully compatible.
- HDF5 files are not included in this repository. Contact the HETDEX collaboration or refer to their [public data releases](https://hetdex.org/hetdex-public-release-hdr3/) for access.
- All cosmological calculations assume a standard ΛCDM cosmology with constants defined in the **Constants** section.


