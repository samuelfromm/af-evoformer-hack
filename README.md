# AFEvohack

Hack of Alphafold 2 so that it outputs additional results computed by feeding the output of intermediate layers of the evoformer into the standard heads (in particular the structure module and the predicted aligned error head.) Note that these heads are trained using the final layer and we did not retrain the heads for the intermediate layers.

Usage:

* To control which layers to output, use the `--extra_evoformer_output_layers` flag. For instance, `--extra_evoformer_output_layers='10'` outputs an additional "structure", pTM values, etc. by using the pair representation computed by the 10-th layer of the evoformer.
* To skip certain intermediate layers in the evoformer, use the `--skip_evoformer_blocks` flag. For instance, `--skip_evoformer_blocks='20,30'` skips layers 20 and 30.
* To only calculate the PredictedAlignedErrorHead (pTM and ipTM), use the `--run_only_pae_head` flag. In particular this skips the structure module.
* We use a version of Alphafold 2.3.1. We refer to https://www.nsc.liu.se/support/systems/berzelius-software/berzelius-alphafold/#running-alphafold-using-conda
on how to create a CONDA environment to run Alphafold


## TODO

* Add code to output the result of the head associated with "masked_msa", "distogram", "experimentally_resolved".    
* Add support for Alphafold monomer.



## Kown issues

* The implementation is very (memory) inefficient (as we save the output of each evoformer layer, even if they are not needed). Running larger proteins might cause issues.
