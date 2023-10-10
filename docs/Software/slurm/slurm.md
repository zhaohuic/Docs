---
title: SLURM
---
Slurm (Simple Linux Utility for Resource Management) is an open-source workload manager and job scheduler designed for high-performance computing clusters. It is widely used in research, academia, and industry to efficiently manage and allocate computing resources such as CPUs, GPUs, memory, and storage for running various types of jobs and tasks. Slurm helps optimize resource utilization, minimizes job conflicts, and provides a flexible framework for distributing workloads across a cluster of machines. It offers features like job prioritization, fair sharing of resources, job dependencies, and real-time monitoring, making it an essential tool for orchestrating complex computational workflows in diverse fields.

## Availability

```python exec="on"
import pandas as pd
# Create a dictionary with data
data = {
    'Software': ['slurm'],
    'Module Load Command': ['`module load wulver`']
}
df = pd.DataFrame(data)
print(df.to_markdown(index=False))
```
## Application Information, Documentation
The documentation of SLURM is available at [SLURM manual](https://slurm.schedmd.com/documentation.html). Please note that the module `wulver` is already loaded when user logs in to the cluster. If you use `module purge` command, make sure to use `module load wulver` in the slurm script to load SLURM. 

## Using SLURM on Cluster
In Wulver, SLURM submission will have new requirements, intended for more fair sharing of resources without impinging on investor/owner rights to computational resources.  All jobs must now be charged to a PI-group account.

1. To specify the job use `--account=PI_ucid`, for example, `--account=doctorx`.  You can specify `--account` as either a `sbatch` or `#SBATCH` parameter
2. Wulver has three partitions, differing in GPUs or RAM available:

```python exec="on"
import pandas as pd 
import numpy as np
df = pd.read_csv('docs/assets/tables/partitions.csv')
# Replace NaN with 'NA'
df.replace(np.nan, 'NA', inplace=True)
print(df.to_markdown(index=False))
```
3. Wulver has three levels of “priority”, utilized under SLURM as Quality of Service (QoS):
```python exec="on"
import pandas as pd 
import numpy as np
df = pd.read_csv('docs/assets/tables/slurm_qos.csv')
# Replace NaN with 'NA'
df.replace(np.nan, 'NA', inplace=True)
print(df.to_markdown(index=False))
```

### Example of slurm script

??? example "Sample Job Script to use: submit.sh"

    ```slurm
        #!/bin/bash -l
        #SBATCH --job-name=job_nme
        #SBATCH --output=%x.%j.out # %x.%j expands to slurm JobName.JobID
        #SBATCH --error=%x.%j.err
        #SBATCH --partition=general
        #SBATCH --qos=standard
        #SBATCH --account=PI_ucid # Replace PI_ucid which the NJIT UCID of PI
        #SBATCH --nodes=1
        #SBATCH --ntasks-per-node=8
        #SBATCH --time=59:00  # D-HH:MM:SS
        #SBATCH --mem-per-cpu=4000M
    ```

Here, the job requests 1 node with 8 cores, on the `general` partition with `qos=standard`. Please note that the memory relies on the number of cores you are requesting. As per the policy, users can request up to 4GB memory per core, therefore the flag  `--mem-per-cpu` is used for memory requirement. In this above script `--time` indicates the wall time which is used to specify the maximum amount of time that a job is allowed to run. The maximum allowable wall time depend on SLURM QoS, which you can find in [QoS](slurm.md#using-slurm-on-cluster)  To submit the job, use `sbatch submit.sh` where the `submit.sh` is the job script. Once the job has been submitted, the jobs will be in the queue, which will be executed based on priority-based scheduling. To check the status of the job use `squeue -u UCID` (replace `UCID` with your NJIT UCID) and you should see the following 
```bash
  JOBID PARTITION     NAME     USER  ST    TIME    NODES  NODELIST(REASON)
   635   general     job_nme   ucid   R   00:02:19    1      n0088
```
Here, the `ST` stands for the status of the job. You may see the status of the job `ST` as `PD` which means the job is pending and has not been assigned yet. The status change depends upon the number of users using the partition and resources requested in the job. Once the job starts, you will see the output file with an extension of `.out`. If the job causes any errors, you can check the details of the error in the file with `.err` extension.

In case of submitting the on GPU, you can use the following the SLURM script 

??? example "Sample Job Script to use: gpu_submit.sh"

    ```slurm
        #!/bin/bash -l
        #SBATCH --job-name=gpu_job
        #SBATCH --output=%x.%j.out # %x.%j expands to slurm JobName.JobID
        #SBATCH --error=%x.%j.err
        #SBATCH --partition=gpu
        #SBATCH --qos=standard
        #SBATCH --account=PI_ucid # Replace PI_ucid which the NJIT UCID of PI
        #SBATCH --nodes=1
        #SBATCH --ntasks-per-node=8
        #SBATCH --gres=gpu:2
        #SBATCH --time=59:00  # D-HH:MM:SS
        #SBATCH --mem-per-cpu=4000M
    ```
This will request 2 GPUS per node on the `GPU` partition.

### Interactive session on a compute node

 Interactive sessions are useful for tasks that require direct interaction with the compute node's resources and software environment. To start an interactive session on the compute node, use the following after logging into Wulver
 ```bash
    srun -p general -n 1 --ntasks-per-node=8 --qos=standard --account=PI_ucid --mem-per-cpu=2G --time=59:00 --pty bash
 ```
To start an interactive session on GPU, use the following command

 ```bash
    srun -p gpu -n 1 --ntasks-per-node=8 --qos=standard --account=PI_ucid --mem-per-cpu=2G --gres=gpu:2 --time=59:00 --pty bash
 ```
Replace `PI_ucid` with PI's NJIT UCID. 

!!! note
       
        Please note that if you are using GPUs, check that whether your script is parallelized. If your script is not prallelized and oonly depends on GPU, then you don't need to request more cores per node unless you require the memory. In that case use `--ntasks-per-node=1`.
