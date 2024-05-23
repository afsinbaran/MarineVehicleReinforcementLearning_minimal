# Underwater Vehicle Reinforcement Learning - Minimal

[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.7981976.svg)](https://doi.org/10.5281/zenodo.7981976)

An unofficial fork the original [Underwater Vehicle Reinforcement Learning repo](https://github.com/UnnamedMoose/MarineVehicleReinforcementLearning) by MARIN. This fork has almost no functional difference from the original, it just has been simplified and cleaned for the course "Control of Marine Vehicles with Deep RL" of Naval Architecture and Ocean Engineering Faculty at Istanbul Technical University. Please refer to the original repo if you want more information about the code.

## Overview

*Quoted from the original repo*

Simple example of how to manoeuvre an underwater vehicle using reinforcement learning.

The problem is posed by placing an underwater vehicle at a random position and
heading inside the domain. It then needs to make its way to the origin and adopt
a specific heading. There is a background turbulent flow along the x-axis with
creating time-varying disturbances moving the vehicle away from the goal point.

The manoeuvring model is deliberately simplified
in order to keep the simulations fast. Specifically, added mass and inertia have
been ignored, rigid body accelerations are not taken into account, and cross-coupling
hydrodynamic coefficients are set to zero. Only three degrees of freedom (surge,
sway, yaw) are considered and time integration is performed using the Euler method.
All of this is done in order to make the solution procedure as fast as possible
and allow rapid training of RL agents rather than prioritising accuracy of the
physics model.

In addition to an RL agent, a simple proportional-derivative (PD)
controller is used as a benchmark.

![Alt text](fig_readme/episode_anim.gif?raw=true "Example episode.")

## Usage

*Slight differences with the original repo*

This fork removes all the log files, trained agents, etc... from the repo. To remove the bloat from the repo I needed to nuke the history. I've achieved this by creating an orphan branch, committing the minimal version to it, and removing the original main branch.

Other than that, the environment code has been moved into it's own package for better user experience:
    * `verySimpleAuv.py` (untouched): Implements the environment.
    * `flowGenerator.py` (untouched): Uses pre-computed spectral POD from [pySPOD](https://github.com/MathEXLab/PySPOD) to generate turbulent flow. Data has been generated using [ReFRESCO](https://www.marin.nl/en/facilities-and-tools/software/refresco) CFD code building on the synthetic turbulence generation technique described in [Lidtke et al.](https://doi.org/10.3390/jmse9111274).
    * `resources.py` (minor changes): Implements functions for plotting, training and evaluating RL agents.

The module *definitely* could be implemented better.

An example usage is provided in `main.py`. This script trains multiple agents with the same configuration on the CPU using multiprocessing and benchmarks them against a simple PD controller. It is a modified version of `main_00_sbl.py` from the current iteration of the original repo (as of 23/05/2024). `main.py` shaves of and adjusts parts of the code for a better user experience.

The fork also includes a `requirements.txt` file that should have been in the original repo. For students who are not as familiar with virtual environments, to set up the environment and install dependencies:

1. Open a terminal and navigate to your working directory.

2. Create a virtual environment:

```
python -m venv venv
```

3. Activate the virtual environment:

	* On Windows:
	```
	.\venv\Scripts\activate
	```
	
	* On macOS/Linux:
	```
	source venv/bin/activate
	```

4. Install the requirements:

```
pip install -r requirements.txt
```

## How to cite?

To cite the **original repo**, you can currently (23/05/2024) use the following bibtex but please refer to the original repo for possible future changes:

```
@software{Lidtke_2023_7981976,
  author       = {Lidtke, Artur K.},
  title        = {Underwater Vehicle Reinforcement Learning},
  month        = May,
  year         = 2023,
  publisher    = {Zenodo},
  version      = {v1.0},
  doi          = {10.5281/zenodo.7981976},
  url          = {https://doi.org/10.5281/zenodo.7981976}
}
```
