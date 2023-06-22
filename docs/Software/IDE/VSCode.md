---
title: VS Code
---
Visual Studio Code (often abbreviated as VS Code) is an Integrated Development Environment (IDE). It is a lightweight and highly extensible code editor developed by Microsoft. Although referred to as a code editor, VS Code offers many features. One of the important feature of VS Code is an integrated terminal that allows developers to execute commands, run scripts, and interact with the command-line interface without leaving the editor. VS Code also provides Git integration, enabling developers to manage version control operations, such as committing, branching, and merging, without switching to a separate Git client. 

## Availability
VS Code is not installed on the cluster. To use VS Code, you need to install it on your computer and connect remotely to the cluster using NJIT VPN.

## Application Information, Documentation
The documentation of VS Code is available at [VS Code documentation](https://code.visualstudio.com/docs). You can download the VS Code from [VS Code download page](https://code.visualstudio.com/Download)

## Using VS Code

!!! warning

        If you want to use VS Code on NJIT cluster, don't use VS Code installed on your machine to connect to cluster! Please use the method described belelow so that you can use VS Code not only to edit scripts, but also run your script on the cluster.

Use the following slurm script 
To use VS Code on NJIT cluster, you need to install VS Code extension [Remote-SSH](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-ssh). You can do so directly within VS Code: Use the top-menu bar and navigate to <kbd>File</kbd>-><kbd>Preferences</kbd>-><kbd>Extensions</kbd>. Then search for Remote-SSH and install.
The Remote-SSH extension allows you to connect to a NJIT cluster directly from your local machine. Once the extension is installed, the bottom-left of your VS Code application will show a green box (<kbd>Open a Remote Window</kbd>). Clicking on it opens a dropdown menu (see the video below), where you should select <kbd>Configure SSH Hosts</kbd>. You will see a config file where you can specify the address of the cluster (HostName) as well as your username and store them under a convenient name. See the below snippet for the entries in Lochness cluster.
```
Host lochness
  HostName lochness.njit.edu
  User ucid
```
Replace `ucid` with your NJIT userid. Now you can log in to `lochness` host.  

<video controls style="max-width: 500px;">
  <source src="../../../assets/images/vscode.mov" controls>
  Your browser does not support the video tag.
</video>

!!! note

        Once you select the host to connect to NJIT cluster, you willl be required to enter the password which is same as your NJIT UCID password. To avoid authenticaltion for password everytime you connect to the host please follow  [Passwordless Authentication](cluster_access.md#passwordless-authentication-to-the-njit-cluster).

!!! warning

        Don't run computations in VS Code! Use VS Code only to edit scripts, use linting, etc on the head node. If you intend to run your script, use either use Slurm or connect to compute node via VS Code.

### Using VS Code on Compute Nodes
The head node is mainly suitable for editing scripts. Since the resources of the head node are shared across all users, it is not good practice to use it for any coding sessions that require more computing power. To use compute node with VS Code, you need to request an interactive session on a computing node which can be done via Slurm. 
On the login terminal, use the following command 
```bash
# Start an interactive session with 4 cores and 32G memory on low_priority partition
srun --partition=low_priority --cpus-per-task=4 --mem-per-cpu=8G --partition=gpu --pty bash
```
Users can use their PI's partition, if they have access to it.

Unlike the head node of the computing cluster, to which you can connect directly via SSH, the compute nodes of the cluster don’t have a direct connection. For VS Code to connect to a computing node, it’s therefore necessary to connect through the head node. This is done via a proxy connection.

First, check the exact name of the compute node that you have requested. You can check the node number once you are connected to the compute node as shown below. 

```bash
node803-41 ~ >:
```

Next, open the `config` again as mentioned in [Using VS Code](VSCode.md#using-vs-code). 
Here, `HostName` is the name of the compute node (which may change across sessions) and `ProxyJump` specifies the address of the head node. Note, that the `lochness` host is already defined in the config file mentioned in [Using VS Code](VSCode.md#using-vs-code) section.

```ssh
Host lochness_compute
  HostName node803
  ProxyJump lochness
  User ucid
```
Replace `ucid` with your NJIT userid.

!!! note

        You need to change the `Hostname` everytime you submit the request an interactive session in compute node, since you will be assigned a different node number.

Now, start a new VS Code session and connect to a remote host via the Remote-SSH extension as before. Select the address of the newly specified host (in the example case shown above, it's `lochness_compute`) and wait for the connection to establish.
## Related Applications

* PyCharm

## User Contributed Information

!!! info "Please help us improve this page"
        Users are invited to contribute helpful information and corrections
        through our [Github repository](https://github.com/arcs-njit-edu/Docs/blob/main/CONTRIBUTING.md).


