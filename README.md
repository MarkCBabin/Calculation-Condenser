# Calculation-Condenser
These series of python and bash scripts are intended to allow for the queuing of jobs using Gaussian or QChem (soon to come) and to automatically read the outputs to determine 1) if the calculation finished correctly and 2) if so, to condense the relevant information into a short .txt file. 

##############################################################
			aether_queue
##############################################################	

aether_queue is a bash script intended to run two Gaussian 09 jobs (but can be easily modified to other versions) at a time. Upon completion, the script then runs G09_Output_Condenser_v2.0.py and submits two more jobs until all jobs listed in the array are completed. 

To use aether_queue:

1) Open in a text editor and add the file names to the array "a" following the syntax noted in the comments.
	i) use quotation marks to give file names (without extension) and separate entries with a space
2) Alter "SOURCEDIR" and "DESTDIR" to declare where files will be pulled from and where they will be moved to
	i) this is necessary as Gaussian 09 will create .chk files wherever aether_queue is located, and the script automatically moves these files to DESTDIR
	ii) typically, I leave this script and G09_Output_Condenser on my desktop or another easily accessed folder



##############################################################
		G09_Output_Condenser
##############################################################

This python script reads a .log file from Gaussian 09 (doing a geom or opt+freq calcuation) and determines if the calculation ran successfully (i.e. to completion) and if so creates a .txt file (or whatever extension you specify) containing the name of the file, the energy of the structure, the geometry, all normal mode frequencies and displacement vectors, as well as creates inputs for the MOBCAL and ezSpectrum programs commonly used by our group. Note that files are written to in an "append" style, meaning that one .txt file can be written to contain multiple .log files' information by simply writing to the same file (it will not overwrite, just write more at the end).


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
