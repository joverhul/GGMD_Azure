# Azure Instructions
This is instructions to run the Generalized Generative Molecular Design (GGMD) Pipeline.  

## Environment Setup

Before beginning, an AML environment should be created. The enviornment source should use an existing docker image with option conda file.

Existing container registry image path (Azure parent image):
mcr.microsoft.com/aifx/acpt/stable-ubuntu2004-cu116-py38-torch1121:latest

Use the conda file in this repo "Azure_AML_env_conda.yml" as the uploaded customized conda file.

A prepare_image job will be created, and the build should be successful.

## Job Setup

Create a yaml file for job submission following proper AML practices.  An example yaml file is provided at AML_GGMD.yaml.  This yaml file will serve as a base model for the JTVAE example inside the examples code. This contains the ro_mount input smiles file, the ro_mount input vocab file used to train the JTVAE model, and the ro_mount JTVAE model.  The output is saved as a rw_mount folder that will contain the generationed file from the GMD run. 

The inputs of this file should be customized based on your folder name. 
### yaml file contents
#### code
Folder that contains your source code.

#### command
Contains the .sh file, along with the inputs and outputs.

#### inputs
Input files and input names mounted on the AML space.

#### outputs
Output files that will be written to AML.

#### environment
The name of the environment you created to run the job in.

#### compute
The name of the compute cluster the job will be run on.

#### naming
The display name, experiment name, and description are all customizable for what you will call the job.

### sh script edits
To submit the job, create a .sh file that will run your desired code. An runnable example can be found script-ggmd.sh.

If you are using the AMPL scoring function provided by GGMD, you need to build your singularity container that relates to the version of AMPL used, otherwise please comment this out.

Set your input files in the order that they are listed in the yaml file.  See the example files for guidance.

The source code is uploaded from the folder you provided in the code line of the yaml file. Set your config.yaml for the specific job and the code file set to './source/main.py'.

### submit job

Once all files are updated, run the cell 

'!az ml job create -f ggmd-submit.yaml'

in the ggmd-submit-job.ipynb notebook.

Estimated time for jobs using provided values:
LogP scorer with JTVAE: ~4 minutes
LogP scorer with Autogrow: ~3 minutes
AMPL scorer with JTVAE: ~20 minutes
The extended time for the AMPL scorer is due to building the container.

## Instructions for file edits

For instructions for how to run each specific example, and the file changes necessary see the example README.md files in the example subdirectories.


