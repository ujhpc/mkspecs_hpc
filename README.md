HPC mkspecs for Qmake (Qt)
--------------------------

## Setting up

Put `mkspecs` into your *Qmake* based app root:

	git submodule add https://github.com/ujhpc/mkspecs_hpc.git mkspecs

To enable support for *Qt* `<= 5.1` *Qmake* please add `features` symlink:

	ln -s mkspecs/features .

**NOTE:** *Qt* 5.2.1 (or higher) require `.qmake.conf` file (may be empty) in
project root in order to tell *Qmake* where to search for `mkspecs`, as this
folder search heuristics were removed in 5.2.1.

## Usage

### CUDA

In your *CUDA* enabled project add:

	CONFIG += cuda
	CUDA_SOURCES += kernel.cu
	NVCC_FLAGS += some_flags

This will detect `CUDA_HOME` from `nvcc` command path, otherwise it will raise
error. You may override `CUDA_HOME` to specify path manually.

### Intel CC for MIC

This adds also `linux-icc-mic` compiler specification which is a simple
variation of `linux-icc-64` adding `-mmic` target flags.

1. To use it from command line call: `qmake -spec linux-icc-mic`

2. To use it from *Qt Creator* clone your *ICC* SDK and put `linux-icc-mic`
	into empty place for *Qmake* spec.
