---
title: SLURM
---
Slurm (Simple Linux Utility for Resource Management) is an open-source workload manager and job scheduler designed for high-performance computing clusters. It is widely used in research, academia, and industry to efficiently manage and allocate computing resources such as CPUs, GPUs, memory, and storage for running various types of jobs and tasks. Slurm helps optimize resource utilization, minimizes job conflicts, and provides a flexible framework for distributing workloads across a cluster of machines. It offers features like job prioritization, fair sharing of resources, job dependencies, and real-time monitoring, making it an essential tool for orchestrating complex computational workflows in diverse fields.

## Availability

```python exec="on"
import pandas as pd

df = pd.read_csv('docs/assets/tables/module.csv')
soft = df.query('Software == "slurm"')
print(soft.to_markdown(index=False))
```
## Application Information, Documentation
The documentation of ParaView is available at [SLURM manual](https://slurm.schedmd.com/documentation.html). To use the ParaView on cluster, users need to use the same version of ParaView on their local machine. You can download the ParaView from [ParaView official download page](https://www.paraview.org/download)