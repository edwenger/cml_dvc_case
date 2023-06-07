# CML with DVC use case

This repository contains a sample project using [CML](https://github.com/iterative/cml) with DVC to push/pull data from cloud storage and track model metrics. When a pull request is made in this repository, the following will occur:
- GitHub will deploy a runner machine with a specified CML Docker environment
- DVC will pull data from cloud storage
- The runner will execute a workflow to train a ML model (`python train.py`)
- A visual CML report about the model performance with DVC metrics will be returned as a comment in the pull request

The key file enabling these actions is `.github/workflows/cml.yaml`.

## Secrets and environmental variables
In this example, `.github/workflows/cml.yaml` contains three environmental variables that are stored as repository secrets.

| Secret  | Description  | 
|---|---|
|  GITHUB_TOKEN | This is set by default in every GitHub repository. It does not need to be manually added.  |
| AZURE_STORAGE_ACCOUNT  | Azure storage account name | 
| AZURE_STORAGE_SAS_TOKEN | Azure credential for accessing Azure storage account containers |

DVC works with many kinds of remote storage. To configure this example for a different cloud storage provider, see our [documentation on the CML repository](https://github.com/iterative/cml#using-cml-with-dvc).

## Cloning this project
Note that if you clone this project, you will have to configure your own DVC storage and credentials for the example. We suggest the following procedure:

1. Add your storage credentials as user or repository secrets for Codespaces.  Then start a Codespace and wait until the postCreateCommand has finished installing requirements.txt
2. Run `python get_data.py` to generate your own local copy of the dataset. After initializing DVC in the project directory and configuring your remote storage (see .dvc/config) run `dvc add data` and `dvc push` to push your dataset to remote storage.
3. `git add`, `commit` and `push` to push your DVC configuration to GitHub.
4. Add your storage credentials as repository secrets for Actions.
5. Enable GitHub Actions in the forked repository + modify cml.yaml conditions to run on...


