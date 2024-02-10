# Contents

```
Ball and Stick
	E-I_frequency
	Setting Inputs
	Two Inputs

Realistic Morphology
	E-I_frequency
	Setting Inputs
	SWC Files
mod_files
	...
```

The folder named "Ball and Stick" contains the `.hoc` files necessary to run simulations using the ball and stick model (Fig. 6, Supp. Fig. 4-6).

"E-I_frequency" contains the `.hoc` files for measuring the firing output in response to synaptic integration of multiple excitatory and inhibitory inputs (Fig. 6).

"Setting Inputs" contains the `.hoc` files for setting the values of AMPA, NMDA, GABA synaptic current amplitude and tau (Supp. Fig. 4-6).

"Two Inputs" contains the `.hoc` files for measuring the change in membrane potential evoked by the arrival of two synaptic inputs (Fig. 6).

The folder named "Realistic Morphology" contains the `.hoc` files to necessary to run simulations using the realistic morphology of D1-MSNs.

"E-I_frequency" contains the `.hoc` files for measuring the firing output in response to synaptic integration of multiple excitatory and inhibitory inputs (Fig. 7).

"Setting Inputs" contains the `.hoc` files for setting the values of AMPA, NMDA, GABA synaptic current amplitude and tau (Supp. Fig. 4-6).

"SWC Files" contains the `.swc` files with the realistic morphology of D1-MSNs in EAAC1+/+ and EAAC1-/- mice.

The folder named "mod_files" contains the NMODL files (`.mod`) which need to be compiled to be used in the NEURON model. 


# BALL-AND-STICK MODEL - OVERVIEW

## Before you run the ball-and-stick simulations

Before running any of these simultations, the following folders/files must be placed in the same folder as the main `.hoc` file:

	Required folder:
		tau_tables

	Required files:
		all_tau_vecs.hoc
		nrnmech.dll (compiled from the mod files)

To launch a simulation, load the primary `.hoc` file into NEURON, and run it from the NEURON command prompt using the following command:

	go("Output_filename")

Replace "Output_filename" with your desired name for the `.dat` output file.

When the simulation is complete, an output `.dat` named file will appear in the same folder as the original `.hoc` file that was run. 

Make sure the simulation is complete before opening the `.dat` file

## Setting input parameters

```
AMPA_amp_tau.hoc
NMDA_amp_tau.hoc
GABA_amp_tau.hoc
```

The files allow the user to determine how changing the local amplitude and tau for one AMPA, NMDA, or GABA input alters the somatic membrane potential, using the ball-and-stick model.
A simulation is run for each segment of the dendrite while systematically varying the weight and tau of the AMPA input.
The range and step size of each parameter is set by the user from the header of each .hoc file,as described below.

In the header of each of the .hoc files users can set a value for:

- model type (choose "1" for EAAC1+/+, "2" for EAAC1-/-)
- number of steps for distance (`num_d_steps`)
- number of steps for local amplitude (`num_g_steps`)
- number of steps for local tau (`num_tau_steps`)
- offset for input location (`distance_offset`)

## Two Inputs

```
IPI_Excitatory.hoc
```
or
```
IPI_Inhibitory.hoc
```

These files allow to measure the change in somatic membrane potential evoked by two synaptic inputs, either excitatory or inhibitory.

The first input is located at increasing distances from the soma, using location parameters seleted by the user (see below).

The second input is located either:
1. halfway between the first input and the distal portion of the dendrite
2. halfway between the first input and the proximal portion of the dendrite

In the header of each of the `.hoc` files users can set a value for:

- model type (choose "1" for EAAC1+/+, "2" for EAAC1-/-)
- stimulation order (choose "1" for proximal-follows-distal, "2" for distal-follows-proximal)
- number of steps for distance (`num_d_steps`)
- number of steps for local amplitude (`num_g_steps`)
- number of steps for local tau (`num_tau_steps`)
- offset for input location (`distance_offset`)

## E-I_frequency

```
Timing_files_excitatory.hoc
```
or 
```
Timing_files_inhibitory.hoc
E-I_Frequency.hoc
```

Generate the file containing information on the number and timing of activation of each input by first running "Timing_files_excitatory.hoc" and/or "Timing_files_inhibitory.hoc". 
Here, the user selects the mean frequency of activation of excitatory/inhibitory inputs, and the code returns the timing of activation of each input. 
The mean frequency value selected by the user represents the mean of a Gaussian distribution with SD=1 Hz.
The user can also specify how many permutations of the activation timing need to be generated (num_permutations)
All inputs are located randomly throughout the dendrite.

The file called "E-I_Frequency.hoc" allows to measure the number of action potentials recorded at the soma in response to the selected pattern of activation for excitatory/inhibitory inputs, using the ball-and-stick model.
 
In the header of each of the "E-I_Frequency.hoc" file, the user sets the following parameters:

- model type (choose "1" for EAAC1+/+, "2" for EAAC1-/-)
- number of excitatory steps (`num_excit_step`) 
- number of inhibitory steps (`num_inhib_step`)
- the number of repetitions (`num_repetitions`), each with different random values for the timing of activation and location 



# REALISTIC MORPHOLOGY MODEL - OVERVIEW

SWC Files
- EAAC1+_+.swc
- EAAC1-_-.swc

This set of simulations is based on the use of realistic 3D reconstructions of D1-MSNs, which can be found in the folder called "SWC Files".

This folder contains two `.swc` files, for D1-MSNs in the dorsolateral striatum of EAAC1+/+ and EAAC1-/- mice ("EAAC1+_+.swc" and "EAAC1-_-.swc", respectively)

## Before you run the realistic morphology simulations

Before running any of these simultations, the following folders/files must be placed in the same folder as the main `.hoc` file:

	Required folder:
		tau_tables

	Required files:
		all_tau_vecs.hoc
		nrnmech.dll (compiled from the mod files)

Before running simulations from the realistic morphology, the following files must also be placed in the same folder as the main `.hoc` file:

		EAAC1+_+.swc
		EAAC1-_-.swc
		ranstream.hoc

To launch a simulation, load the primary `.hoc` file into NEURON, and run it from the NEURON command prompt using the following command:

	go("Output_filename")

Replace "Output_filename" with your desired name for the `.dat` output file.

When the simulation is complete, an output `.dat` named file will appear in the same folder as the original `.hoc` file that was run. 
Make sure the simulation is complete before opening the `.dat` file

## Setting input parameters

```
AMPA.hoc
NMDA.hoc
GABA.hoc
```

The files allow the user to determine how changing the local amplitude and tau for one AMPA, NMDA, or GABA input alters the somatic membrane potential, using the ball-and-stick model.
A simulation is run for each segment of the dendrite while systematically varying the weight and tau of the AMPA input.
The range and step size of each parameter is set by the user from the header of each `.hoc` file, as described below.
The user defines the number of repetitions that can be used for each input location (`num_repetitions`) 

In the header of each of the `.hoc` files users can set a value for:

- model type (choose "1" for EAAC1+/+, "2" for EAAC1-/-)
- number of steps to increment A1 (`num_g_steps`)
- number of steps to increment tau (`num_tau_steps`)
- number of repetitions (`num_repetitions`), each with different random values for the exact input location 

## E-I_frequency

```
Timing_files_excitatory.hoc
```
or 
```
Timing_files_inhibitory.hoc
E-I_Frequency.hoc
```

Generate the file containing information on the number and timing of activation of each input by first running "Timing_files_excitatory.hoc" and/or "Timing_files_inhibitory.hoc". 
Here, the user selects the mean frequency of activation of excitatory/inhibitory inputs, and the code returns the timing of activation of each input. 
The mean frequency value selected by the user represents the mean of a Gaussian distribution with SD=1 Hz.
The user can also specify how many permutations of the activation timing need to be generated (num_permutations)
All inputs are located randomly throughout the dendrite.

The file called "E-I_Frequency.hoc" allows to measure the number of action potentials recorded at the soma in response to the selected pattern of activation for excitatory/inhibitory inputs, using the ball-and-stick model.
 
In the header of each of the "E-I_Frequency.hoc" file, the user sets the following parameters:

- model type (choose "1" for EAAC1+/+, "2" for EAAC1-/-)
- number of excitatory steps (`num_excit_step`) 
- number of inhibitory steps (`num_inhib_step`)
- number of repetitions (`num_repetitions`), each with different random values for the timing of activation and exact input location 
