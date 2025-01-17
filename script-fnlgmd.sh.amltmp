#!/bin/bash

echo "hello"

WRK="."
echo $WRK

##### If running an AMPL scorer for GGMD, uncomment the version of AMPL needed. #####

## Singularity build for AMPL 1.5
#singularity build ampl.sif docker://atomsci/atomsci-ampl:v1.5.0
#echo "ampl 1.5 singularity image pulled"

# Singularity build for AMPL 1.6
singularity build ampl.sif docker://atomsci/atomsci-ampl
echo "ampl 1.6 singularity image pulled"

CODE="./source/main.py"
CONF="./examples/AMPL_model_JTVAE/config.yaml"

smiles_input_file=$1
output_directory=$4

vocab_path=$2
model_path=$3

echo $*

python $CODE -config $CONF     \
            -smiles_input_file $smiles_input_file    \
            -vocab_path $vocab_path     \
            -model_path $model_path     \
            -output_directory $output_directory






