# LAMMPS

[LAMMPS](https://lammps.sandia.gov/) is a large scale classical
molecular dynamics code, and stands for Large-scale Atomic/Molecular Massively
Parallel Simulator.  LAMMPS has potentials for soft materials (biomolecules,
polymers), solid-state materials (metals, semiconductors) and coarse-grained or
mesoscopic systems. It can be used to model atoms or, more generically, as a
parallel particle simulator at the atomic, meso, or continuum scale.

## Availability

```python exec="on"
import pandas as pd

df = pd.read_csv('docs/assets/tables/module.csv')
soft = df.query('Software == "LAMMPS"')
print(soft.to_markdown(index=False))
```


| Version | Module name   | Toolchain |
|---------|---------------|-----------|
| 102025  | lammps/102025 | foss      |

!!! note

     explain what toolchain means here


## Application Information, Documentation and Support

The official LAMMPS is available at [LAMMPS Online Manual](https://lammps.sandia.gov/doc/Manual.html). 
LAMMPS has a large user base and a good user support. 
Question related to using LAMMPS can be posted to the [LAMMPS User forum](https://matsci.org/c/lammps/40). 
Archived [user mailing list](https://sourceforge.net/p/lammps/mailman/lammps-users/) are also useful to resolve 
some of the common user issues. 

!!! tip
    If *after* checking the above forum, if you believe that there is an issue
    with the module, please file a ticket with [Service Now](mailto:hpc@njit.edu)


## Using LAMMPS 

To use the default version of LAMMPS, type:

```console
module load lammps
```

### Using LAMMPS

??? example "Sample Batch Script to Run LAMMPS"

    ```slurm
    #!/bin/bash
    #SBATCH -J test_lammps
    #SBATCH -C haswell
    #SBATCH -q debug
    #SBATCH -N 2
    #SBATCH -t 30:00
    #SBATCH -o test_lammps.o%j

    module load lammps

    srun -n 64 -c 2 --cpu-bind=cores lmp_cori -in test.in
    ```

Then submit the job script using the sbatch command, e.g., assuming the job
script name is `test_lammps.slurm`:

```console
sbatch test_lammps.slurm
```

## Building LAMMPS from source

Some users may be interested in building LAMMPS from source to enable more specific LAMMPS packages. 
The source files for LAMMPS can be [downloaded](https://www.lammps.org/download.html) as either a tar file 
or from the [LAMMPS Github repository](https://github.com/lammps/lammps). 

??? example "Building on Wulver"
	The following procedure was used to build LAMMPS on Wulver. 
    In the terminal:

    ```bash
    module purge
    module load esslurm
    module load gcc/11.2.0
    module load openmpi/4.1.2
    module load cmake

    git clone https://github.com/lammps/lammps.git
    cd lammps
    mkdir build
    cd build

    cmake -DCMAKE_INSTALL_PREFIX=$PWD/../install_hsw -DCMAKE_CXX_COMPILER=mpicxx \
                -DCMAKE_BUILD_TYPE=Release -D BUILD_MPI=yes -DKokkos_ENABLE_OPENMP=ON \
                -DKokkos_ARCH_HSW=ON -DCMAKE_CXX_STANDARD=17 -D PKG_MANYBODY=ON \
                -D PKG_MOLECULE=ON -D PKG_KSPACE=ON -D PKG_REPLICA=ON -D PKG_ASPHERE=ON \
                -D PKG_RIGID=ON -D PKG_KOKKOS=ON -D DOWNLOAD_KOKKOS=ON \
                -D CMAKE_POSITION_INDEPENDENT_CODE=ON -D CMAKE_EXE_FLAGS="-dynamic" ../cmake
    make -j16
    make install
    ```

## Related Applications

* [GROMACS](gromacs.md)

## User Contributed Information

!!! info "Please help us improve this page"
        Users are invited to contribute helpful information and corrections
        through our [Github repository](https://github.com/arcs-njit-edu/Docs/blob/main/CONTRIBUTING.md).


