# Access to Wulver
Wulver is a new cluster which will be onlne on July 15th, 2023. To see the specifications of Wulver cluster please see the [Wulver Documentation](wulver.md). 

## Login to Wulver
If you already have access to existing clusters such as Lochness, you can log in to Wulver using `ssh ucid@login01.tartan.njit.edu`. Replace `ucid` with your UCID. If you don't have prior access to NJIT cluster, you need to request for access.
Faculty can obtain a login to NJIT's HPC & BD systems by sending an email to [hpc@njit.edu](mailto:hpc@njit.edu). Students can obtain a login either by taking a class that uses one of the systems or by asking their faculty adviser to [contact](mailto:hpc@njit.edu) on their behalf. Your login and password are the same as for any NJIT AFS system.
Please see the documentation on [cluster access](cluster_access.md) for details.

## General Linux Commands
In the table below, you can find the basic linux commands required to use the cluster. For more details on linux commands, please see the [Linux commands cheat sheets](https://www.linuxtrainingacademy.com/linux-commands-cheat-sheet).

```python exec="on"
import pandas as pd

df = pd.read_csv('docs/assets/tables/commands.csv')
#soft = df.query('Software == "fluent" | Software == "ANSYS"')
print(df.to_markdown(index=False))
```

## Slurm Configuration

```slurm
#!/bin/bash -l
#SBATCH --job-name=job_nme
#SBATCH --output=%x.%j.out # %x.%j expands to slurm JobName.JobID
#SBATCH --error=%x.%j.err
#SBATCH --partition=defq
#SBATCH --qos=standard
#SBATCH --nodes=1
#SBATCH --ntasks-per-node=8
#SBATCH --time=59:00  # D-HH:MM:SS
#SBATCH --mem=4G
```
Please note that default and Max Memory per CPU at 4GB/Core
QOS
* Low is preemptable by Standard, High
* Low, Standard have maximum 3 Day Walltime
* High has maximum 14 Day Walltime
* Multifactor Priority Enabled – Low, Standard, High have Priority 10, 30, 50 respectively
