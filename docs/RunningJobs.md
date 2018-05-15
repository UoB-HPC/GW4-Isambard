Isambard Phase 1 uses the PBS Pro schedular to manage compute resources.

[PBS Pro 13.1 User Guide](http://www.pbsworks.com/pdfs/PBSProUserGuide13.1.pdf)

# Limits

Job submission is limited to two jobs per user per queue

# Queue configuration

* knlq    - To run on the eight single-socket Intel Xeon Phi "Knights Landing" 7210 CPU nodes
* pascalq - To run on the four dual-card Nvidia Tesla P100 "Pascal" GPU nodes
* all     - To run on any node type, not recommended for use

KNLq is split into two sets of MCDRAM configuration, nodes 001-004 are in cache memory mode (quad_0) and nodes 005-008 are in flat memory mode (quad_100). These modes can be targeted using the `aoe=` PBS attribute.

To see the available queues and their current state:

    qstat -q

# Running a batch job

## Example
<pre>
#!/bin/bash
#PBS -q pascalq
#PBS -l nodes=1
#PBS -l walltime=00:10:00

cd "$PBS_O_WORKDIR"
...
</pre>

# Running an interactive job

Passing the `-I` flag to `qsub` allows a compute node to be used interactively.

For example, to request an interactive job on one of the Pascal nodes utilizing 1 GPU and 16 of the 36 available Broadwell CPU cores, use the following command:

    qsub -I -q pascalq -l nodes=1:ncpus=16:ngpus=1

# Specifying correct resources

To avoid blocking resources which aren't being used by your job, it is important to specify the correct amount of resources in your job script.

For example, this command declares that your job will run on a single node and will use one of the two available GPUs. The omission of the `ncpus` attribute causes it to default to `1`, meaning other jobs can enter the system to use any of the remaining 35 Broadwell CPU cores and the unused GPU.

    qsub -I -q pascalq -l nodes=1:ngpus=1

If you request `ngpus=2`, then any subsequently submitted job requesting a GPU will not run on the same node until a node is freed. Similarly setting `ncpus=36` will block any jobs requiring a CPU from running; Remember, 18 of the 36 cores are Hyperthreads.

# Load CUDA Toolkit on Pascal nodes
To load the default version of CUDA run:

    module load cudatoolkit

Specific versions can be found with:

    module avail cudatoolkit
