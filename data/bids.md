---
title: Brain Imaging Data Structure
parent: Data
---


# Overview

The [Brain Imaging Data Structure (BIDS)](https://bids.neuroimaging.io/) is a way to arrange
your imaging data along with associated metadata in a human-readable way. Ordering your data
in a standard way facilitates sharing data with others. Beyond that, there is a plethora of
standard (reproducible) processing pipelines (called [BIDSApps](https://bids-apps.neuroimaging.io/))
readily available that interface with any dataset in BIDS format.

The [standard](https://bids-specification.readthedocs.io/en/stable/) is continuously
expanded to further modalities (sMRI, dMRI, fMRI, MEG, EEG, ...) as well as results
from standard processing steps (called 'derivatives').


# Conversion to BIDS

There are many tools that support the user in converting existing data to BIDS format.
The most common usecase for us is the conversion from the DICOM format (the format
in which we receive our MRI data) to BIDS. A good choice of conversion software is
[BIDSCoin](https://github.com/Donders-Institute/bidscoin) which provides a way of
creating an MRI protocol-specific template for automatic conversion while facilitating
the template creation through a graphical interface. 


# BIDS validation

After having created (or augmented) a BIDS dataset, it is good practice to
assert that the BIDS specification is satisfied. For this purpose, the tool
[BIDS-validator](https://github.com/bids-standard/bids-validator) can be used
to check if the standard is followed and provides a report over all violations
and the available data entities.


# Resources

 * Main page for all BIDS-related resources: [link](https://bids.neuroimaging.io/)
 * Collection of BIDSApps: [link](https://bids-apps.neuroimaging.io/)
 * BIDSCoin conversion software: [link](https://github.com/Donders-Institute/bidscoin)
 * BIDS validator tool: [link](https://github.com/bids-standard/bids-validator)
 * BIDS starter kit as an entry point to the BIDS universe: [link](https://bids-standard.github.io/bids-starter-kit/)
 * Full specification of the BIDS standard: [link](https://bids-specification.readthedocs.io/en/stable/)


# Examples

Ask your lab mates for example data sets in BIDS format that we use in the lab.
