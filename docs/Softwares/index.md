# Software Environment
All software and numerical libraries available at the cluster can be found at `/opt/site/easybuild/software/`. The list of software and libraries installed on Lochness can be accessed by using the following command
```
module av
```
!!! note

    Add the following in `.modules` file located in `$HOME` directory
    ```
    module use /opt/site/easybuild/modules/all/MPI
    module use /opt/site/easybuild/modules/all/Core
    module use /opt/site/easybuild/modules/all/Compiler
    ```
If you could not find software or libraries on HPC cluster, please contact us at [hpc@njit.edu](mailto:hpc@njit.edu) to get it installed.

You can check specific packages and list of their versions using `module av`. For example, the list of different versions of Python installed on cluster cna be checked by using,
```
module av Python

```
The above command gives the following output
```
------------------------------------------------------------------------------------------------------------------- /opt/site/easybuild/modules/all/Compiler -------------------------------------------------------------------------------------------------------------------
   GCCcore/10.2.0/Python/2.7.18             GCCcore/11.2.0/IPython/7.26.0                GCCcore/8.3.0/Meson/0.51.2-Python-3.7.4           GCCcore/9.3.0/Flask/1.1.2-Python-3.8.2                         GCCcore/9.3.0/archspec/0.1.0-Python-3.8.2
   GCCcore/10.2.0/Python/3.8.6       (D)    GCCcore/11.2.0/Python/2.7.18-bare            GCCcore/8.3.0/Meson/0.59.1-Python-3.7.4    (D)    GCCcore/9.3.0/GObject-Introspection/1.64.0-Python-3.8.2        GCCcore/9.3.0/pkgconfig/1.5.1-Python-3.8.2
   GCCcore/10.3.0/Python/2.7.18-bare        GCCcore/11.2.0/Python/3.9.6-bare             GCCcore/8.3.0/Python/2.7.16                       GCCcore/9.3.0/Meson/0.55.1-Python-3.8.2                        GCCcore/9.3.0/pybind11/2.4.3-Python-3.8.2
   GCCcore/10.3.0/Python/3.9.5-bare         GCCcore/11.2.0/Python/3.9.6           (D)    GCCcore/8.3.0/Python/3.7.4                 (D)    GCCcore/9.3.0/Python/2.7.18
   GCCcore/10.3.0/Python/3.9.5       (D)    GCCcore/11.2.0/protobuf-python/3.17.3        GCCcore/8.3.0/pkgconfig/1.5.1-Python-3.7.4        GCCcore/9.3.0/Python/3.8.2                              (D)
```

To see how to load the modules (for example `Python/3.9.6`) the following command needs to used.
```
module spider Python/3.9.6
```
This will show the which prerequisite modules need to loaded prior to loading `Python`

```
----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  Python: Python/3.9.6
----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
    Description:
      Python is a programming language that lets you work more quickly and integrate your systems more effectively.


    You will need to load all module(s) on any one of the lines below before the "Python/3.9.6" module is available to load.

      Core/GCCcore/.11.2.0
      GCCcore/.11.2.0

    Help:

      Description
      ===========
      Python is a programming language that lets you work more quickly and integrate your systems
       more effectively.


      More information
      ================
       - Homepage: https://python.org/
```
As shown in the above output, user needs to load `GCCcore/.11.2.0` module first before loading the Python module is available to load. To use `Python 3.9.6`, use the following command
```
module load GCCcore/.11.2.0 Python
```
You can verify whether Python is loaded using,

```
module li
```
and this will result is the following output
```
Currently Loaded Modules:
  1) GCCcore/.11.2.0 (H)   3) binutils/.2.37 (H)   5) ncurses/.6.2     (H)   7) Tcl/8.6.11    9) XZ/.5.2.5  (H)  11) libffi/.3.4.2 (H)  13) Python/3.9.6
  2) zlib/.1.2.11    (H)   4) bzip2/.1.0.8   (H)   6) libreadline/.8.1 (H)   8) SQLite/3.36  10) GMP/.6.2.1 (H)  12) OpenSSL/.1.1  (H)

  Where:
   H:  Hidden Module
```


