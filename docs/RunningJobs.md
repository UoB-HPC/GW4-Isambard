Isambard Phase 1 uses [PBS Professional](http://www.pbsworks.com/PBSProduct.aspx?n=PBS-Professional&c=Overview-and-Capabilities) to manage compute resources.

[PBS Pro 13.1 User Guide](http://www.pbsworks.com/pdfs/PBSProUserGuide13.1.pdf)

# Queue configuration

TODO: Write this once queue configuration has been finalized

To see the available queues and their current state:

    qstat -q

# Running a batch job

TODO: Add details of how to write and submit batch job script

# Running an interactive job

Passing the `-I` flag to `qsub` allows a compute node to be used interactively.
For example, to request an interactive job on one of the Broadwell nodes, use the following command:

    qsub -I -q pascalq -l nodes=1:ncpus=36
