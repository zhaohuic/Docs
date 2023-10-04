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