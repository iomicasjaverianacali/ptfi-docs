For this repository to be used, the following listed packages need to be installed. Check their websites for the installation process.

!!! note "Python version"

    It is recommended to install Python 3.11.


1. [**DreaMS**](https://github.com/iomicasjaverianacali/DreaMS-fork)

2. [**Mist-CF**](https://github.com/samgoldman97/mist-cf)

This library has a potential source of issues during the installation process: 

- In `setup.cfg` change `version = <version number: 0.0.1` with `version = 0.0.1`.


[**Mist-Pred**](https://github.com/coleygroup/ms-pred)

1. The file `algos2.pyx` has some issues with new data types in numpy. 

```python
...

adj_mat_copy = adjacency_matrix.astype(numpy.int64, order='C', casting='safe', copy=True) # jdvg

...

path_copy = path.astype(numpy.int64, order='C', casting='safe', copy=True) # jdvg
edge_feat_copy = edge_feat.astype(numpy.int64, order='C', casting='safe', copy=True) # jdvg

...

cdef numpy.ndarray[numpy.int64_t, ndim=4, mode='c'] edge_fea_all = -1 * numpy.ones([n, n, max_dist_copy, edge_feat.shape[-1]], dtype=numpy.int64) # jdvg
```

2. The file `misc_utils.py` has some issues with old `LightningLoggerBase` pytorch lightning class. 

```python
#from pytorch_lightning.loggers import LightningLoggerBase # jdvg
from pytorch_lightning.loggers.logger import Logger  # jdvg
from pytorch_lightning.utilities.rank_zero import rank_zero_only # jdvg
#from pytorch_lightning.utilities import rank_zero_only # jdvg
#from pytorch_lightning.loggers.base import rank_zero_experiment #jdvg

...

class ConsoleLogger(Logger):
    ...
    
    @property
    @rank_zero_only # jdvg
    def name(self):
        pass

    @property
    @rank_zero_only # jdvg
    def experiment(self):
        pass

    @property
    @rank_zero_only # jdvg
    def version(self):
        pass
```

3. The file `nn_utils.py` has an outdated definition for an adjancency matrix.

```python
...

#A = g.adj(scipy_fmt="csr")  # adjacency matrix # jdvg
A = g.adj_external(scipy_fmt="csr") # jdvg
```