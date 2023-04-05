# GNU and Intel Compilers 
We offer both GNU and Intel compilers. Here is the list of compilers you can find on our cluster. 
## Availability

|  Compilers  |  Versions  |          modules           |
|:-----------:|:----------:|:--------------------------:|
|     GNU     |   11.2.0   |        `GCC/10.2.0`        |
|     GNU     |   12.2.0   |        `GCC/12.2.0`        |
|    Intel    |  2021.4.0  | `intel-compilers/2021.4.0` |

# MPI Libraries
MPI (Message Passing Interface) libraries are a set of software tools that allow for parallel computing on distributed memory systems, such as computer clusters. These libraries provide a standardized interface for communication between processes running on different nodes of the cluster. There are several implementations of MPI libraries available, such as OpenMPI, MPICH, and Intel MPI. Currently, the following MPI libraries on our cluster.

|  Compilers  |  Versions  | Compiler Dependency |       module load command          |
|:-----------:|:----------:|:-------------------:|:----------------------------------:|
|   OpenMPI   |   4.1.1    |    `GCC 11.2.0`     |  `module load GCC/11.2.0 OpenMPI`  |
|   OpenMPI   |   4.1.4    |    `GCC 12.2.0`     |  `module load GCC/12.2.0 OpenMPI`  |
|    IMPI     |  2021.4.0  |  `intel 2021.4.0`   | `module load intel-compilers impi` |

