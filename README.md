This suite of programs for calculating solutions to the n-body problem relies on the <mpi.h> library. If after following the below compilation instructions, the MPI library header or methods flag errors for missing packages, you may need to install additional development packages or need to direct your compiler to where its stored.

In each program, the n-body solver will typically use the parameters provided during the run script in the following simplified process:
    generate initial conditions
        if <g>
            generate randomnly
        if <i>
            take initial conditions from user
    for each timestep t in <number of timesteps> {
        for each particle p in <number of particles>
            compute force on p over <size of timestep> induced by all other particles in <number of particles>
        for each particle p in <number of particles>
            update velocity and position of p
        if <output frequency> is equal to current timestep in <number of timesteps>
           Output new positions and velocities
        }
 
* NON-MPI METHODS *

* nbody_basic.c *
This program requires the additional file of timer.h to compile and run properly.

COMPILING:
gcc -g -Wall -o nbody_basic nbody_basic.c -lm

The user can define COMPUTE_ENERGY to have the program print total potential energy, total kinetic energy and total energy at the end of each timestep. This can be done as follows:

gcc -g -Wall -DCOMPUTE_ENERGY -o nbody_basic nbody_basic.c -lm

Running: ./nbody_basic <number of particles> <number of timesteps> <size of timestep> <output frequency> <g|i>

* MPI-BASED METHODS *

For all methods except nbody_basic.c, an additional parameter is used of <number of processes>. This resembles a number of cpu cores to portion the workload of the nbody problem across. The core nbody code will be simultaneously run on all cores, for a portion of the problem equal to <number of particles>/<number of processes>. For all methods with a <number of processes> parameter, <number of particles> but be evenly divisible by it. Otherwise, the code may produce incorrect final results.

* mpi_nbody_basic.c *

COMPILING:
mpicc -g -Wall -o mpi_nbody_basic mpi_nbody_basic.c -lm

The user can define NO_OUTPUT if they wish to run the program without any printed outputs in the terminal. This can be done as follows:

mpicc -g -Wall -DNO_OUTPUT -o mpi_nbody_basic mpi_nbody_basic.c -lm

This user can define DEBUG if they wish to recieve step by step outputs to the terminal to help identify how values are being handled in between timesteps for troubleshooting purposes. This can be done as follows:

mpicc -g -Wall -DDEBUG -o mpi_nbody_basic mpi_nbody_basic.c -lm

RUNNING:
mpiexec -n <number of processes> ./mpi_nbody_basic <number of particles> <number of timesteps>  <size of timestep> <output frequency> <g|i>

* part1a.c *

COMPILING:
mpicc -g -Wall -o part1a part1a.c -lm

The user can define NO_OUTPUT if they wish to run the program without any printed outputs in the terminal. This can be done as follows:

mpicc -g -Wall -DNO_OUTPUT -o part1a part1a.c -lm

This user can define DEBUG if they wish to recieve step by step outputs to the terminal to help identify how values are being handled in between timesteps for troubleshooting purposes. This can be done as follows:

mpicc -g -Wall -DDEBUG -o part1a part1a.c -lm

RUNNING:
mpiexec -n <number of processes> ./part1a <number of particles> <number of timesteps>  <size of timestep> <output frequency> <g|i>

* part1b.c *

COMPILING:
mpicc -g -Wall -o part1b part1b.c -lm

The user can define NO_OUTPUT if they wish to run the program without any printed outputs in the terminal. This can be done as follows:

mpicc -g -Wall -DNO_OUTPUT -o part1b part1b.c -lm

This user can define DEBUG if they wish to recieve step by step outputs to the terminal to help identify how values are being handled in between timesteps for troubleshooting purposes. This can be done as follows:

mpicc -g -Wall -DDEBUG -o part1b part1b.c -lm

RUNNING:
mpiexec -n <number of processes> ./part1b <number of particles> <number of timesteps>  <size of timestep> <output frequency> <g|i>