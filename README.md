# COCO → Skyless Dataset (Detectron2)

This project automatically removes the **sky** from COCO images using Detectron2 panoptic segmentation, then rebuilds the dataset with updated COCO annotations.  
It demonstrates both **instance segmentation** and **panoptic segmentation** in practice.

---

## Installation

Tested on **Python 3.10 / 3.12**, Torch 2.8, CUDA 12.x (GPU optional).

```bash
# Clone this repository
git clone <Assignment-COCO-Detectron2-Skyless>
cd coco-skyless

# Install dependencies
pip install -r requirements.txt
```

Or manually:

```bash
pip install opencv-python pycocotools tqdm numpy pillow pyyaml matplotlib pandas pytz
pip install torch torchvision --index-url https://download.pytorch.org/whl/cu121
pip install 'git+https://github.com/facebookresearch/detectron2.git'
```

---

## Folder Structure

```
coco-skyless/
├─ data/
│  ├─ coco/       # Original COCO images + annotations
│  ├─ subset/     # Outdoor subset
│  └─ skyless/    # Cropped skyless images + annotations
└─ outputs/
   ├─ instances_demo/   # Mask R-CNN demo overlays
   └─ pairs/            # Side-by-side: Original vs Skyless + New annotations
```

---

## Usage

1. Open **COCO_Skyless_Assignment.ipynb** in Google Colab (GPU recommended).
2. (Optional) Change runtime → GPU.
3. Run cells in order:
   - Install dependencies
   - Prepare folders
   - Download COCO val2017
   - Build outdoor subset (`MAX_IMAGES=50–200`)
   - Run instance + panoptic predictors
   - Skyless conversion → saves cropped images + new JSON
   - Validation demos & side-by-side pairs

Outputs are written to `outputs/`.

---

## Pipeline Summary

- **Instance Segmentation (Mask R-CNN):** detects and segments objects (people, cars, etc.)
- **Panoptic Segmentation (Panoptic FPN):** detects both objects and *stuff* like sky
- **Sky Removal:** crop image below the lowest detected sky pixel
- **Re-annotation:** adjust masks, bounding boxes, areas

---

## Example Results

- `outputs/instance_vs_panoptic.png`
- `outputs/pairs/…_pair.jpg` (side-by-side Original vs Skyless)

---

## Reporting

Each image is logged with:
- `status` (`ok`, `no_sky`, `no_anns`, `skip_small`)
- Skyline cut position
- Kept annotations count

---

## Authors

- Sakineh Abdollahzadeh

---

*Generated: 2025-09-04 18:35*
