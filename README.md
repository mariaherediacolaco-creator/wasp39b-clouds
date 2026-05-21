# WASP-39b Patchy Cloud Transmission Spectrum

## Overview
This notebook models the transmission spectrum of WASP-39b, a hot Jupiter observed by JWST, under varying terminator cloud fractions using the [PICASO](https://natashabatalha.github.io/picaso/) radiative transfer code. The JWST data comes from Ahrer et al. 2022 (Nature), the first published JWST transmission spectrum of WASP-39b.

## Scientific Question
How does partial cloud coverage at the terminator affect the observed transmission spectrum, and what does this mean for atmospheric retrievals?

## Method
Two end-member spectra were computed:
- **Clear atmosphere** (0% cloud cover): no cloud opacity
- **Fully cloudy atmosphere** (100% cloud cover): grey cloud deck at 1 bar with optical depth 10

Intermediate cloud fractions (25%, 50%, 75%) were obtained by linearly mixing the two spectra, following the patchy cloud parameterization in PICASO.

## Planet Parameters (WASP-39b)
| Parameter | Value |
|-----------|-------|
| Mass | 0.28 MJup |
| Radius | 1.27 RJup |
| Star Teff | 5400 K |
| Star logg | 4.5 |
| Star radius | 0.895 RSun |
| Stellar grid | Phoenix |

## Transmission Spectrum

![Patchy clouds model](plot_wasp39b-patchy_clouds.png)

## Results

As cloud fraction increases from 0% to 100%:
- The **water bands** (0.9, 1.4, 1.9 µm) are progressively muted
- The **CO2 feature at 4.3 µm** — detected by JWST in WASP-39b — collapses dramatically
- Intermediate cloud fractions produce spectra degenerate with changes in molecular abundances

## Note on Absolute Offset
The models in this notebook sit ~0.003 above the JWST data in absolute transit depth. This is expected: the atmosphere profile used here is PICASO's built-in generic hot Jupiter P-T profile (`HJ_pt()`), which assumes a hotter, more extended atmosphere than WASP-39b's actual retrieved profile. The paper's PICASO model (included for comparison) was run with WASP-39b's fitted P-T profile, 10x solar metallicity, C/O = 0.5x solar, and fsed = 0.6. Fitting the actual P-T profile and chemical abundances to the data is the retrieval step this project does not perform. The focus here is on the relative effect of cloud fraction on spectral feature amplitude, which is independent of the absolute offset.

## Key Takeaway
This degeneracy between cloud coverage and chemical abundances is one of the central challenges in exoplanet atmospheric retrieval. A 50% cloudy terminator can mimic an atmosphere with lower water or CO2 abundance. Independent constraints — such as polarimetry — could help break this degeneracy by probing cloud geometry directly.

## Data Sources
- JWST data: Ahrer et al. 2022, Nature, https://doi.org/10.1038/s41586-022-05269-w
- Zenodo data archive: https://doi.org/10.5281/zenodo.6959427

## Requirements
- PICASO 4.0
- Python 3.11
- See [PICASO installation guide](https://natashabatalha.github.io/picaso/installation.html)
