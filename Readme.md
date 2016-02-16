---
# NoName: 
## A code for Computational Cosmology Algorithm Exploration


---

# Introduction
NoName is the beginnings of a Computational Cosmology code of so far 
primarily pedagogical value. 
[Tom Abel](http://tomabel.org/) has been writing this as part of graduate
course at Stanford. It is a flexible enough framework that numerous algorithms 
may be implemented. Some choices made here are influenced by the
[enzo](http://enzo-project.org) and [Gadget](http://wwwmpa.mpa-garching.mpg.de/gadget/) 
codes.


## Current Features
	* Particle Mesh dynamics of collisionless particles
	* Comoving Coordinates
	* Restart files


## Getting Started

The code is intended to be run in the run directory as in:
`julia --color=yes -i -e "using NoName; gp, gd, p = run_noname();" particle_mesh.conf`
Here the `-i` makes julia enter interactive mode after the run is finished and
the code prints some instructions which variables hold the results. 

This assumes that the `LOAD_PATH` contains the directory in which to find
`NoName.jl`. 
You can make sure it is always found by adding 
`push!(LOAD_PATH, "/Users/tabel/Research/codes/noname/src")`
(make sure to change this to your path!) in your
`$HOME/.juliarc` 
file. 

## Dependencies
	* Logging      for basic and colorful logging
	* AppConf      for configuration file management
	* HDF5         data output
	* JLD          restart functionality
	* ArgParse     to parse commandline
	* Cosmology    for cosmological comoving coordinates
	* NearestNeighbors  for SPH and Friend of friends 


## Caveats
	* No kind of parallelism so far
	* Hydro does not work yet
	* My first larger julia code framework so very likely full of idiosyncracies 

## Configuration files

Basic code behaviour is influenced by the ___.conf files.
There is one in the `src/default.conf` directory which sets up defaults. 
The user may chose to create directory in their home directory `$HOME/.noname/` 
and store a `default.conf` there to match their preferences. This
user defined file will be read just before the one specified on the command line at
invocation `julia ../../src/noname.jl particle_mesh.conf`. 
The one on the command line has the last word. 

## Parameters

```julia
# This file specifies all the default parameters for our code
# Check the Source or some of parameter.info outputfiles for a full list
HydroMethod = MUSCL
dims        = (30, 1, 1) # main grid dimensions (active zones)
Nghosts     = ( 3, 3, 3) # ghost zones on each side in each dimension
γ           = 1.66667    # equation of state adiabatic index
DualEnergyFormalism=true # 
DomainLeftEdge  = [0. ,0., 0.]  # Size of Domain: Only tested 0..1 so far
DomainRightEdge = [1., 1., 1.]  # 
CourantFactor = 0.3

cosm_Ωm = .3 # Omega Matter
cosm_h = 0.7 # Hubble constant in units of 100 km/s/Mpc

CurrentOutputNumber=0             # Count Outputs 
OutputDirectory = "/tmp/noname"   # Where to store the output
OutputSeparateDirectories=true    # Create directories for each output
LastOutputCycle = -1
LastOutputTime  = 0.
OutputEveryNCycle = 0
OutputDtDataDump = 0.

verbose = false
RestartFileName = /tmp/restart.jld  #
ProfilingResultsFile = profiling_results.bin 
InitialDt = 0.0000001
MaximumDt = 1e30
StartTime = 0
CurrentTime = 0
StopTime = 0
StartCycle = 0
CurrentCycle = 0
StopCycle = 1000000

ParticleDimensions = [1, 1, 1] # number of particles along each dimension
ParticleDepositInterpolation = cic # none and cic implemented so far
ParticleBackInterpolation    = cic # none and cic implemented so far
```