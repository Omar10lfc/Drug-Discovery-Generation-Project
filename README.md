# Generative Models for Drug Discovery Project – Detailed Workflow

## 1. Project Introduction
This project investigates the use of deep generative models to create novel molecules with desirable properties for drug discovery. The workflow leverages the QM9 dataset and explores several neural network architectures, including Diffrent types of Autoencoders (AEs) and Variational Autoencoders (VAEs).

## 2. Environment Setup
- **Imports:** Essential libraries for data handling (NumPy, pandas), visualization (matplotlib, seaborn), cheminformatics (RDKit), machine learning (PyTorch, torch-geometric, scikit-learn), and utility functions.
- **Device Selection:** Automatically uses GPU (CUDA) if available for faster computation.

## 3. Data Acquisition and Preprocessing
- **Dataset:** QM9, a quantum chemistry dataset with 130k+ small organic molecules, each represented by a SMILES string and annotated with quantum chemical properties.
- **Loading:** Uses `torch_geometric.datasets.QM9` to download and load the dataset.
- **Preprocessing:**
  - Converts molecular graph data to SMILES strings.
  - Extracts properties: HOMO, LUMO, gap, number of atoms, molecular weight, and logP.
  - Stores processed data in a CSV file (`data/qm9_processed.csv`).

## 4. Exploratory Data Analysis (EDA)
- **Data Inspection:**
  - Displays the first few rows of the processed dataset.
  - Summarizes dataset shape and descriptive statistics (mean, std, min, max for each property).
  - Checks for missing values (none found).
- **Feature Explanation:**
  - **SMILES:** Text representation of molecular structure.
  - **HOMO/LUMO:** Quantum chemical properties related to electron donation/acceptance.
  - **Gap:** Energy difference between HOMO and LUMO (stability/reactivity).
  - **num_atoms, molecular_weight, logP:** Basic molecular descriptors relevant to drug-likeness.

## 5. Model Building
- **Model Types:**
  - **Standard VAE:** Learns a latent representation to generate new molecules.
  - **Conditional VAE:** Generates molecules conditioned on specific properties.
  - **Sparse Autoencoder:** Encourages sparse latent representations for interpretability.
  - **Denoising Autoencoder:** Learns to reconstruct molecules from noisy inputs, improving robustness.
- **Implementation:**
  - Models are built using PyTorch, with custom encoder/decoder architectures suitable for molecular data.
  - Data is split into training and test sets, and features are scaled as needed.

## 6. Training and Evaluation
- **Training:**
  - Each model is trained to minimize reconstruction loss (and KL divergence for VAEs).
  - Training progress is monitored and visualized.
- **Evaluation Metrics:**
  - **Validity Rate:** Percentage of generated molecules that are chemically valid.
  - **Property Prediction Error:** Measures how well generated molecules match target properties.
  - **Pairwise Similarity:** Assesses diversity among generated molecules.
- **Results:**
  - All models achieve 100% validity.
  - Denoising AE has the lowest property prediction error but less diversity.
  - Sparse AE and Conditional VAE offer a balance between accuracy and diversity.

## 7. Visualization
- **Plots:**
  - Training/validation loss curves.
  - Property distributions for generated vs. real molecules.
  - Example molecular structures generated by each model.

## 8. File Structure
- `Project4_Drug_Discovery_Generation_Notebook.ipynb`: Main notebook with all code and analysis.
- `data/qm9_processed.csv`: Preprocessed dataset for modeling.
- `data/qm9/`: Directory containing raw and processed QM9 data files.

## 9. How to Run
1. Install all required dependencies (see imports at the top of the notebook).
2. Run the notebook cells sequentially. The dataset will be downloaded and processed automatically.
3. Review outputs, plots, and generated molecules in each section.

## 10. References
- [QM9 Dataset](https://deepchemdata.s3-us-west-1.amazonaws.com/datasets/molnet_publish/qm9.zip)
- [RDKit](https://www.rdkit.org/)
- [PyTorch](https://pytorch.org/)
- [torch-geometric](https://pytorch-geometric.readthedocs.io/)
