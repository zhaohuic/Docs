# Compilers and Toolchains
## GNU and Intel Compilers 
We offer both GNU and Intel compilers. Here is the list of compilers you can find on our cluster.
```python exec="on"
import pandas as pd

df = pd.read_csv('docs/assets/tables/module.csv')
# Header values to be added
#column_names=["Compilers","modules"]
soft = df.query('Software == "GCC" | Software == "intel-compilers"')
soft = soft[~soft.apply(lambda row: row.astype(str).str.contains('system').any(), axis=1)]
print(soft.to_markdown(index=False))
```

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