# DEEPScreen: Virtual Screening with Deep Convolutional Neural Networks Using Compound Images

* DEEPScreen is a large-scale DTI prediction system, for early stage drug discovery, using deep convolutional neural networks
* One of the main advantages of DEEPScreen is employing readily available 2-D structural representations of compounds at the input level instead of conventional descriptors that display limited performance
* DEEPScreen learns complex features inherently from the 2-D representations, thus producing highly accurate predictions. 
* DEEPScreen system was trained for 704 target proteins (using curated bioactivity data) and finalized with rigorous hyper-parameter optimization tests
* DEEPScreen system was run on more than a million of compound records in ChEMBL database to produce nearly 21 million novel DTI predictions (file: resultFiles/DEEPScreen_Largescale_DTI_predictions.zip)
* Ready-to-use target-based predictive models of DEEPScreen can be used to scan any small molecule against 704 target proteins (explained below) 


![alt text](http://user.ceng.metu.edu.tr/~arifaioglu/publication_figures/deepscreen/deepscreen_figure.png)

## Descriptions of folders and files under the DEEPScreen repository

* **bin** This folder includes the source code of DEEPScreen

* **inputDatasets** folder contains various datasets used in system training and tests:
   * **ChEMBL23_preprocessed_activities_sp_b_pchembl.zip** contains bio-activities from the ChEMBL database (v23) after the application of multiple filtering operations to obtain a clean training set.
   * **ChEMBL24_preprocessed_activities_sp_b_pchembl.zip** contains bio-activities from the ChEMBL database (v24) after the application of the same filtering operations applied for ChEMBL23_preprocessed_activities_sp_b_pchembl.zip. This dataset was used to extract novel bio-interactions that was not included in ChEMBL v23, for our analyses.
   * **DEEPScreen_finalized_training_dataset_act_inact.txt** is the finalized training dataset of DEEPScreen. The file contains active and inactive compounds for each of the 704 target proteins. The files has the same format as act_inact_comps_10.0_20.0_chembl_preprocessed_sp_b_pchembl_data_blast_comp_20.txt, the only difference is that this file contains the information for 704 trained targets of DEEPScreen, instead of all ChEMBL targets.
   * **Renin_Molecular_Docking_Input_Files.zip** contains various input files/datasets for the molecular docking experiments on the renin target protein, to be used in the case study.
   * **RXRb_Molecular_Docking_Input_Files.zip** contains various input files/datasets for the molecular docking experiment on the RXRbeta target protein, to be used in the DEEPScreen vs conventional classifier comparison.

* **trainingFiles** folder includes the files used in the training of the system:
    * **act_inact_comps_10.0_20.0_chembl_preprocessed_sp_b_pchembl_data.txt** contains the active and inactive compound information for each target protein in ChEMBL, before the similarity-based negative training dataset enrichment process. In this file, there are two lines for each target, in the following format:
    
       ```
       CHEMBL1790_act	CHEMBL205013,CHEMBL96731,CHEMBL328791,...
       CHEMBL1790_inact	CHEMBL306645,CHEMBL1765671,CHEMBL1765668,....
       ```
    
       The list of active/inactive compounds separated by commas (i.e., the second tab seperated column: *CHEMBL205013,C...*) for the correnponding target (i.e., the first column: *CHEMBL1790_act*),
    * **act_inact_comps_10.0_20.0_chembl_preprocessed_sp_b_pchembl_data_blast_comp_20.txt** contains the active and inactive compound information for each target protein in ChEMBL, after the similarity-based negative training dataset enrichment process. The format of the file is same as above,
    * **chembl23_chemreps.txt.zip** contains the SMILES and InChI representations for all ChEMBL compounds (version 23).
    * **chembl_uniprot_mapping.txt** contains the id mapping between UniProt accessions and ChEMBL ids for proteins,
    * **DUDEDatasetFiles.zip** contains training/test dataset for the DUD-E dataset,
    * **Lenselink_Dataset_Files.zip** contains training/test datasets in Lenselink et al.'s study,
    * **MUVDatasetFiles.zip** contains training/test dataset for the MUV dataset, together with the InChI representations for all ChEMBL compounds (version 23),
    * **sample_test_compound_file.txt** contains the SMILES representations for an example set of query compounds, in tab-seperated format, with a header. The first column is the query compound identifier and the second colunmn is the SMILES,
    * **trained_target_families.txt** contains the high level protein family information for 704 targets of DEEPScreen, in tab-separated format (Target UniProt accession, Target ChEMBL id and protein family name).
    
* **tempImage** folder is empty. It is required for storing the temporarily generated 2-D images of compounds.
    
* **tflearnModels**
    * folder is used for storing the trained predictive models (it currently contains the model files for only one example target protein: CHEMBL1790),
    * the trained model files for 704 DEEPScreen targets can be dowloaded from [here](https://www.dropbox.com/sh/x1w9wqe1fxmdl1w/AACD7gV2vRFPgoN653WCRjaia?dl=0) and should be placed under this folder, in the local machine before running the scripts
    
* **resultFiles** folder contains results of various tests/analyses:
   * **Conventional_ECFP4_Models_Performance_Test_Results.txt** contains the test performance results of the conventional/shallow classifiers (i.e., LR, FR and SVM) trained with compound molecular fingerprints (i.e., ECFP4), which represents the current state-of-the-art,
   * **Conventional_Image_Models_Performance_Test_Results.txt** contains the test performance results of the conventional/shallow classifiers (i.e., LR, FR and SVM) trained with compound 2-D image features (same as DEEPScreen),
   * **DEEPScreen_704_Targets_UniP_EntN_GenSym_Org_ChEid.txt** contains the information (i.e., UniProt accession, Entry name, Gene name, Organism and Target ChEMBL id) for the 704 DEEPScreen target proteins in tab-separated format,
   * **DEEPScreen_Largescale_DTI_predictions.zip** contains the results of the large-scale DTI prediction run (only active/interacting compound-target pair predictions are included) for all of the DEEPScreen targets, in tab-separated format (i.e., Target ChEMBL id, Target UniProt accession, Compound ChEMBL id),
   * **deepscreen_models_hyperparameters_performance_results.tsv** stores the hyper-parameter values and the performance results of the finalized DEEPScreen models in the independent performance tests,
   * **DEEPScreen_Models_Performance_Test_Results.txt** same as deepscreen_models_hyperparameters_performance_results.tsv but in a simplified format, where only the independent test performance results are included,
   * **dude_models_hyperparameters_performance_results.tsv** stores the hyper-parameter values and the test performance results of the models trained with the DUD-E dataset,
   * **lenselinks_models_hyperparameters_performance_results.tsv** stores the hyper-parameter values and the test performance results of the models trained with Lenselink et al's dataset,
   * **LOGS** folder contains the log files of the hyper-parameter opmization and performance test runs,
   * **muv_models_hyperparameters_performance_results.tsv** stores the hyper-parameter values and the test performance results of the  models trained with the MUV dataset.
   * **Renin_Active_Ligand_Drug_Predictions_ChEMBLid.txt** contains the interacting ligand predictions (only FDA approved or experimental drugs) for the renin target protein (ChEMBL compound ids), to be used in the case study.
   * **Renin_Molecular_Docking_Results.zip** contains various results files of the molecular docking experiments on the renin target protein, to be used in the case study.
   * **RXRb_Molecular_Docking_Results.zip** contains various results files of the molecular docking experiment on the RXRbeta target protein, to be used in the DEEPScreen vs conventional classifier comparison.
         
## Dependencies
#### [tflearn 0.3.2](https://pypi.org/project/tflearn/)
#### [sklearn 0.19.2](https://scikit-learn.org/0.19/install.html)
#### [numpy 1.14.5](https://pypi.python.org/pypi/numpy/1.13.3)
#### [cairosvg 2.1.2](https://pypi.org/project/CairoSVG/)
#### [rdkit 2016.09.4](http://rdkit.org/docs/Install.html)


## How to train a target-based DEEPScreen model

* Install dependencies and necessary libraries
* Clone the DEEPScreen repository (files under the trainingFiles folder are not downloaded directly when the repository is cloned, instead they should be downloaded and placed int the local trainingFiles folder manually)
* Decompress the zipped files
* Run DEEPScreen script by providing values for the following command line arguments:
    * The selected DNN architecture (ImageNetInceptionV2 or CNNModel)
    * target ChEMBL ID
    * The optimizer type (adam, momentum or rmsprop)
    * The learning rate
    * The number of epochs
    * The number of neurons in the first fully-connected layer
    * The number of neurons in the second fully-connected layer
    * The drop-out keep rate
    * Save model (should be 1 to save the model or 0 for not saving)

To train a model using the same hyper-parameter value selections as DEEPScreen, you can use the hyper-parameter values given in the file: **deepscreen_models_hyperparameters_performance_results.tsv**, which is located under the **resultFiles** folder. Below is a sample command to train a predictive model for target **CHEMBL1790**:

```
python trainDEEPScreen.py CNNModel CHEMBL1790 adam 0.0005 15 128 0 0.8 1
```

**Output of the script:**

The performance evaluation results and the specific predictions for the compounds in the independent test set are given as the output. In the last line, the predictions for the test compounds are written in tab-separated format, where each field is separated by commas as:

* <compound_id>,<prediction_outcome>,<true_label>

An example output of the command above:

```
Test AUC:0.9445025083612041
Test AUPRC:0.9379908635681835
Test_f1score:0.88
Test_mcc:0.78
Test_accuracy:0.89
Test_precision:0.91
Test_recall:0.85
Test_tp:78
Test_fp:8
Test_tn:96
Test_fn:14
Test Predictions:
CHEMBL435331,TP,ACT     CHEMBL3354592,TP,ACT    CHEMBL44134,TN,INACT    CHEMBL422701,TN,INACT   CHEMBL105961,FN,ACT ...,
```

## How to re-produce the results for DEEPScreen vs state-of-the-art predictors performance comparison

The name of the targets and hyper-parameter values are available in the following files:
* **dude_models_hyperparameters_performance_results.tsv**,
* **lenselinks_models_hyperparameters_performance_results.tsv**,
* **muv_models_hyperparameters_performance_results.tsv** 
which are located under the **resultsFiles** folder.
* To train DEEPScreen on the MUV dataset

```
python trainConvNetMUV.py CNNModel MUV_692 adam 0.001 15 128 0 0.8 0
```

* To train DEEPScreen on the DUD-E dataset

```
python trainDEEPScreenDUDE.py ImageNetInceptionV2 hdac8 adam 0.0001 5 0 0 0.8 0
```

* To train DEEPScreen on Lenselink et. al.'s dataset

```
python trainDEEPScreenLenselink.py ImageNetInceptionV2 CHEMBL274 adam 0.0001 5 0 0 0.8 0
```

The output of these commads same as the output shown above. Please note that you should unzip the corresponding folders (**DUDEDatasetFiles.zip**, **MUVDatasetFiles.zip** or **Lenselink_Dataset_Files.zip**) before running the training scripts.

## How to run ready-to-use DEEPScreen models to generate predictions for a set of query compounds

* Each target protein has a model, consisting of three files
* To be able to run a trained model, the files should be located under the **tflearnModels** folder
* The trained model files for 704 DEEPScreen targets can be dowloaded from [here](https://www.dropbox.com/sh/x1w9wqe1fxmdl1w/AACD7gV2vRFPgoN653WCRjaia?dl=0)

**Example:**

The model files for an example target **CHEMBL1790** are under **tflearnModels** folder. For our example, the the model files for the target **CHEMBL1790** are as follows:

* CNNModel_CHEMBL1790_adam_0.0005_15_128_0.8_True-300.data-00000-of-00001
* CNNModel_CHEMBL1790_adam_0.0005_15_128_0.8_True-300.index
* CNNModel_CHEMBL1790_adam_0.0005_15_128_0.8_True-300.meta

Users should run **loadDEEPScreenModel.py** script to provide predictions for a set of compounds. The arguments of this script are as follows:

```
python loadDEEPScreenModel.py  <target_id> <model_name> <path_to_smiles_of_compounds>
```

where **<target_id>** is the ChEMBL id of the target protein, **<model_name>** stands for the name of the model for the corresponding target stored under the **tflearnModels** folder (without the filename extension), and the last argument is the path to the SMILES of the query compounds. The SMILES file is a tab-seperated file with a header where the first column is the query compound identifier and the second colunmn is the smiles strings. You could have additional columns, which will be discarded by the script. There is a sample file (i.e. **sample_test_compound_file.txt**) under **../trainingFiles** folder. You can run the following script to get the predictions for the compounds in the sample file. 

```
python loadDEEPScreenModel.py  CHEMBL1790 CNNModel_CHEMBL1790_adam_0.0005_15_128_0.8_True-300 ../trainingFiles/sample_test_compound_file.txt
```

Output: The script provides compound identifiers (i.e., ChEMBL ids), which are predicted as active (i.e., interacting) for the corresponding target:

```
ACTIVE PREDICTIONS:CHEMBL1790
CHEMBL350383
CHEMBL319636
CHEMBL182627
CHEMBL444956
CHEMBL331956
```

## License

DEEPScreen
    Copyright (C) 2018 CanSyL

This program is free software: you can redistribute it and/or modify it under the terms of the GNU General Public License as published by the Free Software Foundation, either version 3 of the License, or (at your option) any later version.

This program is distributed in the hope that it will be useful, but WITHOUT ANY WARRANTY; without even the implied warranty of MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE. See the GNU General Public License for more details.

You should have received a copy of the GNU General Public License along with this program.  If not, see <http://www.gnu.org/licenses/>.

