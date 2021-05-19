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

### Recon-all
Main reconstruction command - _recon-all_ takes T1 MR data (in nifti format) and performs all steps, or part of FreeSurfer grey matter reconstruction and segmentation procress.

An example of base terminal command:

```scss
 recon-all -all -subject subjectname -i /path/to/input_volume 
 ```
where _-all_ flag, performing all steps of reconstruction; _-subject_ name of subject directory created in $SUBJECTS_DIR folder; _-i_ path to input MRI volume.

The entire reconstruction process typically takes 8-24 hours per one subject.


---

### Thalamic nuclei segmentation 

Freesurfer 7.0 provides a tool which can perform a segmentation of thalamus into 25 thalamic nuclei using probabilistic atlas. 
Thalamic nuclei segmentation command required that the T1 MRI data has been analyzed with the main FreeSurfer stream, make sure to run _recon-all_ as a first step.

To run segmentation, type:

```scss
    segmentThalamicNuclei.sh  subjectname
```
Procrss will take 15 to 30 min.

The output will consist of the following three files, which can be found under the subject's mri directory:

_ThalamicNuclei.v12.T1.volumes.txt_: this text file stores the estimated volumes of the thalamic nuclei.

_ThalamicNuclei.v12.T1.mgz_: stores the discrete segmentation volumes at subvoxel resolution (0.5 mm).

_ThalamicNuclei.v12.T1.FSvoxelSpace.mgz_: stores the discrete segmentation volume in the FreeSurfer voxel space (normally 1mm isotropic, unless higher resolution data was used in recon-all with the flag -cm).

To extract the volumetric data from thalamus, type:
```scss
    asegstats2table --statsfile=thalamic-nuclei.lh.v12.T1.stats --tablefile=path/to/output/directory/tablefile.txt --subjects subjectname1 subjectname2
```
Above command will generate thalamic nuclei volume metrics from the left thalamus. To extract measurements from the right thalamus, pick the _thalamic-nuclei.rh.v12.T1.stats_ file.

### Hippocampal subfields





## _NB!_
Hippocampal subfields and thalamic segmentation require the matlab runtime package (MCR). The MCR allows users to run distributed matlab-compiled programs without paying for a matlab license

To install MCR for Freesurfer 7, type 
```scss
    fs_install_mcr R2014b
```