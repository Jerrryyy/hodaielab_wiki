---
title: Creating a BIDS dataset with Datalad
parent: Data
---


# Overview

The following steps can be followed to setup a bids dataset
from a set of subject-wise dicom data. The referenced scripts
build on DataLad for data version control and wrap a large
part of the complexity in setting up the environments.


# Individual steps

The following variables are used to ease readability of the code examples.

```
# path to local clone of 'git@github.com:djoerch/uhn_utils'
UTILS_REPO="/.../uhn_utils"

# path to dicom dataset
DICOM_REPO="/.../test_dicom"

# path to bids dataset
BIDS_REPO="/.../test_bids"

# prefix for subject folders
SUBJ_PREFIX="sub-"

# prefix for session folders
SES_PREFIX="ses-"
```


### 1. Structure the source dicom folder

The dicom folder containing subject folders needs to follow a specific format.
It can either be created manually, or using a script, e.g. `build_dicom_dataset.sh`
as used in the NVC project (see code snippet below).

```
# path to local clone of 'git@github.com:djoerch/nvc'
NVC_REPO="/.../nvc"
bash ${NVC_REPO}/tools/subject_screening/build_dicom_dataset.sh \
    selected_subjects_bilateral_nvc.csv \
    ${DICOM_REPO} \
    ses-pre
```

The expected folder structure is as follows:

```
--<DICOM_REPO>      # root of the dicom dataset
   |
   |--<subj_01>     # subject folder
   |   |
   |   |--<ses-01>  # session folder with ALL dicom files
   |   |   |
   |   |   |--<file_01>.dcm
   |   |   |--...
   |   |
   |   |--...       # another session folder (optional, as many as needed)
   |
   |--...           # another subject folder (as many as needed)
```


### 2. Create a clean datalad repository

The mapping from MRNs to BIDS names ('sub-XX') should happen BEFORE
the datalad dataset is created to avoid capturing the MRN names. This
step is optional and depends on the state of the data. The mapping
from initial subject folder names to the new names is written to the
specified subject mapping file (.csv). This step can be repeated when
adding new subjects. No data will be overwritten.

```
# subject name mapping (will be created); two columns (ordered): 'original', 'bids'
SUBJECT_MAPPING="/.../subject_mapping.csv"  # separator MUST be ';' (not ',')

# list of folders in the dicom dataset which are NOT subject folders
EXCLUDED_FOLDERS_LIST="/.../excluded_folders.txt"  # one folder name per line

# number of digits for BIDS subject ids
DIGITS=3

# launch renaming of subject folders with BIDS names
bash ${UTILS_REPO}/datalad/conversion/00_map_subject_ids.sh \
    ${DICOM_REPO} \
    ${SUBJECT_MAPPING} \
    ${SUBJ_PREFIX} \
    ${EXCLUDED_FOLDERS_LIST} \
    ${DIGITS}
```

All scripts may be rerun multiple times (e.g. to add new subjects).
Repeated script runs will neither overwrite data nor fail due to existing
folders. So, go ahead :)

```
# list of subjects to be added to the dicom dataset
SUBJECT_LIST="/.../subject_list.txt"  # one folder name per line

# launch optional creation of datalad dataset and subject subdatasets if needed
bash ${UTILS_REPO}/datalad/conversion/01_create_datasets.sh \
    ${DICOM_REPO} \
    ${SUBJECT_LIST}
```

```
# sort dicom data by creating one folder per image sequence per subject / session
bash ${UTILS_REPO}/datalad/conversion/02_dicomsort.sh \
    ${DICOM_REPO} \
    ${SUBJECT_LIST} \
    ${SES_PREFIX}
```

```
# remove white spaces from all sequence folder names in the dicom dataset
bash ${UTILS_REPO}/datalad/conversion/03_clean_dicom_folder_names.sh \
    ${DICOM_REPO} \
    ${SUBJ_PREFIX} \
    ${SES_PREFIX}
```


### 3. Convert the dicom data to a bids dataset

The BIDS dataset is created from the cleaned dicom dataset.

```
bash ${UTILS_REPO}/datalad/conversion/04_create_bids_dataset.sh \
    ${BIDS_REPO} \
    ${DICOM_REPO}
```

The conversion from dicom to BIDS is done using the software BidsCoin.
The template describing the mapping from dicom names to valid bids filenames
is described in YAML format. The mapping usually needs to be adjusted to the
MRI sequences that were used, but we have a template for our sequences in the lab.
If you have custom needs, use the lab template and modify it for your needs.

```
# path to so-called template-bidsmap matching YOUR particular study data (there is configured lab version)
TEMPLATE_BIDSMAP="/.../bidsmap_nvc.yaml"

# list of subjects to be used for generating the so-called study-bidsmap; should be representative
SUBJECT_LIST="/.../subject_list.txt"  # one subject per line

# list of sessions to be used for generating the study-bidsmap; should be representative, too.
SESSION_LIST="/.../session_list.txt"  # one session name per line

# create the mapping from dicom data to valid bids names based on the available data
bash ${UTILS_REPO}/datalad/conversion/05_create_bidsmap.sh \
    ${BIDS_REPO} \
    ${TEMPLATE_BIDSMAP} \
    ${SUBJECT_LIST} \
    ${SESSION_LIST}
```

```
# customaize the infered study bidsmap for the data at hand
bash ${UTILS_REPO}/datalad/conversion/06_customize_bidsmap.sh \
    ${BIDS_REPO}
```

```
# list of subjects to be converted to BIDS format (could be a subset in case new subjects are added)
SUBJECT_LIST="/.../subject_list.txt"  # one subject per line

# list of sessions to be converted to BIDS format (could be a subset in case of new sessions to be added)
SESSION_LIST="/.../session_list.txt"  # one session name per line

# convert chosen subjects / sessions from dicom to bids format
bash ${UTILS_REPO}/datalad/conversion/07_convert_to_bids.sh \
    ${SUBJECT_LIST} \
    ${SESSION_LIST}
```
