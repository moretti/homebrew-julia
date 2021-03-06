homebrew-julia
==============

A small tap for the [Homebrew project](http://mxcl.github.com/homebrew/) to install [Julia](http://julialang.org/). After installing Homebrew, you must install a fortran compiler. After that, all other dependencies will automatically be downloaded and compiled followed by Julia herself:

```
$ brew update
$ brew install gfortran
$ brew tap staticfloat/julia
$ brew install --HEAD julia
```

If you want to use [Gaston](https://bitbucket.org/mbaz/gaston) for plotting, install gnuplot with the optional `wxmac` included before trying to plot with Gaston:

```
$ brew install gnuplot --wx
```

Compiling 64-bit Julia
======================
Julia and dependent libraries can be compiled in 64-bit mode, allowing for 64-bit array indexes, and therefore arrays larger than 2^32 elements along a single axis.  To compile Julia in 64-bit mode, specify the `--64bit` option when installing:

```
$ brew install --HEAD --64bit julia
```

This will compile all necessary dependencies as 64-bit as well, with a `64` suffix on the name to distinguish these dependencies from their 32-bit counterparts (e.g. `openblas-julia` has the 64-bit counterpart `openblas-julia64`).  Note that it currently is not possible to install 32-bit and 64-bit julia side-by-side.


Using OpenBLAS HEAD
===================
If you wish to test the newest development version of [OpenBLAS](https://github.com/xianyi/OpenBLAS) with Julia, you can do so by manually unlinking OpenBLAS, and installing the HEAD version of the formula:

```
$ brew unlink openblas-julia
$ brew install openblas-julia --HEAD
```

This will install the latest `develop` branch of OpenBLAS.  Julia will happily link against this new version, but unfortunately SuiteSparse will not, so we must recompile SuiteSparse and therefore Julia:

```
$ brew rm suite-sparse-julia julia
$ brew install --HEAD julia
```

Known Issues
============
* The `--with-accelerate` option does not work due the newer BLAS functions available in OpenBLAS, relied upon by Julia. This is not being actively investigated, as usage of Accelerate is not a high priority.

