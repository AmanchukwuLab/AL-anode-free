# Active learning for anode-free lithium metal battery electrolyte optimization

This repository contains codes, datasets, and model checkpoints for the article "Active learning accelerates electrolyte solvent screening for anode-free
lithium metal batteries". The objective of this work is to utilize Gaussian process regression (GPR) models and Bayesian model averaging (BMA) to optimize capacity retention efficiently across a virtual search space of 1 million electrolyte candidates.

## Project Overview
The repository includes:
1. All labeled and unlabeled datasets from each batch of active learning campaign.
2. All codes and notebooks to replicate main findings of this study.
3. Trained surrogate model checkpoints from each batch of active learning campaign.

## Directory Structure
```plaintext
.
├── README.md
├── datasets
│   ├── batch-1
│   │   └── top_5000_suggestions_batch1_uniq_solvents.csv
│   ├── batch-2
│   │   ├── label_data_post_batch1.csv
│   │   ├── top_5000_suggestions_batch2_uniq_solvents.csv
│   │   └── virtual_search_space_for_batch2.csv
│   ├── batch-3
│   │   └── label_data_post_batch2.csv
│   │   ├── top_10000_suggestions_batch3_uniq_solvents.csv
│   │   └── virtual_search_space_for_batch3.csv
│   ├── batch-4
│   │   └── label_data_post_batch3.csv
│   │   ├── top_10000_suggestions_batch4_uniq_solvents.csv
│   │   └── virtual_search_space_for_batch4.csv
│   ├── batch-5
│   │   └── label_data_post_batch4.csv
│   │   ├── top_5000_suggestions_batch5_uniq_solvents.csv
│   │   └── virtual_search_space_for_batch5.csv
│   ├── batch-6
│   │   └── label_data_post_batch5.csv
│   │   ├── top_5000_suggestions_batch6_uniq_solvents.csv
│   │   └── virtual_search_space_for_batch6.csv
│   ├── batch-7
│   │   └── label_data_post_batch6.csv
│   │   ├── top_5000_suggestions_batch7_uniq_solvents_EI.csv
│   │   ├── top_5000_suggestions_batch7_uniq_solvents_greedy.csv
│   │   └── virtual_search_space_for_batch7.csv
│   └── virtual_search_space_1million.csv
├── models
│   ├── batch-1
│   │   ├── matern_batch1.pkl
│   │   ├── pairwise_batch1.pkl
│   │   ├── rbf-ess_batch1.pkl
│   │   └── rq_batch1.pkl
│   ├── batch-2
│   │   ├── matern_batch2.pkl
│   │   ├── pairwise_batch2.pkl
│   │   ├── rbf-ess_batch2.pkl
│   │   └── rq_batch2.pkl
│   ├── batch-3
│   │   ├── matern_batch3.pkl
│   │   ├── pairwise_batch3.pkl
│   │   ├── rbf-ess_batch3.pkl
│   │   └── rq_batch3.pkl
│   ├── batch-4
│   │   ├── matern_batch4.pkl
│   │   ├── pairwise_batch4.pkl
│   │   ├── rbf-ess_batch4.pkl
│   │   └── rq_batch4.pkl
│   ├── batch-5
│   │   ├── matern_batch5.pkl
│   │   ├── pairwise_batch5.pkl
│   │   ├── rbf-ess_batch5.pkl
│   │   └── rq_batch5.pkl
│   ├── batch-6
│   │   ├── matern_batch6.pkl
│   │   ├── pairwise_batch6.pkl
│   │   ├── rbf-ess_batch6.pkl
│   │   └── rq_batch6.pkl
│   └── batch-7
│       ├── matern_batch7.pkl
│       ├── pairwise_batch7.pkl
│       ├── rbf-ess_batch7.pkl
│       └── rq_batch7.pkl
└── notebooks
    ├── active-learning
    │   ├── active_learning_batch_1.ipynb
    │   ├── active_learning_batch_2.ipynb
    │   ├── active_learning_batch_3.ipynb
    │   ├── active_learning_batch_4.ipynb
    │   ├── active_learning_batch_5.ipynb
    │   ├── active_learning_batch_6.ipynb
    │   └── active_learning_batch_7.ipynb
    ├── active-learning_only-LFP-data
    │   ├── active_learning_batch_1.ipynb
    │   ├── active_learning_batch_2.ipynb
    │   ├── active_learning_batch_3.ipynb
    │   ├── active_learning_batch_4.ipynb
    │   ├── active_learning_batch_5.ipynb
    │   ├── active_learning_batch_6.ipynb
    │   └── active_learning_batch_7.ipynb
    ├── manuscript-plots
    │   ├── functional_group_classification.ipynb
    │   ├── t-SNE_plot.ipynb
    │   └── shap_analysis.ipynb
    └── screening
        ├── screen_emolecules_database.ipynb
        └── screen_pubchem_database.ipynb
```

## Datasets
The following datasets are used in this project:

1. **Virtual chemical search space**
   - File `virtual_search_space_1million.csv` inside the directory `datasets`: this is the original virtual search space containing 1 million electrolytes on which optimization is carried in this work.
   - Files named `virtual_search_space_for_batch*.csv` inside the directory `datasets/batch-*`: virtual search space for each subsequent active learnign campaign will be effectively the labeled electrolytes removed from the original search space. Therefore, different files are required for each batch.
   - These files are not present in the GitHub repo as they are ~500 MB in size while GitHub only allows uploads upto 25 MB in size. They can be downloaded from [Box](https://uchicago.box.com/s/8ffdqrfgf7v4fogxi4nkzl2dlw6fuj72) and then put inside respective directories.

2. **Labeled datasets**
   - Files named `label_data_batch*.csv` inside the directory `datasets/batch-*`: labeled datasets obtained from preceding batches (used for training surrogate models in each batch along with in-house data) (from batch 2 onwards).

3. **Top 5000/1000 suggested datasets** 
   - Files named `top_5000_suggestions_batch*_uniq_solvents.csv` or `top_10000_suggestions_batch*_uniq_solvents.csv`: these files contain unique solvent combinations from top 5000 or 10000 suggestions by the active learning framework in each batch. These were fed to the eMolecules repository to manually find purchasable candidates.

## Notebooks
The repository includes codes (Jupyter notebooks) for different purposes inside:

1. `notebooks/active-learning`: Contains `active_learning_batch_*.ipynb` files for each batch. Run the notebooks to reproduce active learning result for each batch (including all data in the initial training data).
2. `notebooks/active-learning_only-LFP-data`: Contains `active_learning_batch_*.ipynb` files for each batch. Run the notebooks to reproduce active learning result for each batch (including all data in the initial training data).
3. `notebooks/screening`: Contains notebooks for screening original unlabeled repositories (eMolecules, PubChem) based on undesired chemical moeities, synthesizability, & ionic conductivity
4. `notebooks/manuscript-plots`: Contains notebooks for reproducing figures in the main text

## Model checkpoints
All trained model checkpoints are stored inside directory `models/batch-*` containing four files named `pairwise_batch*.pkl`, `rq_batch*.pkl`, `matern_batch*.pkl`, and `rbf-ess_batch*.pkl` for each of the four surrogate models in each batch used in this study.

## How to Run
Follow these steps to run the notebooks:

1. Clone the repository:
   ```bash
   git clone https://github.com/AmanchukwuLab/AL-anode-free
   cd AL-anode-free
   ```

2. Create virutal environment, install the required dependencies, and activate the virtual environment:
   ```bash
   conda env create -f environment.yaml
   conda activate al_afb
   ```

3. Launch Jupyter Notebook:
   ```bash
   jupyter notebook
   ```

4. Open the notebooks from the `notebooks` directory and run them cell-by-cell.

## Dependencies
The following libraries are required:
- Python 3.9+
- Jupyter Notebook
- Pandas
- NumPy
- Scipy
- Scikit Learn
- Pickle
- Matplotlib

Install the required libraries using the provided `requirements.txt` file.

## Citation
Please consider citing this work if you use our datasets or codes:
```plaintext
@article{ma2025active,
  title={Active learning accelerates electrolyte solvent screening for anode-free lithium metal batteries},
  author={Ma, Peiyuan, and Kumar, Ritesh and Wang, Ke-Hsin, and Amanchukwu, Chibueze V.},
  journal={Nature Communications},
  year={2025},
  volume={16},
  pages={8396},
  doi={https://doi.org/10.1038/s41467-025-63303-7}
}
```
