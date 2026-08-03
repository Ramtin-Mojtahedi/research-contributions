# Research contributions — fork snapshot

<!-- repository-guide:start -->
## Fork snapshot guide

This repository is a fork of `Project-MONAI/research-contributions`. It contains several independently versioned research prototypes rather than one application, one dependency environment, or one end-to-end pipeline. The original authorship, citations, and directory-level instructions remain authoritative for each contribution.

### Contents of this snapshot

| Directory | Published scope | Main entry points |
|---|---|---|
| `SwinUNETR/BRATS21` | A model-overview document for 3D brain-tumour segmentation with Swin UNETR | `README.md` only; no executable code is committed in this directory |
| `UNETR/BTCV` | UNETR training, fine-tuning, and sliding-window testing for BTCV multi-organ CT segmentation | `main.py`, `trainer.py`, `test.py` |
| `coplenet-pneumonia-lesion-segmentation` | Pretrained COPLE-Net inference demo for pneumonia-lesion segmentation | `run_inference.py`, `coplenet.py` |
| `lamp-automated-model-parallelism` | Model-parallel 3D U-Net training demo for head-and-neck segmentation | `train.py`, `unet_pipe.py`, `data_utils.py` |

### Dependency evidence is contribution-specific

| Contribution | Evidence in the committed files |
|---|---|
| `UNETR/BTCV` | `monai==0.7.0`, `nibabel==3.1.1`, `tqdm==4.59.0`, `einops==0.3.0`, `tensorboardX==2.1`; source also imports PyTorch, which is not pinned in that requirements file |
| COPLE-Net | README installs `monai[nibabel]==0.2.0`; source imports PyTorch, NumPy, MONAI, and nibabel-backed transforms; tests import `parameterized` |
| LAMP | README installs `monai==0.2.0` and `torchgpipe`; source imports PyTorch, NumPy, MONAI, and TorchGPipe; tests import `parameterized` |
| Swin UNETR / BRATS21 | No executable source or dependency manifest is committed in this snapshot |

The MONAI requirements conflict across contributions. A root-level combined requirements file would therefore be misleading.

### Contribution-level execution boundaries

- **UNETR/BTCV:** dataset JSON and NIfTI volumes are transformed by MONAI, trained with UNETR and Dice-based loss, saved as checkpoints, and evaluated with sliding-window inference and Dice scores.
- **COPLE-Net:** lung-cropped and normalized NIfTI inputs plus an external pretrained checkpoint are passed through sliding-window inference and written as segmentation outputs.
- **LAMP:** head-and-neck CT data and masks are augmented, passed through a U-Net partitioned with GPipe, optimized with Dice and focal losses, and evaluated with per-class Dice scores.
- **Swin UNETR / BRATS21:** the directory documents a model concept only; it does not contain a runnable workflow.

### Reproducibility and provenance boundary

- Datasets and pretrained weights are external to the repository and may require separate access or licensing.
- Each contribution targets its own historical MONAI environment and should be isolated from the others.
- This fork should not imply personal authorship of the upstream implementations. Preserve the original citations and contribution-level attribution when reusing any code.
- No single workflow diagram is provided because the four directories represent separate research artifacts with incompatible environments and different execution goals.
<!-- repository-guide:end -->

---

## Original upstream documentation

**MONAI Research Contributions** is a platform built to showcase cutting-edge research utilizing MONAI. This enables the community to see MONAI “in action” and  researchers to gain visibility for their MONAI-based work. The repository is regularly reviewed and selected contributions that have demonstrated their popularity or relevance can be integrated into MONAI components in a second step. Contributions are welcome! Simply follow the contribution guidelines stated below and file a pull request.

**Contribution Guidelines:**

1. Contributions are required to be published and have successfully undergone peer-review (If the contributing person is not the author of the work, no approval from the authors of the paper is required, but the contribution needs to be clearly labeled as a “Third-party contribution”). 

2. The implementation is required to feature MONAI components to a substantial extent. 
 
3. The implementation is required to include a boilerplate shell script (to be published) allowing code-reviewers to execute the code and reproduce the paper’s results with one click.

4. Under the hood, code quality does not have to match standards of the MONAI main repository, as the Research Contribution repository aims at a fast track for code change proposals and demonstrating cutting-edge research ideas. 

5. New contributions will be given a MONAI version tag (visible in the associated Readme) according to the utilized version of MONAI. This avoids the need to maintain compatibility of contributions for following MONAI releases.
