# Calculation-Condenser
These series of python and bash scripts are intended to allow for the queuing of jobs using Gaussian or QChem (soon to come) and to automatically read the outputs to determine 1) if the calculation finished correctly and 2) if so, to condense the relevant information into a short .txt file. 

Input: python G09_Output_Condenser_v2.0.py input_name output_name

output_name can be whatever filetype desired, I often use name.txt for convenience.

Output: (name.txt) 

You will get a txt (or whatever other format) with the following information

====================================================================================
====================================================================================
				                             Using Version 2.0
			                    This section is for input_name.log
				                          Success:	TRUE/FALSE
====================================================================================
====================================================================================

if FALSE: error code from Gaussian & last optimization step number

if TRUE:

SCF Energy
Frequncies (if calculated)
Normal modes (if calculated)
Geometry
MOBCAL input 
ezSpectrum input (if opt+freq)
