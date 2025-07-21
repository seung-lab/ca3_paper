# Connectomic reconstruction from hippocampal CA3 reveals spatially graded mossy fiber inputs and selective feedforward inhibition to pyramidal cells
![dataset](dataset_fig.png)
The repository is for the following preprint.  
(https://www.biorxiv.org/content/10.1101/2025.07.09.663979v1)

## Data availability
The EM image data and segmentation can be accessed at (https://pyr.ai)  
A list of all identified cell types can be found at (https://codex.flywire.ai/research/mouse_ca3_explorer)

## Install dependencies
The codes were written using Python version 3.10.14.  
The python module versions used for the analysis are in [requirements.txt](requirements.txt) file.  

Create a virtual environment. Then install all dependencies using:  
`pip install -r requirements.txt`   

The repository is not set up for pip installation.   

## Hardware dependencies
All notebook codes in this repo do not require GPUs. GPUs are required for vesicle segmentation, which was accomplished by using the software called [Cellpose](https://github.com/mouseland/cellpose).  
Training on one NVIDIA GTX 1050 Ti GPU took about 2 hours   
  
## Volumetric data and meshes
The EM and segmentation datasets are too large for conventional downloads. They can be accessed via cloudvolume, a tool that faciliates a numpy-like interface to the data for subvolume reading. 
Data is periodically updated and versioned. If you want to reproduce the results of the paper, use the materialization version 195.   
- Access the 195 version segmentation volume using:  
`from cloudvolume import CloudVolume as cv`  
`vol =cv('gs://zheng_mouse_hippocampus_production/v2/seg_m195',parallel=True, progress=False, use_https=True)`  

- Access the mesh for a specific segment ID  
`mesh = vol.mesh.get(648518346446845973)`

- Access skeleton  
`skeleton = vol.skeleton.get(648518346446845973)`  

Please reach out to the Seung Lab if you need a copy of entire volumetric dataset (e.g. to train machine learning models).
Triangulated meshes are available for all segments in the datasets (proofread and unproofread) and can be download on a per-segment basis.  

## Connectome annotations and queries

[Tutorial](https://github.com/seung-lab/ca3_paper/blob/main/CAVE%20tutorial.ipynb)  
[CAVE](https://www.caveconnecto.me/CAVEclient/) is the software infrastructure used to host the CA3 dataset and the primary access point for programmatic queries. Through CAVE synaptic connections and annotations can be queried.


## MF bouton extraction demo
To see a demo of MF bouton extraction, run the notebook script Demo_MF_bouton_extraction.ipynb  
For bouton extraction, you need both presynaptic neuron ID (i.e. MF) and postsynaptic neuron ID (i.e. Pyr cell).   
You can change the cells by changing the values in pyr_ids and mf_ids variables.  
The bouton extraction result will be saved as an .html file: ![MF bouton](bouton_extraction_example.png)  

## License
This work is licensed under a [Creative Commons Attribution-NonCommercial 4.0 International License](https://creativecommons.org/licenses/by-nc/4.0/).
[![License: CC BY-NC 4.0](https://licensebuttons.net/l/by-nc/4.0/88x31.png)](https://creativecommons.org/licenses/by-nc/4.0/)
