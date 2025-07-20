# FeatOptGS: Feature-Optimized 3D Gaussian Splatting for Sparse-View Synthesis

[Ning Xing](https://orcid.org/), [Zhongkang Zhang](https://orcid.org/0009-0004-0933-3853), [Catarina Moreira](https://orcid.org/), [Joaquim Jorge](https://orcid.org/)

## Overview

FeatOptGS introduces a novel method for enhancing 3D reconstruction and novel view synthesis under sparse-view conditions. By combining innovative image decomposition feature extraction, geometric consistency optimization, and Gaussian ellipsoid splitting mechanisms, FeatOptGS significantly improves rendering clarity and accuracy, addressing issues of detail loss and blur in traditional Gaussian ellipsoids. Our method demonstrates superior performance in complex scenes, maintaining high rendering quality and inference speed across various resolutions and training viewpoints.

## Features

- **Sparse-View Synthesis**: Effectively enhances 3D reconstruction quality from a limited number of input views.
- **Image Decomposition**: Utilizes albedo, shading, and residual decomposition to eliminate lighting discrepancies and improve geometric alignment.
- **Gaussian Refinement**: Introduces adaptive Gaussian ellipsoid splitting to refine large ellipsoids, reducing rendering blur and improving detail retention.
- **Geometric Consistency**: Ensures spatial consistency across views through advanced feature extraction and matching priors.

> ⭐️ **Update:**
- **2025/7/20** Results, including optimized models and rendered images, are now available at [this link](https://pan.baidu.com/s/1poWYaOQ-K1NSb7ojkuU7LQ?pwd=aamt). (This link contains some results and image decomposition results, and will continue to be updated in the future.)



## Installation

### Prerequisites

We recommend setting up the environment on a machine with the following configurations:

- **Operating System**: Ubuntu 18.04 (other similar configurations may work)
- **CUDA**: 11.6
- **GCC**: 9.4.0

### Steps

1. **Clone the Repository**

   ```bash
   git clone https://github.com/ZhongkangZ/FeatOptGS.git --recursive
   cd FeatOptGS


2. **Install Dependencies**

   Set up the environment by installing dependencies via `conda`.

   ```bash
   conda env create --file environment.yml
   conda activate featoptgs

### Dataset

For data, you can either use public datasets or prepare your own.

#### 1. **LLFF Dataset**

* **Download LLFF from the official link**: [Google Drive Link](https://drive.google.com/drive/folders/128yBriW1IG_3NJ5Rp7APSTZsJqdJdfc1).
* **Unzip the dataset** to `<your LLFF path>`.

The structure should look like:

```
LLFF/
├── fern/
│   ├── images/
│   │   ├── IMG_4026.JPG
│   │   ├── IMG_4027.JPG
│   │   ├── ...
│   ├── sparse/
│       └── 0/
├── flower/
│   ├── images/
│   │   ├── IMG_2962.JPG
│   │   ├── IMG_2963.JPG
│   │   ├── ...
│   ├── sparse/
│       └── 0/
```

#### 2. **DTU Dataset**

* **Download DTU Rectified (123 GB)** from the official website: [DTU Rectified](https://roboimagedata.compute.dtu.dk/?page_id=36/).
* **Unzip the dataset** to `<your DTU_Rectified path>`.

The dataset structure should look like:

```
DTU/
├── Rectified/
│   ├── scan1/
│   │   ├── images/
│   │   │   ├── rect_001_0_r5000.jpg
│   │   │   ├── rect_001_1_r5000.jpg
│   │   │   ├── ...
│   │   ├── sparse/
│   │       └── 0/
│   ├── scan2/
│   │   ├── images/
│   │   │   ├── rect_001_0_r5000.jpg
│   │   │   ├── rect_001_1_r5000.jpg
│   │   │   ├── ...
│   │   ├── sparse/
│   │       └── 0/
```

#### 3. **Image Decomposition Results**

You can obtain image decomposition results from [Marigold](https://github.com/prs-eth/marigold). For more information, check the Marigold repository and the setup instructions.

```bash
git clone https://github.com/prs-eth/marigold.git
cd marigold
```

Follow the instructions in their [README](https://github.com/prs-eth/marigold) to extract albedo, shading, and residual maps for your images.

## Training

### Training Multiple Scenes

To train multiple scenes in parallel, use the provided batch training scripts:

* For example:

  ```bash
  bash train_batch.sh
  ```

### Training a Single Scene

For training a single scene, configure the parameters in `single_train.sh` and run it:

```bash
bash ./single_train.sh
```

### Configurations

* **scene**: Path to your scene data.
* **exp\_name**: Name for the experiment.
* **gpu**: Specify which GPU to use.

### Evaluation

After training, results will be saved automatically in the log directory. You can manually render and compute metrics with the following commands:

```bash
python render.py -m <path to trained model> # Generate renderings
python metrics.py -m <path to trained model> # Compute error metrics
```

## Acknowledgements

We thank all authors and contributors for their efforts in making this project possible.
