# 🌈Met-Vision 

This project was carried out as part of the "Met-Vision stratifies single cell metabolism revealing coexisting energetic states in tissue macrophages 
redistributed by inflammation" paper. 

This repository allows you to extract, interpret and classify functional metabolic information from live-cell imaging data with single-cell resolution. 
It is composed of two parts : the Fiji macro and the Python scirpt.

In the [macro folder](https://github.com/AdrianaBioinfo/MetVision/tree/main/macro) you will find the macro for displaying the single-cell view and the individual cell crops.
Individual crops are used as input to the python pipeline.

The outputs of the pipeline are :
- Pie chart representing the distribution of each metabolic class in sample/folder
- Heatmaps of ATP:ADP ratio over time and associated markers (maximum 2)
- Histograms of markers
- Tracks plot colored by cluster

## 	:zero: Preprocessing of the movies

Ensure that your films do not contain XY drift. Otherwise, correct it with Fast4DReg.

Link to Fast4DReg tutorial : https://imagej.net/plugins/fast4dreg

## :one: Visualization of single cell metabolic dynamics

Our custom macro is in the In the [macro folder](https://github.com/AdrianaBioinfo/MetVision/tree/main/macro).
Run the macro. You will have to enter the following information: 
- markers sorted by channels (ATP & ADP without space): ATPADP, F480, MHCII
- check "yes" for saving crops if you want to run the python pipeline
- "yes" to normalize the data
- "yes" to add a border around cells, if you want a grid display

The outputs are saved in the folder containing your input movie.
- *_outputs corresponds to folder with single-cell display for * marker
- indiv_crop corresponds to folder with crops of each cell for each marker

## 	:two: Prerequisites for python pipeline

To run the script you must have python. 
To download python: https://www.python.org/downloads/. The version used for this project is 3.11.9.

Clone the repository:

```SHELL
git clone https://github.com/AdrianaBioinfo/MetVision.git
```

Move to the new directory:

```SHELL
cd MetVision/src/
```

Install Miniconda :  https://docs.conda.io/en/latest/miniconda.html#windows-installers.
Once Miniconda is installed, create the envrionment and load it :

```SHELL
conda env create -f env_MetVision.yml
conda activate metvision
```
If you want to deactivate the environment, use the command :

```SHELL
conda deactivate
```
-----------------------
## :three: Running Analysis

You must have all the data in one folder (indiv_crop folder).
The subfolders need to contain "ATPADP" and the marker(s) name(s). Otherwise they will not be included in the analysis.

Ex: 
```SHELL
Working_directory:indiv_crop/
    ├──sample_X_ATPADP/
    │       ├──sample_X_crop_1
    |       ├──sample_X_crop_n
    ├──sample_X_Marker1/
    │       ├──sample_X_crop_1
    |       ├──sample_X_crop_n  
    ├──sample_X_Marker2/
            ├──sample_X_crop_1
            ├──sample_X_crop_n
    ├──sample_Y_ATPADP/
    │       ├──...
    ├──sample_Y_Marker1/
    │       ├──... 
    ├──sample_Y_Marker2/
            ├──...

```
Go in the file with the src script:
```SHELL
cd src/
```
Run the whole Python analysis, where path_to_individual_crops_folder corresponds to your path to indiv_crop folder:
```
python main.py -path path_to_individual_crops_folder -markers ATPADP F480 MHCII
```

If you need help about inputs, you can use the --help command:

```SHELL
cd src/
python main.py --help
```
```
  -h, --help            show this help message and exit
  -path PATH_WORKING_DIRECTORY, --path_working_directory PATH_WORKING_DIRECTORY
                        Enter path of the working directory
  -markers MARKERS [MARKERS ...], --markers MARKERS [MARKERS ...]
                        List of markers to process (e.g., ATPADP F480 MHCII)
  -output OUTPUT_PATH, --output_path OUTPUT_PATH
                        Optional. Enter path for the output folder. By default output folder = path
  -preds RUN_PREDICTIONS, --run_predictions RUN_PREDICTIONS
                        Optional. Compute predictions. By default "yes". You can set it to "no"
```

If you use the pipeline please cite the paper.
