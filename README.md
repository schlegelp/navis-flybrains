<p align="center">
<img src="https://github.com/schlegelp/navis-flybrains/blob/main/_static/flybrains_logo.png?raw=true" width="400">
</p>

# navis-flybrains
Transforms to map between different _Drosophila_ template brains. Intended to be used with [navis](https://github.com/schlegelp/navis).

This library is analogous to Greg Jefferis' [nat.templatebrains](https://github.com/natverse/nat.templatebrains), [nat.jrcbrains](https://github.com/natverse/nat.jrcbrains) and [nat.flybrains](https://github.com/natverse/nat.flybrains) for R.

`flybrains` ships with meta data and surface meshes for 17 template brains.
Transforms need to be downloaded separately (see below).

## Installation
You can install `flybrains` from PyPI:

```bash
pip3 install flybrains
```

### External dependencies
In order to use the Jefferis lab transforms, you will need to have
[CMTK](https://www.nitrc.org/projects/cmtk/) installed.

## Bridging transforms

<p align="center">
<img src="https://github.com/schlegelp/navis-flybrains/blob/main/_static/bridging_graph.png?raw=true" width="800">
</p>

It's highly recommended that after install, you download the optional
bridging transforms to map between template brains.

> :exclamation: If you already have downloaded these registrations via `nat.jrcbrains` and/or `nat.flybrains` you can skip this: `flybrains` should be able to find the registrations downloaded via R and register them for you (see also code at the bottom).

```Python
>>> import flybrains

# This downloads (or updates) various CMTK bridging and mirror transforms
# generated or collated by the Jefferis lab - see docstring for details
>>> flybrains.download_jefferislab_transforms()

# This downloads h5 bridging transforms generated by the Saalfeld lab (Janelia)
# - see docstring for details
>>> flybrains.download_saalfeldlab_transforms()

# Register the transforms - this is only necessary if you just downloaded them
>>> flybrains.register_transforms()
```

In the future, simply importing `flybrains` is sufficient to make the
transforms available to [navis](https://navis.readthedocs.io/en/latest/):

```Python
>>> import navis
>>> import flybrains
>>> import numpy as np
>>> points = np.array([[0, 0, 0]])
>>> navis.xform_brain(points, source='FAFB', target='JRC2018F')

```

On import of `flybrains`, these data sources are injected into and can be
readily used to e.g. transform 3d coordinates between brain spaces.

To check which transforms are available (either downloaded or via R) you can
run this:

```Python
>>> # Generate a report - note the mix reg downloaded via Python and R
>>> flybrains.report()
Flybrains Status Report
=======================
Data Home: /Users/philipps/flybrain-data

Jefferis lab registrations: 41 of 41
Saalfeld lab registrations: 0 of 6

nat regdirs
-----------
/Users/philipps/Library/Application Support/rpkg-nat.templatebrains/regfolders: 41 CMTK | 0 H5 transforms
/Library/Frameworks/R.framework/Versions/3.6/Resources/library/nat.flybrains/extdata/bridgingregistrations: 5 CMTK | 0 H5 transforms
/Library/Frameworks/R.framework/Versions/3.6/Resources/library/nat.flybrains/extdata/mirroringregistrations: 5 CMTK | 0 H5 transforms
/Users/philipps/Library/Application Support/R/nat.jrcbrains: 0 CMTK | 5 H5 transforms
```

## Documentation
Please see the [transform tutorial](https://navis.readthedocs.io/en/latest/source/tutorials/transforming.html)
for navis to learn how to use the data `flybrains` provides.

## Changes
- `0.1.1` (06/01/21): added `um` (for microns) suffix to `JRCFIB2018F` transforms; added affine `JRCFIB2018Fraw` -> `JRCFIB2018F` -> `JRCFIB2018Fum` transforms
- `0.1.0` (03/01/21): first working version  

## Acknowledgements
Critically based on `nat.flybrains` and `nat.jrcbrains` by Greg Jefferis
_et al._ for inspiration for the implementation and meta data on e.g. template
brains.

As reference for the Jefferis lab registrations, please use:

```
The natverse, a versatile toolbox for combining and analysing neuroanatomical data.
A.S. Bates, J.D. Manton, S.R. Jagannathan, M. Costa, P. Schlegel, T. Rohlfing, G.S. Jefferis
eLife. 9 (2020) e53350. doi:10.7554/eLife.53350.
```

As (partial) reference for the Saalfeld lab registrations, please see:

```
An unbiased template of the Drosophila brain and ventral nerve cord.
John A Bogovic, Hideo Otsuna, Larissa Heinrich, Masayoshi Ito, Jennifer Jeter, Geoffrey Meissner, Aljoscha Nern, Jennifer Colonell, Oz Malkesman, Kei Ito, Stephan Saalfeld
bioRxiv 376384; doi: https://doi.org/10.1101/376384
```

For references of individual template brains, please see their docstrings:
```Python
>>> help(flybrains.IBN)
```
