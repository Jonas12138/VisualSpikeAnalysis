# Data and feature notes

## Source

- Dataset: Allen Institute Visual Coding-Neuropixels.
- [Dataset documentation](https://allensdk.readthedocs.io/en/latest/visual_coding_neuropixels.html)
- [Access instructions](https://allensdk.readthedocs.io/en/latest/_static/examples/nb/ecephys_data_access.html)
- Download status: not recorded yet.
- Local cache directory: to be recorded; suggested location `data/raw/`.
- Access date, AllenSDK version, and source file checksum: to be recorded after download.
- Follow the dataset's usage and citation guidance when distributing results or data.

## What the data mean

The processed NWB data include spike timestamps assigned to recorded units and a table identifying stimulus presentations and their timing. A unit is an estimated source of spikes, not a guaranteed perfectly isolated neuron.

For this project:

| Item | Meaning |
| --- | --- |
| One sample | One presentation of a selected natural image |
| One feature | One selected unit's spike count in the response window |
| `X` | Numeric matrix, presentations by units |
| `y` | Image ID for each presentation; IDs are categorical labels |
| Timestamp units | Seconds |
| Feature units | Spike count; optional rates must be explicitly labeled spikes/second |

## Selection record

| Setting | Planned or selected value |
| --- | --- |
| Session ID | TBD |
| Session type | Verify `brain_observatory_1.1` |
| Region | VISp |
| Stimulus table | `natural_scenes` |
| Image IDs | TBD; exclude blank/invalid stimulus entries |
| Image-selection rule | TBD; choose before inspecting decoder accuracy |
| Unit quality filters | TBD; record explicit thresholds and whether SDK defaults were used |
| Ordered unit IDs | Save locally and record the path |
| Response window | TBD; specify seconds relative to stimulus onset |
| Number of presentations per class | TBD |
| Number of units | TBD |

## Feature construction

For presentation `i`, count each selected unit's spikes in the half-open interval `[onset_i + start_offset, onset_i + end_offset)`.

- Use the same window duration for every sample, unless a different representation is explicitly justified.
- Verify that the window fits the intended stimulus interval and does not accidentally include the next stimulus.
- Preserve presentations and units with zero counts.
- Align labels by presentation ID; do not assume independent table row orders match.
- Keep the column-to-unit mapping fixed across training, validation, and prediction.
- Record any missing-data exclusions and the resulting class counts.
- If temporal bins are introduced, record bin edges and feature ordering.
- Any label-driven unit selection, learned normalization, or dimensionality reduction must use training data only.

## Evaluation split

Status: not selected or saved yet.

Record the intended claim, partition procedure, seed if relevant, counts per class, and paths to saved presentation IDs. Use a development split for model selection and keep a final test partition untouched.

- Keep all windows/bins from the same presentation in one partition.
- Decide how temporally related presentations are handled; record block boundaries or any exclusion gap used.
- Verify each partition contains both selected classes and no duplicate presentation IDs.
- Random presentation splits estimate within-session performance under that sampling scheme. A later time-block holdout gives a different check of stability over time.
- Repeated presentations of the same image can appear in different partitions because the task is recognizing known image classes on new presentations. This does not test decoding unseen image identities.
- Do not concatenate different sessions' units as if they were the same feature columns.

Suggested local files, created by future analysis:

```text
data/processed/splits.json
data/processed/unit_ids.json
data/processed/features.npz
```

Record exact paths and regeneration steps in the relevant experiment entry. These files are ignored by Git by default; back them up separately if they cannot be regenerated exactly.

## Checks to record after preparation

- [ ] Timestamps align with stimulus onset.
- [ ] Feature rows and labels match by presentation ID.
- [ ] No invalid/blank labels are included.
- [ ] Zero-spike samples remain present.
- [ ] All partitions have both classes and are disjoint.
- [ ] Unit count, feature count, and class counts are recorded.
