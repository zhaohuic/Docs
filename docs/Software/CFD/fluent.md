---
title: FLUENT
---


## Availability

```python exec="on"
import pandas as pd

df = pd.read_csv('docs/assets/tables/module.csv')
soft = df.query('Software == "fluent" | Software == "ANSYS"')
print(soft.to_markdown(index=False))
```
## Using Fluent
To use Fluent on cluster, Users need to prepare the case using ANSYS on their local machine first. Please [download](https://njit.instructure.com/courses/8519/assignments/128626) ANSYS and follow the [instructions](https://ist.njit.edu/ansys-installation-instructions) to install ANSYS on your local machine.
Once you install ANSYS on local machine, prepare the fluent case (meshing, setting boundary conditions) and save the case and data in `.cas` and `.dat` format respectively. 
If you are running transient problem and want to save the data at particular timestep or time interval, please see the steps below.

* ![fluent_data1](../../assets/images/fluent_1.png){ width=50% height=50%}
* ![fluent_data2](../../assets/images/fluent_2.png){ width=80% height=80%}

??? example "Sample Batch Script to Run FLUENT : fluent.submit.sh"

    ```slurm
        #!/bin/bash -l
        #SBATCH --job-name=fluent
        #SBATCH --output=%x.%j.out # i%x.%j expands to slurm JobName.JobID
        #SBATCH --ntasks=8
        # Use "sinfo" to see what partitions are available to you
        #SBATCH --partition=regular
        
        # Memory required; lower amount gets scheduling priority
        #SBATCH --mem-per-cpu=5G
        
        # Time required in d-hh:mm:ss format; lower time gets scheduling priority
        #SBATCH --time=5-24:59:00
        
        # Purge and load the correct modules
        module purge > /dev/null 2>&1
        module load ANSYS
        
        # Run the mpi program
        
        machines=hosts.$SLURM_JOB_ID
        touch $machines
        for node in `scontrol show hostnames`
            do
                echo "$node"  >> $machines
            done
        
        fluent 3ddp -affinity=off -ssh -t$SLURM_NTASKS -pib -mpi=intel -cnf="$machines" -g -i journal.JOU
    ```

## Related Applications

* [OpenFOAM](openfoam.md)

## User Contributed Information

!!! info "Please help us improve this page"
        Users are invited to contribute helpful information and corrections
        through our [Github repository](https://github.com/arcs-njit-edu/Docs/blob/main/CONTRIBUTING.md).


