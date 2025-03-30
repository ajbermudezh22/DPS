# Replication of Diffusion Posterior Sampling (DPS) for General Noisy Inverse Problems

This repository contains the implementation and replication efforts for the paper [**"Diffusion Posterior Sampling for General Noisy Inverse Problems"**](https://arxiv.org/abs/2209.14687) (ICLR 2023 Spotlight), originally developed by Chung et al. [Official GitHub Repository](https://github.com/DPS2022/diffusion-posterior-sampling).

> 📍 This was developed as a group project (3 people) for the **Project Machine Learning** course at **TU Berlin (Winter Semester 2024/25)**.

---

## 🧠 Project Overview

The goal of our project was to **replicate and evaluate** the DPS method proposed in the paper. DPS is a novel framework that combines diffusion models with posterior sampling techniques to tackle general (non)linear noisy inverse problems — a setting where traditional projection-based methods often fail.

We explored its application to the following image reconstruction tasks:

### ✅ Linear inverse problems:
- **Image Inpainting**
- **Gaussian Deblurring**
- **Super Resolution**

### ⚠️ Non-linear inverse problems:
- **Motion Deblurring**
- **Phase Retrieval**

---

## 🔧 What We Did

- Re-implemented the pipeline based on the original DPS repository, focusing on modifying `train_apply.py` to cover training and inference tasks.
- Used the pre-trained checkpoint `ffhq_10m.pt` provided by the original authors for better performance.
- Integrated the official `unet.py` diffusion model for high-quality sampling and inference (replacing our earlier, minimalistic version from Milestone 2).
- Ran evaluations on multiple tasks using degraded inputs and visual + numerical comparison with the ground truth.

---

## 📈 Results Summary

| Task               | Quality of Reconstruction | Comments |
|--------------------|----------------------------|----------|
| **Inpainting**     | ✅ Excellent                | Close to original DPS paper |
| **Gaussian Blur**  | ✅ Excellent                | Sharp reconstructions, low error |
| **Super Resolution** | ✅ Very Good              | Mostly preserved detail |
| **Motion Deblurring** | ⚠️ Weak                 | Struggled due to nonlinearities |
| **Phase Retrieval**  | ⚠️ Poor                  | Highly unstable results |

---

## 📷 Visual Examples

### Example – Inpainting

| Label (GT) | Input (Masked) | Recon (DPS) |
|------------|----------------|-------------|
| ![](./figures/label/00000.png) | ![](./figures/inpainting_input/00000.png) | ![](./figures/inpainting_recon/00000.png) |

### Example – Gaussian Deblur

| Label (GT) | Input (Blurred) | Recon (DPS) |
|------------|------------------|-------------|
| ![](./figures/label/00001.png) | ![](./figures/gb_input/00001.png) | ![](./figures/gb_recon/00001.png) |

### Example – Phase Retrieval (Nonlinear)

| Label (GT) | Input (FFT phase) | Recon (DPS) |
|------------|-------------------|-------------|
| ![](./figures/label/00005.png) | ![](./figures/pr_input/00005.png) | ![](./figures/pr_recon/00005.png) |

---

## 💡 Key Takeaways

- **Linear tasks** (inpainting, blur, super-res) were well-handled and produced **high-fidelity reconstructions**.
- **Non-linear tasks**, particularly motion blur and phase retrieval, were **challenging** — likely due to limitations in the approximations within the DPS framework and the lack of exact measurement models.
- Using the **official checkpoint and UNet implementation** was a game changer compared to our earlier minimal diffusion model and shallow training.
- The model **relies on knowing the forward operator** of the degradation process, which limits its use in unknown or real-world noisy data.

---

## 📎 References

Original DPS Paper: [https://arxiv.org/abs/2209.14687](https://arxiv.org/abs/2209.14687)  
Official Repository: [https://github.com/DPS2022/diffusion-posterior-sampling](https://github.com/DPS2022/diffusion-posterior-sampling)

If you found this helpful or want to cite the original work:

```bibtex
@inproceedings{
chung2023diffusion,
title={Diffusion Posterior Sampling for General Noisy Inverse Problems},
author={Hyungjin Chung and Jeongsol Kim and Michael Thompson Mccann and Marc Louis Klasky and Jong Chul Ye},
booktitle={The Eleventh International Conference on Learning Representations },
year={2023},
url={https://openreview.net/forum?id=OnD9zGAGT0k}
}
