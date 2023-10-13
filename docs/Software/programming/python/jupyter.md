# Jupyter Notebooks
The Jupyter Notebook is a web-based interactive computing platform. The notebook combines live code, equations, narrative text, visualizations. In our cluster, we have JupyterLab which is the next-generation user interface for Project Jupyter offering all the familiar building blocks of the classic Jupyter Notebook (notebook, terminal, text editor, file browser, rich outputs, etc.) in a flexible and powerful user interface. 

## Availability

=== "Lochness"

    ```python exec="on"
    import pandas as pd
    
    df = pd.read_csv('docs/assets/tables/module_lochness.csv')
    # Header values to be added
    soft = df.query('Software == "JupyterLab"')
    print(soft.to_markdown(index=False))
    ```


## Using JupyterLab


??? example "Sample Batch Script to run Jupyter Notebook"

    === "Lochness"
    
        ```slurm
        #!/bin/bash -l                                                                                                                                                                                                                          
        #SBATCH --job-name=jupyter_test                                                                                                                                                                                                         
        #SBATCH --output=%x.%j.out                                                                                                                                                                                                              
        #SBATCH --nodes=1                                                                                                                                                                                                                       
        #SBATCH --tasks-per-node=1
        #SBATCH --partition=datasci                                                                                                                                                                                                             
        #SBATCH --gres=gpu:1
        #SBATCH --mem=4G
        #SBATCH --time=0-01:00:00
                                                                                                                                                                                                                                          
        ######################################                                                                                                                                                                                               
        module purge > /dev/null 2>&1
        module load GCCcore/11.2.0 JupyterLab
        port=$(shuf -i 6000-9999 -n 1)
        /usr/bin/ssh -N -f -R $port:localhost:$port login-1.tartan.njit.edu
    
        cat<<EOF
        
        Jupyter server is running on: $(hostname)
        Job starts at: $(date)
        Step 1: Create SSH tunnel
        
        Open new terminal window, and run:
        (If you are off campus you will need VPN running)
        
        ssh -L $port:localhost:$port $USER@login-1.tartan.njit.edu
        
        Step 2: Connect to Jupyter
        
        Keep the terminal in the previouse step open. Now open browser, find the line with
         
        Or copy and paste one of these URLs:
        
        the URL will be something like:
        
        http://localhost:${port}/?token=XXXXXXXX
        
        you should be able to connect to jupyter notebook running remotely on a lochness compute node with above url
        
        EOF
        
        jupyter notebook --no-browser --port $port --notebook-dir=$(pwd)
                     
        ```
Once you submit this job script, you will see an output file indicating port number which you need to use to connect to the HPC cluster in a new terminal window. Please follow further instructions from the output file.

!!! warning 
    
    Please not that JupyterLab or Jupyter Notebook is not availble as module on Wulver, as users can build those packages via Conda. Please see [Conda Documentation](conda.md) for details. Jupyter Notebook can also be accessed on Wulver via [Open OnDemand](https://openondemand.org/). We will provide the instructions soon.


## User Contributed Information

!!! info "Please help us improve this page"

    Users are invited to contribute helpful information and corrections through our [Github repository](https://github.com/arcs-njit-edu/Docs/blob/main/CONTRIBUTING.md).

