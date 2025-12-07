# SAM3DObjects Wheels

Pre-built CUDA extension wheels for [ComfyUI-SAM3DObjects](https://github.com/PozzettiAndrea/ComfyUI-SAM3DObjects).

These wheels provide GPU-accelerated 3D rendering without requiring users to compile CUDA extensions themselves.

## Packages

| Package | Description | Source |
|---------|-------------|--------|
| gsplat | Gaussian Splatting rasterization | [nerfstudio-project/gsplat](https://github.com/nerfstudio-project/gsplat) |
| nvdiffrast | Differentiable rendering | [NVlabs/nvdiffrast](https://github.com/NVlabs/nvdiffrast) |

## Installation

### Automatic (Recommended)

The easiest way is through ComfyUI-SAM3DObjects's installer - it auto-detects your GPU and installs the right wheels:

```bash
cd ComfyUI/custom_nodes/ComfyUI-SAM3DObjects
python install.py
```

### Manual Installation

```bash
# CUDA 12.8 + PyTorch 2.8.x (required for RTX 50 series, works for all)
pip install gsplat nvdiffrast --find-links https://pozzettiandrea.github.io/sam3dobjects-wheels/cu128/
```

## Available Builds

| CUDA | PyTorch | Python | Linux | Windows | RTX 50 Support |
|------|---------|--------|-------|---------|----------------|
| 12.8 | 2.8.1 | 3.10, 3.11, 3.12 | ✅ | ✅ | ✅ |

## GPU Architecture Support

Wheels are compiled for the following CUDA architectures:

| Compute Capability | Architecture | GPUs |
|--------------------|--------------|------|
| SM 7.5 | Turing | RTX 20 series |
| SM 8.6 | Ampere | RTX 30 series |
| SM 8.9 | Ada Lovelace | RTX 40 series |
| SM 9.0 | Hopper | H100 |
| SM 12.0 | Blackwell | RTX 50 series |

## Why Pre-built Wheels?

Building CUDA extensions requires:
- CUDA Toolkit with nvcc compiler
- C++ compiler (Visual Studio on Windows)
- Matching versions of everything

Many users hit compilation errors. These pre-built wheels skip all that complexity.

## Building Locally

If you need a specific configuration not provided here:

```bash
# Clone the source repos
git clone https://github.com/nerfstudio-project/gsplat.git
git clone https://github.com/NVlabs/nvdiffrast.git

# Set your GPU architecture (e.g., 8.9 for RTX 40 series, 12.0 for RTX 50 series)
export TORCH_CUDA_ARCH_LIST="8.9;12.0"

# Build
cd gsplat && pip install . && cd ..
cd nvdiffrast && pip install . && cd ..
```

## License

- gsplat: Apache-2.0
- nvdiffrast: NVIDIA License

## Related

- [ComfyUI-SAM3DObjects](https://github.com/PozzettiAndrea/ComfyUI-SAM3DObjects) - The main SAM3DObjects custom node
- [SAM 3D Objects](https://github.com/facebookresearch/sam-3d-objects) - Original SAM3D by Meta AI
