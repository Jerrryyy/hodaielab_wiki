---
title: FreeSurfer 101
parent: Analyses
---

# FreeSurfer 
FreeSurfer is a software framework for the analysis of structural and functional MR imaging data. It is developed by the [Laboratory for Computational Neuroimaging (Harvard University)](https://martinos.org/). FreeSurfer offers a variety of MRI processing and analysis tasks, such as reconstruction of cortical surface models, anatomical segmentation of the T1 data using cortical gray matter atlases, thalamic, hippocampal segmentation and statistical analysis of the morphometry. Our lab primarily uses FreeSurfer for the T1 weighted MRI data processing and analysis.

---

## How to install freesurfer?
FreeSurfer requires Unix-based environment, therefore it can work on Linux or MacOS working stations. If you use Windows 10 as your main OS, you need to set up the [Linux subsystem on Windows](https://hungs.github.io/hodaie/computing/setup.html) first.

### Download
To install FreeSurfer on your computer, please download [this archieve](https://surfer.nmr.mgh.harvard.edu/pub/dist/freesurfer/7.1.1/freesurfer-linux-centos6_x86_64-7.1.1.tar.gz), or check the official [FreeSurfer website](https://freesurfer.net). 

### License
FreeSurfer is free software, however the license  should be obtained in order to make the framework fully operational.

[Get started now](https://surfer.nmr.mgh.harvard.edu/registration.html){: .btn .btn-primary .fs-5 .mb-4 .mb-md-0 .mr-2 }

### Setup

[Setup instructions](#setup-freesurfer){: .btn .fs-5 .mb-4 .mb-md-0 }

---

## Freesurfer analysis


Detailed tutorials can be found [here](https://surfer.nmr.mgh.harvard.edu/fswiki/Tutorials).
For the longitudinal complete MR segmentation we are using contrast-free T1 Weighted 3D MR imaging. 

Main reconstruction command - _recon-all_ takes T1 MR data (in nifti format) and performs all steps, or part of FreeSurfer grey matter reconstruction and segmentation procress.

An example of base terminal command: 

```scss
 recon-all -all -subject subjectname -i /path/to/input_volume 
 ```
where _-all_ flag, performing all steps of reconstruction; _-subject_ name of subject directory created in $SUBJECTS_DIR folder; _-i_ path to input MRI volume.

The entire reconstruction process typically takes 8-24 hours per one subject.

# NEED MORE DETAILS HERE!!!!!11!!
