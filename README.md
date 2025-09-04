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

## Installation

Tested on **Python 3.10 / 3.12**, Torch 2.8, CUDA 12.x (GPU optional).

```bash
# Clone this repository
git clone <your-repo-url>
cd coco-skyless

# Install dependencies
pip install -r requirements.txt
# or individually:
pip install opencv-python pycocotools tqdm numpy pillow pyyaml matplotlib pandas pytz
pip install torch torchvision --index-url https://download.pytorch.org/whl/cu121
pip install 'git+https://github.com/facebookresearch/detectron2.git'


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

## Usage

1. Open COCO_Skyless_Assignment.ipynb in Google Colab (GPU recommended).

2. (Optional) Change runtime → GPU.

3. Run cells in order:

* Install dependencies

* Prepare folders

* Download COCO val2017

* Build outdoor subset (MAX_IMAGES=50–200)

* Run instance + panoptic predictors

* Skyless conversion → saves cropped images + new JSON

* Validation demos & side-by-side pairs
Outputs are written to outputs/.


## Pipeline Summary

* Instance Segmentation (Mask R-CNN): detects and segments objects (people, cars, etc.)

* Panoptic Segmentation (Panoptic FPN): detects both objects and stuff like sky

* Sky Removal: crop image below the lowest detected sky pixel

* Re-annotation: adjust masks, bounding boxes, areas

## Example Results

* outputs/instance_vs_panoptic.png

* outputs/pairs/…_pair.jpg (side-by-side Original vs Skyless)

## Reporting

Each image is logged with:

* status (ok, no_sky, no_anns, skip_small)

* Skyline cut position

* Kept annotations count

## Authors

Sakineh Abdollahzadeh
---
*Generated: 2025-09-04 17:44*
