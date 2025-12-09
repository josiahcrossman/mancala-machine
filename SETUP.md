# Setup instructions

## Requirements
### If running locally
Install requirements.txt, and have cuda 12.6 installed. Python version should be 3.11.5

### If running in Duke OnDemand Cluster (recommended)

These are the commands I had passed in upon setup, with the versions from requirements.txt 

* module load torch
* module load gymnasium
* module restore
* module load miniconda/23.9.0
* module load tensorflow
* module load transformers
* module load numpy

## Training
Simply running all cells in Mancala_machine.ipynb should suffice. 6 different model versions (3 for REINFORCE and 3 for Deep-Qs) will be trained and stored locally.  

## Evaluation. 
Run all cells in evaluation.ipynb to view the agents' performance playing both against a random agent and against each other. At the bottom a couple of episodes are printed such that you can view the agents' logic during gameplay. 


