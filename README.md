# NeRF & Gaussian Splatting 3D Reconstruction

Reconstruct a 3D scene from multi-view photos using neural radiance fields (Nerfacto) and 3D Gaussian Splatting (Splatfacto) via [nerfstudio](https://docs.nerf.studio/).

## Results
### Nerfacto Spiral Render (30K iterations)

https://github.com/user-attachments/assets/8778fd70-6a7f-4707-97ad-dc42df44be03

## Pipeline

1. **Capture** — 50 photos of an indoor scene from different angles
2. **COLMAP** — Structure-from-Motion to estimate camera poses
3. **Data Processing** — `ns-process-data` to generate multi-resolution images + `transforms.json`
4. **Training** — Nerfacto (30K iter, ~3.5h on T4) / Splatfacto
5. **Rendering** — Spiral camera path → novel view video
6. **Evaluation** — PSNR, SSIM, LPIPS

## Data

- 23 frames, 5712×4284, OPENCV camera model
- Multi-resolution: 1x, 1/2, 1/4, 1/8
- COLMAP sparse reconstruction + point cloud

## Quick Start

Open `NeRF_Gaussian_Reconstruction_Final.ipynb` in Google Colab with a **GPU runtime (T4)**.

The notebook handles environment setup, patches for Colab compatibility (Python 3.12 + PyTorch 2.6), training, rendering, and evaluation.

### Colab Patches (documented in notebook)
- `torch.compile` → no-op (crashes on Python 3.12+)
- `torch.load` → `weights_only=False` (PyTorch 2.6+ default change)
- `tiny-cuda-nn` required (without it renders are blank)

## Project Structure
```
├── NeRF_Gaussian_Reconstruction_Final.ipynb   # main notebook
├── results/
│   └── nerfacto_spiral.mp4                    # rendered video
└── README.md
```

## Tools

- [nerfstudio](https://github.com/nerfstudio-project/nerfstudio) 1.1.5
- [COLMAP](https://colmap.github.io/)
- [tiny-cuda-nn](https://github.com/NVlabs/tiny-cuda-nn)
- PyTorch 2.2.2 + CUDA 11.8

## Author

Yuxi Yang






