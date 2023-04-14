# MATLAB

MATLAB (matrix laboratory) is a multi-paradigm numerical computing environment and proprietary programming language developed by MathWorks. MATLAB allows matrix manipulations, plotting of functions and data, implementation of algorithms, creation of user interfaces, and interfacing with programs written in other languages. Although MATLAB is intended primarily for numerical computing, an optional toolbox uses the MuPAD symbolic engine allowing access to symbolic computing abilities. An additional package, Simulink, adds graphical multi-domain simulation and model-based design for dynamic and embedded systems.

## Availability

| Version | Module name |
|---------|-------------|
|  2021a  | matlab/2021a |
|  2021b  | matlab/2021b |


??? note "List of Available Toolchains"
    List to go here

## Using MATLAB

```console
module load matlab
```

???+ exmaple "Sample Batch Script to run MATLAB"

    ```slurm
    #!/bin/bash
    #SBATCH -J test_matlab
    #SBATCH -n 1
    #SBATCH -N 1
    #SBATCH - t 30:00

    module load matlab

    matlab --nodisplay --nosplash -r test

    ```

??? example "Sample MATLAB script"

    ```matlab
    A = [ 1 2; 3 4]
    A.**2
    ```


## Additional information
To learn how to install a version of MATLAB on your local system and use it to run jobs on Wulver, please see [Using Local MATLAB on Wulver](matlab_local.md)


