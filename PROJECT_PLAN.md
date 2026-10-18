# Project plan

## Question and scope

Can neural spike counts predict which of two predefined natural images was presented, on held-out presentations from one mouse recording session?

Initial scope:

- Dataset: Allen Visual Coding-Neuropixels.
- Session: one `brain_observatory_1.1` session, to be selected and recorded in `DATA.md`.
- Region: primary visual cortex (`VISp`).
- Labels: two natural-image IDs, chosen using a documented rule before examining decoding performance.
- Features: one spike count per selected unit in a fixed response window.
- Baselines: majority-class predictor and linear SVM.
- Extension: compare an RBF SVM using the same data and evaluation protocol.
- Output: one image-class prediction per held-out presentation.

This project measures offline decoding of presented stimuli. It does not establish online device control or transfer to humans, other mice, or new sessions.

## Milestones

### 1. Define the data and evaluation

- [ ] Select the session and verify that it includes natural scenes and VISp units.
- [ ] Choose the two image IDs using a rule independent of decoding results.
- [ ] Record the response window and unit quality filters.
- [ ] Define training, validation, and final test partitions before model comparisons.
- [ ] Save actual presentation IDs and verify both classes are represented in each partition.

Done when `DATA.md` contains the selected settings and split rules, with saved split IDs.

### 2. Inspect the recordings

- [ ] Plot a spike raster aligned to stimulus onset.
- [ ] Plot average stimulus-aligned responses.
- [ ] Check units, stimulus durations, missing labels, and zero-spike presentations.
- [ ] Explain what one feature row and its target represent.

Done when a notebook can reproduce the plots and alignment checks.

### 3. Build a baseline

- [ ] Construct `X` and `y`, preserving zero-spike presentations.
- [ ] Check row/label alignment and consistent unit ordering.
- [ ] Fit a majority-class predictor using the training labels.
- [ ] Fit a linear SVM with training-only preprocessing.
- [ ] Record validation accuracy, balanced accuracy, and a confusion matrix.
- [ ] Run a shuffled-label control without consulting final test performance.

Done when experiment E001 has an actual completed record and reproducible outputs.

### 4. Compare controlled experiments

- [ ] Tune linear-SVM `C` using training/validation data only.
- [ ] Compare RBF, tuning `C` and `gamma` without touching the final test set.
- [ ] Optionally investigate feature windows or unit count, changing one main factor at a time.
- [ ] Record unsuccessful experiments as well as improvements.

Done when the chosen pipeline and selection criterion are documented.

### 5. Evaluate and report

- [ ] Freeze preprocessing, features, and model settings.
- [ ] Refit on the permitted development data and evaluate on the reserved test partition.
- [ ] Report sample counts, class balance, baseline results, and uncertainty or clear sample-size limitations.
- [ ] Add the test confusion matrix and conclusions to `RESULTS.md`.
- [ ] Explain generalization limits and possible behavioral or timing confounds.

Done when the conclusions match the actual evaluation and scope.

### 6. Reproduce the project

- [ ] Record working dependency versions and the code commit.
- [ ] Save split IDs, ordered unit IDs, settings, and artifact paths.
- [ ] Restart the notebook kernel and run all cells in order, or rerun the analysis script.
- [ ] Update the README with the verified run procedure.

## Working style

Choose one small task at a time. Before each experiment, write the question and planned change. Afterward, record what happened and the next step. Use Git commits at useful milestones.

## Decisions still to make

- Recording session ID and image IDs.
- Response window and unit quality thresholds.
- Partition boundaries and whether an additional time-block robustness check is feasible.
- Hyperparameter search ranges and model-selection metric.

No choices above should be presented as completed experiments until the corresponding run has happened.
