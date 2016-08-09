#CONVERTING VOLUMES TO STL

####1. unzip <br />
```bash      
 gunzip rh.hippoSfLabels-T1.v10.nii.gz 
```
####2. binarize the volume: <br />
```bash
 fslmaths rh.hippoSfLabels-T1.v10.nii -bin rh.hippo_bin.nii
```
####3. create tessellated surface of binarized volume: <br />
```bash
mri_tessellate rh.hippo_bin.nii.gz 1 rh.hippo
```
####4. convert binary surface to stl format: <br />
```bash
 mris_convert rh.hippo rh.hippo.stl
```
-----------------------------------------------

#EXTRACTING A LABELED REGION

####1. create temp file: <br />
```bash
cp lh.hippoSfLabels-T1.v10.mgz lh.hippo.3dprint.mgz
```
####2. convert to nifti: <br />
```bash
 mri_convert lh.hippo.3dprint.mgz lh.hippo.3dprint.nii.gz
```
####3. set threshold range to the label number (210 for granule cell layer of the dentate gyrus) and binarize mask: <br />
```bash
fslmaths lh.hippo.3dprint.nii.gz -uthr 210 -thr 210 -bin lh.hippo.gcdg.nii.gz
```
-----------------------------------------------

#CLEANING AND REPAIRING  MODEL

##Meshlab (free)

####1. Smoothing <br />
Filters > Smoothing, Fairing, and Deformation > Laplacian Smooth

####2. Export Mesh as .stl

##Netfabb Basic (free)

####1. Click the Platform Overview button (cube with blue information "i" sign) or press F5
####2. If status says "valid mesh" then it's ready to print. If status says "incorrect mesh" then continue
####3. Click the Repair button (red cross)
####4. Click automatic repair at the bottom right
###5. Select Default repair and click Execute
###6. Click Apply Repair and select Remove Old Part
###7. Check the status of the mesh again by pressing F5 or clicking Platform Overview

-----------------------------------------------

#PRINTING/CHANGING SETTINGS  W/ MAKERBOT

Models with angles >45 degrees need support -- can't print on air. Rafts 
are platforms the object is printed on that improves adhesion to the build
plate. 

####1. Open .stl file with Makerbot Desktop software
####2. If object is large with heavy overhangs, set Support Density to 0.20 and select Extra Support. 
####3. Export .stl to .x3g file to a  2 gb or smaller SD card