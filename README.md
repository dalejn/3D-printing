<<<<<<< HEAD
#CONVERTING VOLUMES TO STL

1. unzip 
       gunzip rh.hippoSfLabels-T1.v10.nii.gz 

2. binarize the volume
	  fslmaths rh.hippoSfLabels-T1.v10.nii -bin rh.hippo_bin.nii

3. create tessellated surface of binarized volume
	mri_tessellate rh.hippo_bin.nii.gz 1 rh.hippo

4. convert binary surface to stl format
	 mris_convert rh.hippo rh.hippo.stl

#-----------------------------------------------

#EXTRACTING A LABELED REGION

1. create temp file
	cp lh.hippoSfLabels-T1.v10.mgz lh.hippo.3dprint.mgz

2. convert to nifti
	 mri_convert lh.hippo.3dprint.mgz lh.hippo.3dprint.nii.gz

3. set threshold range to the label number (210 for granule cell layer of the dentate gyrus)
     fslmaths lh.hippo.3dprint.nii.gz -uthr 210 -thr 210 lh.hippo.gcdg.nii.gz

4. divide mask file by label number so all values are binary 0s or 1s
some imaging programs don't work well with binary masks with values other
than 0s or 1s
      fslmaths lh.hippo.gcdg.nii.gz -div 210 lh.hippo.gcdg.nii.gz

#-----------------------------------------------

#CLEANING AND REPAIRING  MODEL

Meshlab (free)

1. Smoothing
Filters > Smoothing, Fairing, and Deformation > Laplacian Smooth

2. Export Mesh as .stl

Netfabb Basic (free)

1. Click the Platform Overview button (cube with blue information "i" sign) or
press F5
2. If status says "valid mesh" then it's ready to print. If status says
"incorrect mesh" then continue
3. Click the Repair button (red cross)
4. Click automatic repair at the bottom right
5. Select Default repair and click Execute
6. Click Apply Repair and select Remove Old Part
7. Check the status of the mesh again by pressing F5 or clicking Platform 
Overview
=======
# 3D-printing
3D printing the brain, hippocampus, and hippocampal subregions with magnetic connectors using freesurfer and Meshlab
>>>>>>> d91ae610c71fb9147e8ce5556bbf9f8e79764e11
