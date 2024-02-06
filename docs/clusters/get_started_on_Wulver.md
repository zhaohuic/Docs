# Access to Wulver
Wulver is a new cluster which will be available by the end of 2023. To see the specifications of Wulver cluster, please see the [Wulver Documentation](wulver.md).
If you already have access to existing clusters such as Lochness, you can log in to Wulver using `ssh ucid@wulver.njit.edu`. Replace `ucid` with your UCID. If you don't have prior access to NJIT cluster, you need to request for access.
Faculty can obtain a login to NJIT's HPC & BD systems by sending an email to [hpc@njit.edu](mailto:hpc@njit.edu). Students can obtain a login either by taking a class that uses one of the systems or by asking their faculty adviser to [contact](mailto:hpc@njit.edu) on their behalf. Your login and password are the same as for any NJIT AFS system.

## Login to Wulver
Please see the documentation on [cluster access](cluster_access.md) for details.

## General Linux Commands
Since the operating system (OS) HPC cluster is linux based RHEL 8, users need to know linux to use the cluster.
In the table below, you can find the basic linux commands required to use the cluster. For more details on linux commands, please see the [Linux commands cheat sheets](https://www.linuxtrainingacademy.com/linux-commands-cheat-sheet).

```python exec="on"
import pandas as pd

df = pd.read_csv('docs/assets/tables/commands.csv')
print(df.to_markdown(index=False))
```

## Wulver Filesystems

See [Wulver Filesystems](Wulver_filesystems.md) for details.

## Software Availability
The software can be loaded via `module load` command. You see the following modules are loaded once you log in to the Wulver (Use the `module li`) command to see the modules. 
```bash
   1) easybuild   2) slurm/wulver   3) null
```

## Slurm Configuration

Please see [SLURM](slurm.md) for details in the slurm configuration.  
