# Visual Spike Analysis

Learning neural decoding with Allen Institute Visual Coding-Neuropixels data and classical machine learning.

**Project question:** Can spike counts from primary visual cortex distinguish two predefined natural images on held-out presentations within one recording session?

**Status:** Documentation and experiment tracking are set up. This repository does not yet contain downloaded recordings, a trained decoder, or measured results.

## Start here

1. Read [the project plan](PROJECT_PLAN.md) for the scope and milestones.
2. Use [the data notes](DATA.md) to record the session, selected units, image labels, and split.
3. Follow [the experiment guide](EXPERIMENTS.md) when you run an experiment.
4. Put final findings in [the results report](RESULTS.md).

Your existing `Untitled.ipynb` is preserved. Use it to explore the data; move repeated preparation and modeling steps into Python functions as the project grows.

## Local setup

Open Anaconda Prompt. If your `allensdk` environment already works:

```bat
conda activate allensdk
cd /d D:\VisualSpikeAnalysis
jupyter lab
```

Select **Python (AllenSDK)** as the notebook kernel.

To create a new environment, use the starter recipe:

```bat
cd /d D:\VisualSpikeAnalysis
conda env create -f environment.yml
conda activate allensdk
python -m ipykernel install --user --name allensdk --display-name "Python (AllenSDK)"
jupyter lab
```

The environment recipe has not been installation-tested here and is not an exact dependency lock. If the named environment already exists, activate it instead of creating it again. After successful installation and import checks, capture the working versions:

```bat
conda env export --no-builds > environment-resolved.yml
```

Review the export before committing: remove a machine-specific `prefix:` line and check for private package URLs. The resolved export records the working packages for that machine; it does not guarantee compatibility on every operating system.

## Suggested project layout

```text
README.md                   Overview and setup
PROJECT_PLAN.md             Scope, tasks, and milestones
DATA.md                     Dataset and feature/split decisions
EXPERIMENTS.md              Experiment index and update instructions
RESULTS.md                  Final report (currently pending)
environment.yml             Starter environment recipe
experiments/                One Markdown record per experiment
Untitled.ipynb              Existing exploration notebook
data/                       Local recordings and derived arrays (ignored)
artifacts/                  Models and per-presentation predictions (ignored)
reports/figures/             Small figures suitable for Git
```

Create the local output folders when you need them. Keep raw recordings unchanged and download them separately from the code repository.

## What to save

- **In Git:** code, notebooks with reviewed outputs, documentation, environment files, small report figures, and experiment records.
- **Outside Git:** downloaded NWB recordings, derived feature arrays, models, and prediction files. Record their paths and regeneration instructions in the experiment record.
- For each run, save the presentation IDs used in each split, the ordered unit IDs, settings, seed, and code commit. A seed alone does not describe a split.

## First deliverable

A reproducible notebook or script that extracts spike counts, compares a majority-class predictor with a linear SVM, and reports validation performance. Final test evaluation happens after model selection.

## References

- [Allen Visual Coding-Neuropixels overview](https://allensdk.readthedocs.io/en/latest/visual_coding_neuropixels.html)
- [Allen quick-start notebook](https://allensdk.readthedocs.io/en/latest/_static/examples/nb/ecephys_quickstart.html)
- [Allen data-access tutorial](https://allensdk.readthedocs.io/en/latest/_static/examples/nb/ecephys_data_access.html)
- [scikit-learn: avoiding data leakage](https://scikit-learn.org/stable/common_pitfalls.html)
