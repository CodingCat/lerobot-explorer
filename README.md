# lerobot-explorer

A focused Jupyter notebook for inspecting LeRobot-style datasets end-to-end: layout discovery, schema and modality inspection, per-episode validation, and frame sampling with state/action overlays.

## What the notebook covers

- **Dataset overview**: Discover dataset root, chunks, episode parquet files, video keys, and meta files.
- **Data layout discovery**: Parse the on-disk layout and summarize what exists vs. what is missing.
- **Feature summary**: Read `meta/info.json` and surface high-level counts and feature keys.
- **Sanity check**: Validate episode coverage across parquet and video assets.
- **Schema**: Load metadata files (`info.json`, `modality.json`, `tasks.jsonl`, `episodes.jsonl`, `stats.json`, `relative_stats.json`) and preview their structure.
- **Feature table**: Build a per-feature schema table and infer storage (parquet vs. video).
- **Modality analysis**: Map logical modalities (state/action/annotation) to physical columns and storage.
- **Episode analysis**:
  - Locate parquet/video assets for a chosen episode.
  - Check step indices, task_index consistency, and basic stats.
  - Inspect state/action base columns.
  - Resolve task descriptions from `tasks.jsonl`.
  - Sample frames from videos and render step-level views.

## Requirements

- Python 3.10+
- Jupyter
- Core packages: `pandas`, `numpy`, `pyarrow`, `opencv-python`, `matplotlib`

## Usage

1. Open `lerobot-explorer.ipynb`.
2. Set `DATA_ROOT` to your dataset path.
3. Run cells top-to-bottom.
4. Optional: adjust `EPISODE_INDEX`, `VIDEO_KEY`, or sampling parameters in the Episode Analysis section.

## Dataset assumptions

The notebook expects a LeRobot-style layout:

```
<DATA_ROOT>/
  meta/
    info.json
    modality.json
    tasks.jsonl
    episodes.jsonl
    stats.json
    relative_stats.json
  data/
    chunk-*/
      episode_*.parquet
  videos/
    chunk-*/
      <video_key>/
        episode_*.mp4
```

If some files are missing, the notebook will still run but will skip related sections or show missing-file warnings.
