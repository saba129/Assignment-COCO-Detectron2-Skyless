# COCO → Skyless Dataset (Detectron2)

Create a **skyless** version of a COCO dataset split: automatically detect the **sky**, crop it out, and **rebuild COCO annotations** (bboxes, masks, areas). Includes inference demos, validation views, and a short report.

## Overview
- Downloads **COCO val2017** (images + `instances_val2017.json`).
- Builds a small **outdoor** subset (configurable).
- Runs **panoptic segmentation** to localize *sky* and crops **below the lowest sky pixel** (the skyline).
- **Re-annotates** the dataset (bbox/masks/areas) in valid COCO format.
- Validates with:
  - **Mask R-CNN** demo overlays.
  - Side-by-side views (original vs skyless) with updated annotations.
  - A compact **processing report** (success/skip/no-sky, etc.).

## Environment
- **Notebook:** Google Colab (GPU recommended; CPU works for small subsets)
- **Core libs:** `detectron2`, `torch/torchvision`, `opencv-python`, `pycocotools`, `numpy`, `matplotlib`, `tqdm`, `pandas`
- **Tested with:** Torch 2.8.x, CUDA 12.x, Python 3.12 (Colab)

## Data & Folder Layout
Default root: `BASE=/content/drive/MyDrive/coco-skyless`
coco-skyless/
├─ data/
│  ├─ coco/
│  │  ├─ images/val2017/
│  │  └─ annotations/instances_val2017.json
│  ├─ subset/
│  │  ├─ images/
│  │  └─ annotations/instances_subset.json
│  └─ skyless/
│     ├─ images/
│     └─ annotations/instances_skyless.json
└─ outputs/
   ├─ instances_demo/
   └─ pairs/

## Quickstart (Colab)
1. Change runtime to GPU (optional).
2. Run cells in order: install → folders → download COCO → subset → predictors → demos → skyless conversion → validators → report.

## Models & Why Both
- **Instance** (Mask R-CNN): object-level demos.
- **Panoptic** (Panoptic FPN): sky detection (stuff class) for cropping.

---
*Generated: 2025-09-04 17:44 by Sakineh Abdollahzadeh*
