---
title: Paraview
---
ParaView is an open-source, cross-platform data visualization and analysis tool that allows users to create visualizations and analyze large datasets. It was developed to process and visualize scientific and engineering data, such as computational fluid dynamics (CFD) simulations, seismic data, medical imaging, and climate data.

ParaView provides a graphical user interface (GUI) that enables users to interactively explore and visualize data. It supports a wide range of data formats and allows users to customize and manipulate visualizations to suit their needs. Additionally, ParaView provides a scripting interface that allows users to automate repetitive tasks and create custom analysis pipelines.

ParaView is widely used in a variety of scientific and engineering fields, including aerospace, automotive, biomedical, energy, and geosciences, among others. It is actively developed and maintained by [Kitware](https://www.kitware.com), a software company that specializes in open-source solutions for scientific computing and data analysis.

## Availability

```python exec="on"
import pandas as pd

df = pd.read_csv('docs/assets/tables/module.csv')
soft = df.query('Software == "ParaView"')
print(soft.to_markdown(index=False))
```
## Application Information, Documentation
The documentation of ParaView is available at [ParaView manual](https://docs.paraview.org/en/latest/index.html). To use the ParaView on cluster, users need to use the same version of ParaView on their local machine. You can download the ParaView from [ParaView official download page](https://www.paraview.org/download)

## Using ParaView
ParaView supports GPU acceleration, which can significantly improve performance and reduce processing times for certain types of data and operations. GPU acceleration is particularly useful for large datasets with many points or cells, as well as for operations such as volume rendering and streamlines.
You can use ParaView with GPU acceleration, but you need to use GPU nodes on our cluster. ParaView is also designed to work in parallel environments, and it supports the Message Passing Interface (MPI) standard for distributed computing. With MPI support, ParaView can be used to visualize and analyze large-scale datasets on cluster. 

??? example "Sample Batch Script to Run ParaView with MPI support: pvserver_cpu.submit.sh"

	```slurm
	#!/bin/bash -l
	#SBATCH --job-name=pvserver_cpu
    #SBATCH --output=%x.%j.out # %x.%j expands to slurm JobName.JobID
    #SBATCH --partition=regular
    #SBATCH --nodes=1
    #SBATCH --ntasks-per-node=32
    #SBATCH --mem-per-cpu=0 # Adjust as necessary
    #SBATCH --time=24:00:00  # D-HH:MM:SS
    ################################################
    #
    # Purge and load modules needed for run
    #
    ################################################
    module purge
    module load ParaView/osmesa/5.9.1
    ################################################
    #
    # Open an ssh tunnel to the login node
    #
    ################################################
    # Run on random port
    port=$(shuf -i 6000-9999 -n 1)
    HOST=$(hostname)
	if [ $(hostname) == $HOST ]; then
		/usr/bin/ssh -N -f -R $port:localhost:$port login-1.tartan.njit.edu
	fi
	################################################
	cat<<EOF

	pvserver is running on: $(hostname)
	Job starts at: $(date)
	
	Step 1: Create SSH tunnel
	
	Open new terminal window, and run:
	(If you are off campus you will need VPN running)
	
	ssh -L $port:localhost:$port $USER@login-1.tartan.njit.edu
	EOF
	################################################
	# Run MPI pvserver
	#
	################################################
	mpiexec -rmk slurm pvserver --server-port=$port --force-offscreen-rendering
	```
To use ParaView with GPU you need to following job script

??? example "Sample Batch Script to Run ParaView with GPU support: pvserver_gpu.submit.sh"

	```slurm
	#!/bin/bash -l
	#SBATCH --job-name=pvserver_test
	#SBATCH --output=%x.%j.out # %x.%j expands to slurm JobName.JobID
	#SBATCH --partition=gpu # Modify the partion name to PI's partition, otherwise use datasci
	#SBATCH --nodes=1
	#SBATCH --ntasks-per-node=1
	#SBATCH --gres=gpu:1
	#SBATCH --mem-per-cpu=0 # Adjust as necessary
	#SBATCH --time=24:00:00  # D-HH:MM:SS
	################################################
	#
	# Purge and load modules needed for run
	#
	################################################
	module purge
	module load ParaView/egl/5.9.1
	################################################
	#
	# Open an ssh tunnel to the login node
	#
	################################################
	port=$(shuf -i 6000-9999 -n 1)
	HOST=$(hostname)
	if [ $(hostname) == $HOST ]; then
			/usr/bin/ssh -N -f -R $port:localhost:$port login-1.tartan.njit.edu
	fi
	################################################
	cat<<EOF
	
	pvserver is running on: $(hostname)
	Job starts at: $(date)
	
	Step 1: Create SSH tunnel
	
	Open new terminal window, and run:
	(If you are off campus you will need VPN running)
	
	ssh -L $port:localhost:$port $USER@login-1.tartan.njit.edu
	EOF
	################################################
	#
	# Run MPI pvserver
	#
	################################################

	mpiexec -rmk slurm pvserver --server-port=$port --force-offscreen-rendering --displays=0,1
	```
Submit the job script using the sbatch command: `sbatch pvserver_gpu.submit.sh` or `sbatch pvserver_cpu.submit.sh`.
Once you submit the job, please open the output file with `.out` extension, and get the port number from the output file. Next, open a new terminal and type
`ssh -L $port:localhost:$port $USER@login-1.tartan.njit.edu`, where `$port` corresponds to the port number.
Once you open ParaView from you local machine go to `File --> Connnect`, and you will see a dialogue box with a name `Choose Server Configuration`. You need select <kbd>Add Server</kbd> option and there you need use the following as shown below.

<video src="../../../assets/images/ParaView-add-connection.mp4" controls>
  Your browser does not support the video tag.
</video>

Once you add the server, you can need to select <kbd>Connect</kbd> to connect ParaView to the cluster.

!!! note

		The port number may change everytime you submit job. In that case you need to modifiy the port number by sleecting the <kbd>Edit Server</kbd> option. The step to modify the server is shown in the above tutorial.
## Related Applications

* Tecplot

## User Contributed Information

!!! info "Please help us improve this page"
		Users are invited to contribute helpful information and corrections
		through our [Github repository](https://github.com/arcs-njit-edu/Docs/blob/main/CONTRIBUTING.md).


