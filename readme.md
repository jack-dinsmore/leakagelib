# LeakageLib

[![DOI](https://zenodo.org/badge/721341641.svg)](https://zenodo.org/doi/10.5281/zenodo.10483297)

Written by Jack Dinsmore in December 2023

This code predicts and corrects leakage patterns in the IXPE satellite using asymmetric PSFs. It is described in the published paper "Dinsmore, J. T. & Romani, R. W. 2024, The Astrophysical Journal, **962** 183" If you use this software, please cite that paper and the DOI of this software.

It also has routines to fit for the polarization of a point source or extended source, both using standard PCUBE analysis and with PSF weights.

Finally, it has a method to assign background probabilities to each event.

If you have questions, bug reports, or feature requests, please email Jack Dinsmore at jtd@stanford.edu.

## Installation
1. Clone this repository to your computer. For example,
```sh
git clone https://github.com/jtdinsmore/leakagelib.git
```
2. Change the `DATA_DIRECTORIES` in **src/settings.py** variable to point to where you store your IXPE data files. You can list multiple directories. Alternatively, you can use the `IXPEData.load_all_detectors_with_path` function in the script to load all your data files, and feed in the directory to the data each time.

3. Whenever you use LeakageLib in your code, add the repo you cloned to path:
```Python
import sys
sys.path.append("<<<PATH TO LEAKAGELIB REPO>>>")
import leakagelib
```

## Files

- **examples** contains example code for the main functions of this library:
    - **examples/leakage-severity.py** plots the distribution of leakage PD as predicted by LeakageLib. You can use this to determine how severe leakage is. You can also change the spectrum of the source and its spatial distribution if desired.

    - **examples/point-source.py** predicts leakage patterns for a given point source and compares to observations. This code will fail if you have not downloaded the point source observation in question (GX 9+9, obsid 01002401). Only the unzipped L2 and housekeeping files are needed (in fact, only the `*att*` housekeeping files are needed, which give the roll of the spacecraft).

    - **examples/predict.py** predicts leakage patterns for a synthetic nebula. This requires no downloads.

    - **example/extract.py** extracts true source polarization from synthetic observations of that nebula and compares them to the truth.

    - **examples/psf-fit.py** fits for the polarization of a point source, using the PSF to assign a probability that the event comes from the source or background.

- **data**: contains data used by the algorithm, including the sigma_tot measured from simulations and the sky-calibrated PSFs produced by the paper accompanying this software package.

- **src**: LeakageLib source code

- **flag_background.py**: Script to flag the background events of a source.