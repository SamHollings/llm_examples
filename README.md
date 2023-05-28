# Large Language Model (LLM) Examples

> **Note**
> This has been setup and run using Github Codespaces with a premium github account, though you should also be able to run this within [Google Collab](https://colab.research.google.com)

This repo contains scripts showing how you might get and use some open source "Large Language Models", or LLMs. These are "ChatGPT" style models where you can submit text in natural language format, e.g. a question, and get an answer back. 

The main benefit of these models over something like ChatGPT, is that **they can feasibly be run without an internet connection**, meaning they could be deployed and served within secure systems.

It will cover:
* [Dolly by Databricks](https://www.databricks.com/blog/2023/04/12/dolly-first-open-commercially-viable-instruction-tuned-llm) 
* [Alpaca Lora by Stanford](https://github.com/tloen/alpaca-lora)

## Contact
This repository is maintained by [@samhollings](https://github.com/SamHollings).

## Description

Getting and using "pretrained" models can daunting to people who haven't done it before. There might be even be the assumption that you need to train them from stratch. Thankfully, for many usecases it's not the case and there are models which have been trained on huge datasets, with very powerful compute, which we can quite easily take and use "out of the box".

> **Note**
> Currently, these "pre-trained" models are typically stored on a website called [HuggingFace](https://huggingface.co/), which is more or less to data science models what github is code - a place where people can store, document, share and re-use models.

This repo will:
1. have some code snippets and/or links to guidance which prep Codespaces or Collab to use GPUs - these are really needed for LLMs are other wise they **aaaaaggggeeeesssss** to run,
2. extract the models from huggingface, saving them to disk (or in a "local" model repository like MLFlow) so they could be used without internet connection
3. Load the model and prep it into a form where it would be used easily - e.g. a function you can submit a string to and you receive a string back
4. Show some examples of how these functionised models can then be applied to tables of data, mimicing potential business uses.

## Prerequisites

Knowledge of Python is required

* Python (> 3.0)
* The requirements.txt contains what packages are needed.


## Getting Started

> **ToDo**


## Project structure

> **ToDo**

```text
|   .gitignore                        <- Files (& file types) automatically removed from version control for security purposes
|   config.toml                       <- Configuration file with parameters we want to be able to change (e.g. date)
|   environment.yml                   <- Conda equivalent of requirements file
|   requirements.txt                  <- Requirements for reproducing the analysis environment 
|   pyproject.toml                    <- Configuration file containing package build information
|   LICENCE                           <- License info for public distribution
|   README.md                         <- Quick start guide / explanation of your project
|
|   create_publication.py             <- Runs the overall pipeline to produce the publication     
|
+---src                               <- Scripts with functions for use in 'create_publication.py'. Contains project's codebase.
|   |       __init__.py               <- Makes the functions folder an importable Python module
|   |
|   +---utils                     <- Scripts relating to configuration and handling data connections e.g. importing data, writing to a database etc.
|   |       __init__.py               <- Makes the functions folder an importable Python module
|   |       file_paths.py             <- Configures file paths for the package
|   |       logging_config.py         <- Configures logging
|   |       data_connections.py       <- Handles data connections i.e. reading/writing dataframes from SQL Server
|   | 
|   +---processing                    <- Scripts with modules containing functions to process data i.e. clean and derive new fields
|   |       __init__.py               <- Makes the functions folder an importable Python module
|   |       clean.py                  <- Perform cleaning and wrangling processes 
|   |       derive_fields.py          <- Create new field definitions, columns, derivations.
|   | 
|   +---data_ingestion                <- Scripts with modules containing functions to preprocess read data i.e. perform validation/data quality checks, other preprocessing etc.
|   |       __init__.py               <- Makes the functions folder an importable Python module
|   |       preprocessing.py          <- Perform preprocessing, for example preparing your data for metadata or data quality checks.
|   |       validation_checks.py      <- Perform validation checks e.g. a field has acceptable values.
|   |
|   +---data_exports
|   |       __init__.py               <- Makes the functions folder an importable Python module
|   |       write_excel.py            <- Populates an excel .xlsx template with values from your CSV output.
|   |
+---sql                               <- SQL scripts for importing data  
|       example.sql
|
+---templates                         <- Templates for output files
|       publication_template.xlsx
|
+---tests
|   |       __init__.py               <- Makes the functions folder an importable Python module
|   |
|   +---backtests                     <- Comparison tests for the old and new pipeline's outputs
|   |       backtesting_params.py
|   |       test_compare_outputs.py
|   |       __init__.py               <- Makes the functions folder an importable Python module
|   |
|   +---unittests                     <- Tests for the functional outputs of Python code
|   |       test_data_connections.py
|   |       test_processing.py
|   |       __init__.py               <- Makes the functions folder an importable Python module
```

### `root`

In the highest level of this repository (known as the 'root'), there is one Python file: `create_publication.py`. This top level file should be the main place where users interact with the code, where you store the steps to create your publication.

This file currently runs a set of example steps using example data.

### `src`

This directory contains the meaty parts of the code. By organising the code into logical sections, we make it easier to understand, maintain and test. Moreover, tucking the complex code out of the way means that users don't need to understand everything about the code all at once.

* `data_connections.py` handles reading data in and writing data back out.
* `processing` folder contains the core business logic.
* `utils` folder contains useful reusable functions (e.g. to set up logging, and importing configuration settings from `config.toml`)
* `write_excel.py` contains functions relating to the final part of the pipeline, any exporting or templating happens here. This is a simplistic application of writing output code to an Excel spreadsheet template (.xlsx). A good example of this application is: [NHS sickness absence rates publication](https://github.com/NHSDigital/absence-rates). We highly recommend to use [Automated Excel Production](https://nhsd-git.digital.nhs.uk/data-services/analytics-service/iuod/automated-excel-publications) for a more in depth Excel template production application.

## Adapting for your project

> Help users configure the repository for their needs. Note that the GitHub/GitLab differentiation is not a usual requirement for a README.

### On GitHub

The [version of this repository on GitHub](https://github.com/NHSDigital/rap-package-template) is out-of-date and will be updated shortly. You are able to create your own GitHub repository from the GitHub version of this template automatically by clicking 'Use this template'.

### On GitLab

Unfortunately the [ability to create a project from template](https://docs.gitlab.com/ee/user/project/working_with_projects.html#create-a-project-from-a-custom-template) is not available on the NHS England GitLab, so the process of using this template is rather manual.

There are several workaround to use this template for your project on GitLab. One method is detailed below:

1. Clone this repository, making sure to replace `<project name>` in the snippet below to the name of your project, **not using any spaces**. To learn about what this means, and how to use Git, see the [Git guide](https://nhsdigital.github.io/rap-community-of-practice/training_resources/git/using-git-collaboratively/).

        git clone https://nhsd-git.digital.nhs.uk/data-services/analytics-service/iuod/rap-repository-template.git <project_name>

2. Change directory into this folder

        cd <project_name>

3. Delete the `.git` file (this removes the existing file revision history)

        rmdir /s .git 

4. Initialise git (this starts tracking file revision history)

        git init
5. Add the files in the repo to revision history and make the initial commit

        git add .
        git commit -m "Initial commit"
6. Create a new blank repository for your project on GitLab
7. Add the URL of this new repository to your template repo

        git remote set-url origin <insert URL>
8. Push to GitLab

        git push -u origin main

-----------

## Licence

Unless stated otherwise, the codebase is released under the MIT License. This covers both the codebase and any sample code in the documentation.

## Acknowledgements
> **ToDo**
