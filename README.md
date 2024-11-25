# KGRA

**This is the data and code for our paper** `Knowledge Graph Relational Attention Model for Drug Repurposing`.

## Requirements
* `Python(version >= 3.6)`
* `pytorch(version>=1.4.0)`
*  `ordered_set(version>=3.1)`
* `pytorch>=1.7.1 & <=1.9`
* `numpy(version>=1.16.2)`
* `torch_scatter(version>=2.0.4)`
* `scikit_learn(version>=0.21.1)`
* `torch-geometric`
  

We highly recommend you to use conda for package management.

## Datasets

We provide the dataset in the [data](data/) folder.

- [GP-KG](data/GP-KG.zip)
- [OpenBioLink](data/Openbiolink.zip)
- [Biokg](data/Biokg.zip)

## Repository structure

The current repository is structured in the following way:
```
|-- KGRA.jpg
|-- README.md
|-- main.py
|-- test.py
|-- config
|   |-- log_config.json
|-- data (Data folder)
|   |-- GP-KG.zip
|   |-- Openbiolink.zip
|   `-- Biokg.zip
`-- model
    |-- RMHA.py
    |-- data_loader.py
    |-- message_passing.py
    |-- predict.py
    |-- tools.py
```

## Model

The basic structure of our model an be found in [model](model/) folder.
The model can be divided into 3 parts, RMHA module, Interact Layer module and Knowledge-weighted loss. 

## Training
Training-related utilities can be found in [`main.py`](main.py). They accept `Iterator`'s that yield batched data,
identical to the output of a `torch.utils.data.DataLoader`. Use the following command to train the model, the model will be named as "test_model" and saved in the directory "model_saved".
```
    python main.py -data dataset_directory -gpu 0 -name test_model -epoch 400
```

## Drug-Disease Predicting
Test-related utilities can be found in [`test.py`](test.py). Create a test file named as "drug_pre.txt" and moved the file to the folder "test_data". Run the following command, predicting results will be saved in the file "results.txt".
```
    python test.py -data test_data -gpu 0 -name test_model -test_file drug_pre.txt -save_result result.txt
```

Parameter Note:
-data the directory of training and testing data
-gpu the GPU to use
-name the name of the model snapshot (used for storing model parameters)
-epoch the number of epochs
-save_result the filename that is used to store test results
-test_file the name of testing file

