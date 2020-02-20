# Platypus

![Build Status](https://travis-ci.org/IvantheDugtrio/Platypus.svg?branch=master)

The Platypus variant caller. The main Web site is https://github.com/andyrimmer/Platypus.

## Installation and execution

To build Platypus, do the following:

```
    make
```

Then to run do

```
    python bin/Platypus.py --bamFiles=BAM.bam --refFile=REF.fa --output=variants.vcf
```

Platypus has been tested with Python 2.6 and 2.7, and requires Cython 0.20.2 or later
to build.

### Prerequisites

Platypus requires HTSlib 1.2.1 or greater. HTSlib can be downloaded from the [HTSlib Web site](http://www.htslib.org/download/).

To build and install HTSlib, cd into HTSlib source and type `make install`. This will install HTSlib under `/usr/local/` (see note below). To install HTSlib in any other directory use `make install prefix=/path/to/dir`.

NOTE: HTSlib should be installed in a standard location (e.g. `/usr/local/`). If not installed in a standard location, you will need to set your library paths:

* For GNU/Linux:

```
    export C_INCLUDE_PATH=/path/to/dir/include
    export LIBRARY_PATH=/path/to/dir/lib (only for making)
    export LD_LIBRARY_PATH=/path/to/dir/lib
```


Note the `/include` and `/lib` sub-directories. e.g. if you installed HTSlib under `/Users/me/htslib` then set

```
    export C_INCLUDE_PATH=/Users/me/htslib/include
    export LIBRARY_PATH=/Users/me/htslib/lib
    export LD_LIBRARY_PATH=/Users/me/htslib/lib
```

HTSlib will automatically make the `include` and `lib` directories on install.

* For OSX:

```
    export C_INCLUDE_PATH=/path/to/dir/include
    export LIBRARY_PATH=/path/to/dir/lib (only for making)
    export DYLD_FALLBACK_LIBRARY_PATH=/path/to/dir/lib
```

### Python 3 support

To make Platypus compatible with Python 3, the following modifications of Platypus's source code as well as minor tweak in Cython for Python 3.

* Redefine `__getslice__` in array.pyx
* Remove `__getslice__` check macro of Python 3 in modulenode.py
* Cythonize pyxs in `src/pysam` to c code
* Update `print` to `print()` in main py codes
* Change `StandardError` to `Exception()` or `raise Exception as`
* Update `PyString` imports in `src/pysam/TabProxies.pyx`

```
    from cpython cimport PyErr_SetString, PyBytes_Check, \
    PyUnicode_Check, PyBytes_FromStringAndSize, \
    PyObject_AsFileDescriptor
```
