# Large Language Model (LLM) Examples
<a target="_blank" href="https://colab.research.google.com/github/SamHollings/llm_examples/blob/main/llm_examples.ipynb">

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

**Either:**
* Press this button and get going: <a target="_blank" href="https://colab.research.google.com/github/SamHollings/llm_examples/blob/main/llm_examples.ipynb"> 

**Or:**
Go to [Google Colab](https://colab.research.google.com/)
* Open from GitHub, selecting this repository and this notebook (or you can load this notebook and upload it into Google Colab)
* Within Colab, got to the "Runtime menu" and change the runtime type to use GPU
* Press run all, and begin playing with the notebook!

## Project structure

> **ToDo**

```text
|   .gitignore                        <- Files (& file types) automatically removed from version control for security purposes
|   config.toml                       <- [**Currently not used**] Configuration file with parameters we want to be able to change (e.g. date)
|   requirements.txt                  <- Requirements for reproducing the analysis environment 
|   pyproject.toml                    <- [**Currently not used**] Configuration file containing package build information
|   LICENCE                           <- License info for public distribution
|   README.md                         <- Quick start guide / explanation of your project
|   llm_examples.ipynb             <- Demonstrates how LLMs can be used - compatible with Google Collab    
|
+---src                               <- [**Currently not used**] Scripts with functions for use in 'create_publication.py'. Contains project's codebase.
|   |       __init__.py               <- Makes the functions folder an importable Python module
|   |
|   +---utils                     <- [**Currently not used**] Scripts relating to configuration and handling data connections e.g. importing data, writing to a database etc.
|   |       __init__.py               <- Makes the functions folder an importable Python module
|   |       file_paths.py             <- [**Currently not used**] Configures file paths for the package
|   |       logging_config.py         <- [**Currently not used**] Configures logging
|   |       data_connections.py       <- [**Currently not used**] Handles data connections i.e. reading/writing dataframes from SQL Server
|   | 
|   +---processing                    <- [**Currently not used**] Scripts with modules containing functions to process data i.e. clean and derive new fields
|   |       __init__.py               <- Makes the functions folder an importable Python module
|   |       clean.py                  <- [**Currently not used**] Perform cleaning and wrangling processes 
|   |       derive_fields.py          <- [**Currently not used**] Create new field definitions, columns, derivations.
|   | 
|   +---data_ingestion                <- [**Currently not used**] Scripts with modules containing functions to preprocess read data i.e. perform validation/data quality checks, other preprocessing etc.
|   |       __init__.py               <- [**Currently not used**] Makes the functions folder an importable Python module
|   |       preprocessing.py          <- [**Currently not used**] Perform preprocessing, for example preparing your data for metadata or data quality checks.
|   |       validation_checks.py      <- [**Currently not used**] Perform validation checks e.g. a field has acceptable values.
|   |
|   +---data_exports
|   |       __init__.py               <- [**Currently not used**] Makes the functions folder an importable Python module
|   |       write_excel.py            <- [**Currently not used**] Populates an excel .xlsx template with values from your CSV output.
|   |
+---sql                               <- [**Currently not used**] SQL scripts for importing data  
|       example.sql
|
+---templates                         <- [**Currently not used**] Templates for output files
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

> **Note**
> the code in the notebook will be refactored to use "src" shortly.

This directory contains the meaty parts of the code. By organising the code into logical sections, we make it easier to understand, maintain and test. Moreover, tucking the complex code out of the way means that users don't need to understand everything about the code all at once.

* `data_connections.py` handles reading data in and writing data back out.
* `processing` folder contains the core business logic.
* `utils` folder contains useful reusable functions (e.g. to set up logging, and importing configuration settings from `config.toml`)
* `write_excel.py` contains functions relating to the final part of the pipeline, any exporting or templating happens here. This is a simplistic application of writing output code to an Excel spreadsheet template (.xlsx). A good example of this application is: [NHS sickness absence rates publication](https://github.com/NHSDigital/absence-rates). We highly recommend to use [Automated Excel Production](https://nhsd-git.digital.nhs.uk/data-services/analytics-service/iuod/automated-excel-publications) for a more in depth Excel template production application.

## Licence

Unless stated otherwise, the codebase is released under the MIT License. This covers both the codebase and any sample code in the documentation.

## Acknowledgements
> **ToDo**
