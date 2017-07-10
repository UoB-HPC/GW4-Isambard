Isambard Phase 1 uses [PBS Professional](http://www.pbsworks.com/PBSProduct.aspx?n=PBS-Professional&c=Overview-and-Capabilities) to manage compute resources.

[PBS Pro 13.1 User Guide](http://www.pbsworks.com/pdfs/PBSProUserGuide13.1.pdf)

# Limits

Job submission is limited to two jobs per user per queue

# Queue configuration

* knlq    - To run on the eight single-socket Intel Xeon Phi "Knights Landing" 7210 CPU nodes
* pascalq - To run on the four dual-card Nvidia Tesla P100 "Pascal" GPU nodes
* all     - To run on any node type, not recommended for use

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
