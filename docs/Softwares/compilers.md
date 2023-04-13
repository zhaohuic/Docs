## GNU and Intel Compilers 
We offer both GNU and Intel compilers. Here is the list of compilers you can find on our cluster.
```python exec="on"
import pandas as pd

df = pd.read_csv('docs/assets/tables/module.csv')
# Header values to be added
#column_names=["Compilers","modules"]
soft = df.query('Software == "GCC" | Software == "intel-compilers"')
#soft.columns = column_names
print(soft.to_markdown(index=False))
```

|  Compilers  |  Versions  |          modules           |
|:-----------:|:----------:|:--------------------------:|
|     GNU     |   11.2.0   |        `GCC/11.2.0`        |
|     GNU     |   12.2.0   |        `GCC/12.2.0`        |
|    Intel    |  2021.4.0  | `intel-compilers/2021.4.0` |

## MPI Libraries
MPI (Message Passing Interface) libraries are a set of software tools that allow for parallel computing on distributed memory systems, such as computer clusters. These libraries provide a standardized interface for communication between processes running on different nodes of the cluster. There are several implementations of MPI libraries available, such as OpenMPI, MPICH, and Intel MPI. Currently, the following MPI libraries on our cluster.

```python exec="on"
import pandas as pd

df = pd.read_csv('docs/assets/tables/module.csv')
# Header values to be added
#column_names=["MPI","modules"]
soft = df.query('Software == "OpenMPI" | Software == "impi"')
#soft.columns = column_names
print(soft.to_markdown(index=False))
```

## Toolchains

### Free Open Source Software (foss)

```python exec="on"
import pandas as pd

df = pd.read_csv('docs/assets/tables/module.csv')
# Header values to be added
#column_names=["Toolchains","modules"]
soft = df.query('Software == "foss"')
#soft.columns = column_names
print(soft.to_markdown(index=False))
```
### Intel

```python exec="on"
import pandas as pd

df = pd.read_csv('docs/assets/tables/module.csv')
# Header values to be added
#column_names=["Toolchains","modules"]
soft = df.query('Software == "intel"')
#soft.columns = column_names
print(soft.to_markdown(index=False))
```