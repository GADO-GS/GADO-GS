# GADO-GS

Project page for **GADO-GS: Geometry-Appearance Decoupled Optimization for Efficient and Compact 3D Gaussian Splatting**.

Project homepage: <https://gado-gs.github.io/GADO-GS/>

## Overview

GADO-GS is a structure-first training framework for efficient and compact 3D Gaussian Splatting. It coordinates three training-time mechanisms within the standard 3DGS pipeline:

- **GADO** applies role-specific update schedules to geometry-related and appearance parameters.
- **PSA** progressively activates higher-order spherical-harmonic bands.
- **VGC** derives a per-Gaussian discrepancy between projected-center depth and auxiliary-view rendered-surface depth. The discrepancy contributes to consistency regularization and VGC-gated adaptive density evolution.

The inference-time Gaussian representation and rasterizer remain unchanged.

## Quantitative summary

The values below are dataset-level averages reported in the manuscript. Each pair is shown as **3DGS / GADO-GS**; full SSIM and LPIPS results are available in the project page tables.

| Benchmark | PSNR (dB) | Training time (s) | Peak VRAM (MB) | Rendering FPS | Model size (MB) | Gaussians |
| --- | ---: | ---: | ---: | ---: | ---: | ---: |
| Mip-NeRF 360 | 27.48 / 27.49 | 2072.9 / 180.7 | 12344.9 / 6049.1 | 123.3 / 892.3 | 646.4 / 89.0 | 2733K / 362K |
| Tanks & Temples | 23.80 / 24.19 | 1022.8 / 149.6 | 7020.0 / 3914.0 | 175.4 / 996.0 | 372.2 / 57.3 | 1574K / 242K |
| Deep Blending | 29.76 / 29.85 | 1690.8 / 140.5 | 12147.0 / 5445.0 | 129.8 / 1127.5 | 587.6 / 51.8 | 2484K / 219K |

Across these benchmarks, GADO-GS reduces training time by a factor of 10.1, increases rendering throughput by a factor of 7.2, and reduces model storage by a factor of 8.4 relative to vanilla 3DGS.

## Training protocol

All benchmark runs use a fixed 30,000-iteration protocol. During GADO-GS training, each iteration samples one primary RGB view and two neighboring auxiliary views. PSA activates SH degrees 1, 2, and 3 at iterations 1,000, 2,000, and 3,000, respectively. VGC uses auxiliary-view rendered-surface depth to form its consistency signal and to gate density evolution; inference still uses the standard 3DGS Gaussian representation and rasterizer.

## Repository contents

This repository contains the project page and its visual assets, including the method overview, progressive SH visualization, quantitative comparisons, ablations, and qualitative results. The implementation will be released through the project homepage upon paper acceptance.

## Local preview

Serve this directory with any static HTTP server and open `index.html`. For example:

```bash
python -m http.server 8000
```

Then open <http://127.0.0.1:8000/> in a browser.
