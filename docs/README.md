# Arabic AI Text Detection - MSIS822

This is my final project for MSIS822. The goal is to distinguish human-written Arabic text from AI-generated text using 
machine learning.

## Phase 1: Project Setup and Data Acquisition

I created the GitHub repository, downloaded the dataset, inspected its structure, and checked the initial data quality 
and class distribution.

## Dataset

Source: 
[KFUPM-JRCAI/arabic-generated-abstracts](https://huggingface.co/datasets/KFUPM-JRCAI/arabic-generated-abstracts)

| Subset                 | Source rows |
| ---------------------- | ----------: |
| by_polishing           |       2,851 |
| from_title             |       2,963 |
| from_title_and_content |       2,574 |
| Total                  |       8,388 |

Each row contains one human-written abstract and four AI-generated versions. The original columns are:

* `original_abstract`
* `allam_generated_abstract`
* `jais_generated_abstract`
* `llama_generated_abstract`
* `openai_generated_abstract`

All five columns have the `string` data type in all three subsets.

## Initial Data Quality Checks

The checks found:

* No missing text values.
* No empty or whitespace-only texts.
* No fully duplicated rows within each subset.

After combining the subsets and trimming leading and trailing whitespace from the human abstracts, I found 2,992 unique 
human abstracts and 5,396 repeated occurrences beyond the first.

Repeated human abstracts may have different AI-generated versions, so they are different from fully duplicated rows.

## Class Distribution

I reshaped the dataset so that each row represents one text and added the classification labels.

| Class        | Label | Text entries | Percentage |
| ------------ | ----: | -----------: | ---------: |
| Human        |     0 |        8,388 |        20% |
| AI-generated |     1 |       33,552 |        80% |
| Total        |       |       41,940 |       100% |

These counts include repeated entries and describe the data before deduplication.

I also added a `group_id` based on the trimmed human abstract. This links related texts and will help keep them 
together when splitting the data in a later phase.

## Running the Notebook

The project uses Python 3.8.20. Package versions are listed in [requirements.txt](../requirements.txt), and the Conda 
environment is defined in [environment.yml](../environment.yml).

For a new setup, run these commands from the project folder:

1. `conda env create -f environment.yml`
2. `conda activate msis822`
3. `jupyter notebook`

Open [notebooks/data_acquisition.ipynb](../notebooks/data_acquisition.ipynb) and run the cells in order. The dataset is 
loaded from Hugging Face.

## Current Progress

This update covers Phase 1: project setup and data acquisition

