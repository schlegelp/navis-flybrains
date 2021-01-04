# navis-flybrains
Transforms to map between different _Drosophila_ template brains.

This library is analogous to Greg Jefferis' [nat.templatebrains](https://github.com/natverse/nat.templatebrains), [nat.jrcbrains](https://github.com/natverse/nat.jrcbrains) and [nat.flybrains](https://github.com/natverse/nat.flybrains) for R.

`flybrains` ships with meta data and surface meshes for 17 template brains.

You can install `flybrains` from PyPI:

```bash
pip3 install flybrains
```

It's highly recommended that after install, you download the optional
bridging registrations.

_If you already have downloaded these registrations via `nat.jrcbrains` and/or_
_`nat.flybrains` you can skip this: `flybrains`_
_should be able to find the registrations downloaded via R and register_
_them for you._

```Python
>>> import flybrains

# This downloads (or updates) various CMTK bridging and mirror transforms
# generated or collated by the Jefferis lab - see docstring for details
>>> flybrains.download_jefferislab_transforms()

# This downloads h5 bridging transforms generated by the Saalfeld lab (Janelia)
# - see docstring for details
>>> flybrains.download_saalfeldlab_transforms()

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
