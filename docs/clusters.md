# Clusters

NJIT Cluster offers three different clusters listed below.

## Wulver

Wulver is a new cluster anticipated to come on line 1Q 2023.

### Specifications:

* 100 x Dell R6525 CPU Nodes
* 2 x AMD 7753 2.45 GHz, 64C128T - Total cores: 12,800
* Memory 512 GB/node - Total memory: 51.2 TB
* Theoretical Performance: 501.760TFlops
* 2 x Dell R6525 High Memory Nodes
* 2 x AMD 7753 2.45 GHz, 64C128T - 256 Total Cores
* Memory - 2 TB/node - Total Memory 4TB
* Theoretical Performance: 10.035TFlops
* 25 x Dell XE8545 GPU Nodes
* 2 x AMD EPYC 7713 2.0GHz,64C/128T - Total cores: 3200 
* Memory 512 GB/node - Total memory: 1 TB
* 4 x NVIDIA HGX A100 - 4x A100 SXM4 80GB - total GPUs: 100
* Theoretical Performance: 102.4TFlops (cpu) + 970TFlops (gpu)
* Totals 127 Nodes, 16,256 Cores, 56.2 TB RAM
* Theoretical Performance: 1.584PFlops
* 100 GB High throughput/low latency Infiniband network
* Arcastream Storage
* Parallel filesystem allowing multiple read/write operations
* Max performance 20 GB/s
* Hierarchical storage; NVME scratch, SAS, Cloud
* User transparent transfer from high-speed to medium to archive storage
* 1 PB total storage
* Virtualized Support and login nodes
* Management and deployment overseen by NJIT:
* Nvidia Bright Cluster Manager
* X-ISS system administration
* SLURM scheduler with full support
* InfiniBand support via Dell or directly from Mellanox
* Will be deployed in the Databank data center in Piscataway

## Lochness

This very heterogeneous cluster is a mix of manufacturers, components, and capacities as it was built up in incremental purchases spanning several years. Much of lochness will be incorporated into the new Wulver cluster 3Q 2023.

### Specifications:

* Total Nodes: 224 including GPU nodes
* Total Cores: 28236
* Total GB RAM: 66738104 (mostly 385GB per node but some with as little as 32GB)
* GPU nodes: 28 
* Total GPUs: 64
* Fifteen different GPU models deployed:
* 8x  nodes w/ 2x P100 GPU(s)
* 4x  nodes w/ 2x A100 GPU(s)
* 3x  nodes w/ 4x TitanRtx GPU(s)
* 2x  nodes w/ 2x K20Xm GPU(s)
* 11x nodes with 1x or 2x other models of Nvidia GPUs
* Seventeen different CPU models deployed:
* 52x Intel(R) Xeon(R) Gold 6226R CPU @ 2.90GHz
* 40x Intel(R) Xeon(R) CPU E5-2630 v4 @ 2.20GHz
* 20x Intel(R) Xeon(R) Silver 4216 CPU @ 2.10GHz
* 20x Intel(R) Xeon(R) Silver 4214 CPU @ 2.20GHz
* 15x Intel(R) Xeon(R) Gold 6230 CPU @ 2.10GHz
* 11x Intel(R) Xeon(R) Gold 6240R CPU @ 2.40GHz
* 29x nodes with 1x to 4x eleven other CPU models
* All nodes have:
    * Ethernet network interface (1GigE or 10GigE)
    * Infiniband network interface (mix of HDR100, EDR, and FDR speeds)
    * 1TB local storage (mostly SSD but a few HD)
* All nodes have network accessible storage:
    * /home/: 26 TB
    * /research/: 97 TB
    * /afs/cad/ 50 TB 

The cluster also features

* "CentOS Linux 7 (Core)" operating system
* Virtualized login and control nodes
* SLURM job scheduler
* Warewulf stateless node provisioning
* Managed entirely by NJIT personnel

Roughly half under warranty; rest are time and materials

## Stheno

### Specifications

* GPU nodes: 2
* Total GPUs: 4
* GPU models:
  * 2x  node(s) w/ 2x K20m GPU(s)
* Total Nodes: 22
* Total Cores: 1224
* Total GB RAM: 2481667
* Nodes:  GB:
    * 15x     128
    * 7x      96
* Processor models:
    * 15x Intel(R) Xeon(R) CPU E5-2630 0 @ 2.30GHz
    * 7x Intel(R) Xeon(R) CPU E5649  @ 2.53GHz

Not included are 10 nodes permanently taken out of service due to hardware failures.  All are out of warranty and EOL’d by manufacturers.