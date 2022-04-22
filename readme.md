# [OII] maps from SITELLE

The WCS information in the cubes and deepframe is wrong (compare with MUSE nebulae catalogue regions). The WCS information in the fits cubes is correct.



This folder contains preliminary [OII] linemaps from CHFT/SITELLE observations. The fitting of the emission lines was performed with the [ORCS](https://orcs.readthedocs.io/en/latest/index.html) package by Thomas Martin. The [OII]3727 and [OII3729] lines are fitted simultaneously with a fixed ratio of [OII]$\frac{3729}{3727}=1.4$.

The data in the subfolders are the raw output from ORCS. The `name_[OII]_maps.fits` files are reprojected to the header of the MUSE data and combine the maps for the [OII]3727 and [OII]3729 lines. 

Each region from Francesco's nebulae catalogue is individually fitted. The result is saved to `name_nebulae_OII.fits`. The spectra of each region (together with the fit) can be found in `name_spectra_OII.fits`.

## Targets

* NGC 2835: fit required binning of 10x10 pixels
* NGC 4535: very poor signal. No successful fit.

not yet observed:

* NGC 1087 
* NGC 1300 
* NGC 4254 
* NGC 4303 
* NGC 4321
* 

-- Fabian Scheuermann, 2020.05.26





## Install

https://github.com/thomasorb/orb

:exclamation: numpy does not support float128 under windows. It is therefore difficult to use orb under windows :exclamation:



### 1. install `conda-build` tools

```
conda install conda-build
```

### 2. create orb3 environment

from file

```
conda env create -f environment.yml
```

or create an environment and install needed modules manually

```
conda create -n orb3 python=3.7 
conda activate orb3
conda install -n orb3 numpy scipy bottleneck matplotlib astropy cython h5py dill pandas pytables
conda install -n orb3 -c conda-forge pyregion
conda install -n orb3 -c astropy photutils astroquery
conda activate orb3
```

now your prompt should be something like `(orb3) $`.

fro windows this requires https://visualstudio.microsoft.com/visual-cpp-build-tools/

```
pip install gvar==9.2 --no-deps
pip install lsqfit==11.2 --no-deps
pip install fpdf --no-deps 
```

### 3. add ORB module

clone [ORB](https://github.com/thomasorb/orb) in local folder

```
git clone https://github.com/thomasorb/orb.git
```

in the downloaded folder

```
python setup.py build_ext --inplace
python setup.py install # not for developer
```

### 4. install ORCS

clone [ORCS](https://github.com/thomasorb/orcs) in local folder and there

```
python setup.py install
```



### 5. install jupyter

```
conda install -n orb3 -c conda-forge jupyterlab
```

Run it

```
conda activate orb3 # you don't need to do it if you are already in the orb3 environment
jupyter lab
```