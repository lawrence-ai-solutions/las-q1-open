# LAS-Q1 Open: lessons and Twin Check

Open teaching material and an open benchmark from **LAS-Q1 Studio**, a quantum-computer emulator calibrated to real hardware,
by Lawrence AI Solutions (James Lawrence, ORCID [0009-0002-6891-1604](https://orcid.org/0009-0002-6891-1604)).

Every lesson and every number here is tied to an experiment that was run on a real 156-qubit superconducting processor, with
the prediction saved **before** the run. Anyone can check the claims, and anyone can test their own noise model on the same data.

## What's here
| Folder | What it is | Licence |
|---|---|---|
| [`lessons/`](lessons/) | 5 open lessons (Bell test, teleportation, Grover search, quantum Zeno effect, 12-qubit entanglement): teacher guide with answers + student worksheet | CC BY 4.0 |
| [`notebooks/twin_check.ipynb`](notebooks/twin_check.ipynb) | Downloads the public datasets and compares 49 predictions with real-hardware measurements; verifies the pre-registration hashes; **test your own noise model** on the same chip-compiled circuits (a standard Qiskit Aer model is included as the starting point) | MIT |

[![Open in Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/lawrence-ai-solutions/las-q1-open/blob/main/notebooks/twin_check.ipynb)
Run the notebook in Google Colab with no install (button above), or locally with `pip install -r requirements.txt` then `jupyter notebook`.

## Data (permanent, citable)
- Experiments dataset, 23 experiments, Nov 2026: https://doi.org/10.5281/zenodo.24517586
- Warp-drive analogue preprint and data: https://doi.org/10.5281/zenodo.24517295

## What is open and what is not
Open: the lessons, the notebook, the predictions (as numbers), the measured results, the compiled circuits and the
submission scripts. **Predictions are published as data; the prediction engine is not part of this release.** LAS-Q1 Studio
itself (the emulator and its noise model) is commercial software; school licences fund its upkeep and new lessons.

## Cite
Lawrence, J. (2026). *Pre-registered quantum hardware experiments (November 2026)*. Zenodo. https://doi.org/10.5281/zenodo.24517586

Independent project; not affiliated with or endorsed by IBM. Real-hardware results were obtained on IBM Quantum processors;
model predictions are labelled as such.
