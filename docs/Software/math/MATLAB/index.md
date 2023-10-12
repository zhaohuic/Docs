# MATLAB

MATLAB (matrix laboratory) is a multi-paradigm numerical computing environment and proprietary programming language developed by MathWorks. MATLAB allows matrix manipulations, plotting of functions and data, implementation of algorithms, creation of user interfaces, and interfacing with programs written in other languages. Although MATLAB is intended primarily for numerical computing, an optional toolbox uses the MuPAD symbolic engine allowing access to symbolic computing abilities. An additional package, Simulink, adds graphical multi-domain simulation and model-based design for dynamic and embedded systems.

## Availability

```python exec="on"
import pandas as pd

df = pd.read_csv('docs/assets/tables/module.csv')
soft = df.query('Software == "MATLAB" | Software == "matlab"')
print(soft.to_markdown(index=False))
```


??? note "List of Available Toolchains"
    List to go here

## Using MATLAB

### Serial Job
??? exmaple "Sample Batch Script to run MATLAB: matlab-serial.sh"

    ```slurm
    #!/bin/bash
    #SBATCH -J test_matlab
    #SBATCH --partition=regular
    #SBATCH -nodes=1
    #SBATCH --ntasks-per-node=1
    #SBATCH - t 30:00
    
    # Load matlab module
    module purge
    module load MATLAB/2022a

    matlab --nodisplay --nosplash -r test

    ```

??? example "Sample MATLAB script"

    ```matlab
    A = [ 1 2; 3 4]
    A.**2
    ```

### Parallel Job

### Single node parallelization
??? exmaple "Sample Batch Script to run MATLAB: matlab_parallel.sh"
    
    ```slurm
    #!/bin/bash
    #SBATCH -J test_matlab
    #SBATCH --partition=regular
    #SBATCH -nodes=1
    #SBATCH --ntasks-per-node=32
    #SBATCH - t 30:00
    
    # Load matlab module
    module purge
    module load MATLAB/2022a

    # Run matlab
    matlab -nodisplay --nosplash -r for_loop.m
    ```

??? example "Sample Parallel MATLAB script: for_loop.m"

    ```matlab
    poolobj = parpool('local',32);
    fprintf('Number of workers: %g\n', poolobj.NumWorkers);

    tic
    n = 2000;
    A = 500;
    a = zeros(n);
    parfor i = 1:n
        a(i) = max(abs(eig(rand(A))));
    end
    toc
    ```

## Multi node parallelization
If you want to learn how to install a version of MATLAB on your local system and use it to run jobs on Wulver, please see [Using Local MATLAB on Wulver](matlab_local.md)


