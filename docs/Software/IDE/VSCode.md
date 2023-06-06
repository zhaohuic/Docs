---
title: VS Code
---
Visual Studio Code (often abbreviated as VS Code) is an Integrated Development Environment (IDE). It is a lightweight and highly extensible code editor developed by Microsoft. Although referred to as a code editor, VS Code offers many features. One of the important feature of VS Code is an integrated terminal that allows developers to execute commands, run scripts, and interact with the command-line interface without leaving the editor. VS Code also provides Git integration, enabling developers to manage version control operations, such as committing, branching, and merging, without switching to a separate Git client. 

## Availability
VS Code is not installed on the cluster. To VS Code you need to install it on your computer and connect remotely to the cluster using NJIT VPN.

## Application Information, Documentation
The documentation of VS Code is available at [VS Code documentation](https://code.visualstudio.com/docs). You can download the VS Code from [VS Code download page](https://code.visualstudio.com/Download)

## Using VS Code
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
        #SBATCH --partition=gpu
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
Once you submit the job you will get the port number from the output file generated and open a new terminal and type
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


