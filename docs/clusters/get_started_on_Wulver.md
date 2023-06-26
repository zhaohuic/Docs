# Access to Wulver
Wulver is a new cluster which will be onlne on July 15th, 2023. To see the specifications of Wulver cluster please see the [Wulver Documentation](wulver.md). 

## Login to Wulver
If you already have access to existing clusters such as Lochness, you can login to Wulver by 
`ssh ucid@login01.tartan.njit.edu`. Replace `ucid` with your UCID. If you don't have prior access to NJIT cluster, you need to request for access.
Faculty can obtain a login to NJIT's HPC & BD systems by sending an email to [hpc@njit.edu](mailto:hpc@njit.edu). Students can obtain a login either by taking a class that uses one of the systems or by asking their faculty adviser to [contact](mailto:hpc@njit.edu) on their behalf. Your login and password are the same as for any NJIT AFS system.
Please see the documentation on [cluser access](cluster_access.md) for details.

## General Linux Commands
In the table below, you can find the basic linux commands required to use the cluster. For more details on linux commands, please see the [Linux commands cheat sheets](https://www.linuxtrainingacademy.com/linux-commands-cheat-sheet).

```python exec="on"
import pandas as pd

df = pd.read_csv('docs/assets/tables/commands.csv')
#soft = df.query('Software == "fluent" | Software == "ANSYS"')
print(df.to_markdown(index=False))
```
