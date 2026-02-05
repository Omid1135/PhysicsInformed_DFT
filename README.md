# Physics-Informed Modeling of Transferable Energetics in Substitutional Alloys

This repository contains the datasets and materials supporting the study:
**"Visualization-Driven Physics-Informed Modeling of Transferable Energetics in Substitutional Alloys"** (submitted to *Physical Review B*).

## Repository Overview

This repository hosts the primary datasets used to train and evaluate the physics-informed machine learning (PIML) models described in the manuscript. The accompanying core analysis and modeling Python code will be made publicly available upon initial acceptance of the manuscript.

## Dataset Description

The data is stored in two HDF5 files, each containing Density Functional Theory (DFT) calculated properties for different substitutional alloy systems on an identical, fixed lattice.

### 1. FeMn_configurational_dataset.hdf5
*   **Source System:** Fe/Mn substitutional alloy.
*   **Purpose:** Primary dataset for model training, validation, and the physics-guided visualization analysis.
*   **Contents:** 1,337 distinct chemical configurations.
*   **Key Quantities per Configuration:**
    *   `total_energy`: DFT total energy (in Ry).
    *   `absolute_magnetization`: Sum of the magnitudes of atomic magnetic moments (in μ_B).
    *   `total_magnetization`: Net sum of signed atomic magnetic moments (in μ_B).
    *   `site_occupation`: A vector encoding the chemical identity (`+1` for Fe, `-1` for Mn) for each of the 18 active substitutional sites.
    *   `configuration_id`: A unique identifier for each structure.

### 2. CoNi_transfer_dataset.hdf5
*   **Target System:** Co/Ni substitutional alloy (configurationally isomorphic to the Fe/Mn system).
*   **Purpose:** Evaluation dataset for zero-shot and few-shot transfer learning tests.
*   **Contents:** 96 distinct chemical configurations.
*   **Key Quantities per Configuration:** Includes the same properties as the Fe/Mn dataset (`total_energy`, `absolute_magnetization`, `total_magnetization`, `site_occupation`), enabling direct use of the physics-informed descriptor.

## File Structure & Access

Each HDF5 file is structured hierarchically. Configurations can be accessed by their `configuration_id` (e.g., `config_0012`). We provide a simple Python script (`example_load_data.py`) demonstrating how to load and inspect the data.

```python
import h5py

# Example: Load a specific configuration from the Fe/Mn dataset
with h5py.File('FeMn_configurational_dataset.hdf5', 'r') as f:
    config = f['config_0100']
    energy = config['total_energy'][()]
    occupation = config['site_occupation'][:]
    print(f"Energy: {energy} Ry")
    print(f"Site occupation vector: {occupation}")
Data Generation Procedure <!-- FIXED: Added `##` here -->
All DFT calculations were performed using the Quantum ESPRESSO package with consistent parameters:

Exchange-Correlation: PBE-GGA.

Pseudopotentials: GBRV ultrasoft.

Cutoffs: 40 Ry (wavefunctions), 400 Ry (charge density).

k-point grid: Monkhorst-Pack with ~0.2 Å⁻¹ spacing.

Spin Polarization: All calculations are spin-polarized. Magnetic moments were initialized in a site-dependent manner and relaxed self-consistently.

The atomic lattice and positions were kept fixed across all configurations; only the chemical occupation on the 18 active substitutional sites was varied.

Code Availability Note
The core Python scripts for physics-informed model training (linear and neural network), and the transfer learning evaluation (zero-shot/few-shot protocols) will be uploaded to this repository upon initial acceptance of the manuscript. This practice aligns with standard procedures to facilitate the peer-review process.

Citation
If you use these datasets in your research, please cite our manuscript (citation details will be updated upon publication).

License
The datasets in this repository are made available under a permissive license to encourage reuse in academic and commercial research.

For the data files (*.hdf5) and accompanying example scripts:
This work is licensed under the MIT License.
