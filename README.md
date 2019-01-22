# The BIDS Toolbox

This repository holds the code for The BIDS Toolbox, a web service for the creation and manipulation of BIDS datasets. It has been developed at Cardiff University Brain Research Imaging Centre (CUBRIC) in collaboration with Cardiff University Data Innovation Research Institute (DIRI) and funded by the Science and Technology Facilities Council (STFC) under the MiDac project.

### Software pre-requisites

Flask, PyDicom and Numpy: can be installed using pip as: `pip install flask flask-restful pydicom numpy`

Dcm2Niix: install latest version from official repository https://github.com/rordenlab/dcm2niix

This software uses parts of [bidskit](https://github.com/jmtyszka/bidskit), but it doesn't need to be installed.

### Running the service

Clone repository and run from parent directory: `python server.py`

File `config.json` contains the configurations parameters for the toolbox. Right now, it allows to enable/disable verbose output console log.

### API

The following POST methods are provided:

+ createBids(): create a BIDS dataset from a set of DICOM images.
+ updateBids(): appends new scans to an existing BIDS dataset created by createBids().

These two methods receive arguments in JSON format:

``` js
{
	"scans": {
		"01": {
			"01": "/path to DICOM files for subject 01, scan 01"
		},
		"02": {
			"01": "/path to DICOM files for subject 02, scan 01",
			"02": "/path to DICOM files for subject 02, scan 02"
		}
		}
	},
	"output": "/ path to BIDS dataset in permanent storage",
	"metadata": {
		"modalities": [{
				"tag": "CHARMED",
				"type": "dwi",
				"modality": "dwi"
			},
			{
				"tag": "t1_mprage",
				"type": "anat",
				"modality": "T1w"
			}
		],
		"datasetDescription": {
			"item": "Item to be added to dataset_description.json"
		}
	},
	"pipeline": {
		"run": "yes",
		"config": {
			"param1": 0.55,
			"param2": 6.12
		}
	}
}
```
