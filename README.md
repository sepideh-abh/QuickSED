# QuickSED

**A lightweight Python package for generating Spectral Energy Distributions (SEDs) from multi-band photometry tables.**

---

## Background

The idea for this package came to me during a hands-on session on radiative processes in astrophysics. I was trying to estimate the effective temperature of a white dwarf by plotting its Spectral Energy Distribution (SED). After collecting data from various catalogs like GAIA and 2MASS, I found myself struggling just to identify which magnitudes belonged to which filters, what zero points to use, and how to convert them properly. I thought — this should be easier. This package is the result of that experience.

---

## Requirements

- Python ≥ 3.8
- numpy
- pandas
- matplotlib
- astropy
- pyphot

---

## Problem the Project Aims to Solve

Astronomers frequently need to visualize the spectral energy distributions of astronomical objects based on photometric data from different surveys. This task involves:
- Merging magnitudes across filters
- Converting to flux units
- Applying extinction or redshift corrections
- Plotting results cleanly

All of this is time-consuming and error-prone when done manually. **BatchSED** aims to simplify this pipeline, especially for batch processing.

---

## Expected Functionality of the Project

1. **Read photometry tables** (CSV, ASCII, or FITS)
2. **Identify filter bands and units** (e.g., GAIA_G, 2MASS_J)
3. **Convert magnitudes to fluxes** using standard zero points
4. **Apply optional extinction or redshift corrections**
5. **Plot log-log SEDs** for one or more objects
6. **Export plots** and optionally a table of corrected fluxes

---

## Why Each Piece of Functionality is Needed

| Feature                      | Why It’s Needed |
|-----------------------------|------------------|
| Filter recognition           | Automate mapping of columns to wavelengths |
| Magnitude-to-flux conversion| Plotting requires flux vs λ |
| Extinction correction       | Dust affects observed SEDs |
| Redshift handling           | Needed for distant galaxies or quasars |
| Batch plotting              | Often working with many objects |
| CLI/Script interface        | Useful for pipelines or non-interactive use |

---

## Interfaces / Dependencies

- **Input**: Table file with one row per object; columns for magnitudes or fluxes.
- **Output**: PNG/PDF plots; optional output CSV with fluxes per filter.
- **Dependencies**: Core Python libraries and `astropy` for astronomical handling.
- **Interface**: Command-line and/or Python script

---

## 👤 User Stories

### Main Functionality

**User Story 1:**  
_As an undergraduate student working on stellar astrophysics, I want to quickly convert a table of magnitudes from different filters into SED plots, so that I can estimate stellar temperatures visually._

**User Story 2:**  
_As a researcher with a catalog of 1000 galaxies, I want to generate SEDs for each object and save the plots to disk in one command, so I can later inspect their shapes._

---

### Edge Cases

**Edge Case 1:**  
_As a user who accidentally includes inconsistent units or unknown filters, I want the program to raise a clear error or warning instead of silently failing._

**Edge Case 2:**  
_As a user analyzing a reddened object, I want to optionally provide extinction values to correct the observed magnitudes, so my SED better reflects intrinsic properties._

---

##  Pseudocode Usage Examples

### Basic Usage: From CSV with GAIA/2MASS magnitudes

```python
from batchsed import SEDBuilder

sed = SEDBuilder("my_photometry.csv")
sed.convert_magnitudes_to_flux()
sed.plot_all(output_dir="output_plots/")
