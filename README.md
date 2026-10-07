# 3DGS Artifact QA Dataset

Sungkyunkwan University (SKKU)

[IMCLab](https://imclab.skku.edu/)

## Overview

This dataset is a collection of rendered videos designed for studying the perceptual quality of artifacts commonly observed in 3D Gaussian Splatting (3DGS) [1]. The source scenes were reconstructed using 3DGS, and two of the following artifact types were applied to each reconstruction before rendering it along a novel-view camera trajectory:

- **Blur**: A loss of high-frequency visual information, perceived as softened edges and reduced fine texture and detail. This produces a smoother but less detailed reconstruction.
- **Floater**: Erroneously reconstructed Gaussian primitives located away from the actual scene surfaces. They appear as isolated or disconnected structures suspended in free space.
- **Popping**: Abrupt, temporally discontinuous changes in visibility or blending during camera motion. In 3DGS, this can occur because splats are represented by a single view-space depth and globally sorted, allowing their compositing order to switch as the viewpoint changes.

Each filename identifies the scene, the two applied artifacts, and their respective intensity settings. The accompanying `scores.csv` file contains the subjective scores collected for the rendered videos.

## Dataset Information

The dataset contains three reconstructed scenes. The **Bicycle** scene originates from the Mip-NeRF 360 dataset [2], while the **Train** and **Truck** scenes originate from the Tanks and Temples benchmark [3].

| Scene | Source | Number of videos | Resolution | Frames per video | Frame rate | Duration |
|---|---|---:|---:|---:|---:|---:|
| Bicycle | Mip-NeRF 360 [2] | 13 | 1236 × 822 | 300 | 30 FPS | 10 s |
| Train | Tanks and Temples [3] | 13 | 1600 × 1000 | 300 | 30 FPS | 10 s |
| Truck | Tanks and Temples [3] | 13 | 1600 × 1000 | 300 | 30 FPS | 10 s |

### Artifact Configurations

Every rendered video contains exactly two artifact types. Although the intensity of each artifact is divided into five levels (1-5), only two levels per artifact were selected for this dataset:

| Artifact |  Levels used in this dataset |
|---|---|
| Blur |  2, 5 |
| Floater |  1, 3 |
| Popping |  2, 5 |

The numeric settings indicate the applied artifact intensity.

### File Naming Convention

```text
<scene>_<artifact-1>_<level-1>_<artifact-2>_<level-2>.mp4
```

For example, `bicycle_blur_2_floater_3.mp4` is a rendering of the Bicycle scene with blur at level 2 and floater artifacts at level 3.

### Directory Structure

```text
3DGS-Artifact-QA/
├── render/
│   ├── bicycle/    # 12 distorted videos + 1 reference video
│   ├── train/      # 12 distorted videos + 1 reference video
│   └── truck/      # 12 distorted videos + 1 reference video
├── scores.csv
└── README.md
```

### Subjective Scores

`scores.csv` contains ratings from 23 participants. The first column is the anonymized participant index, and each of the remaining 39 columns corresponds to a video filename. Scores range from 1 to 5.

> **Filename note:** the Train reference column in `scores.csv` is named `train_ref.mp4`, while the corresponding file is currently named `Train_ref.mp4`. Because filenames are case-sensitive on Linux, one of these names should be changed before using the dataset programmatically.

## References

[1] Kerbl, Bernhard, et al. "3d gaussian splatting for real-time radiance field rendering." ACM Trans. Graph. 42.4 (2023): 139-1.

[2] Barron, Jonathan T., et al. "Mip-nerf 360: Unbounded anti-aliased neural radiance fields." 2022 IEEE/CVF Conference on Computer Vision and Pattern Recognition (CVPR). IEEE, 2022.

[3] Knapitsch, Arno, et al. "Tanks and temples: Benchmarking large-scale scene reconstruction." ACM Transactions on Graphics (ToG) 36.4 (2017): 1-13.
