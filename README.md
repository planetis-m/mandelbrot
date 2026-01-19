# Mandelbrot Generator

A Vulkan compute shader example for generating Mandelbrot set images using Nim and GLSL.

This project demonstrates how to use Vulkan compute pipelines to generate fractal images on the GPU, leveraging the parallel processing capabilities of modern graphics hardware.

## Features

- **GPU-Accelerated Computation**: Uses Vulkan compute shaders for fast Mandelbrot set generation
- **High Performance**: Parallel processing across workgroups for efficient computation
- **Cosine Color Palette**: Beautiful color mapping using trigonometric functions
- **QOI Image Output**: Saves results in the efficient QOI (Quite OK Image) format
- **Debug Support**: Includes validation layers and RenderDoc integration for debugging

<img src="https://i.ibb.co/3mZ25Qds/mandelbrot.jpg" width="40%">

## Prerequisites

- **Nim**: Version 2.1.0 or later
- **Vulkan SDK**: Required for Vulkan API support
- **GLSLC**: Shader compiler from Vulkan SDK for compiling GLSL to SPIR-V
- **Graphics Card**: Vulkan-compatible GPU

## Building

1. **Install dependencies**:
   ```bash
   nimble install
   ```

2. **Build shaders**:
   ```bash
   nimble shaders
   ```
   This compiles the GLSL compute shader to SPIR-V format using `glslc`.

3. **Build the executable**:
   ```bash
   nim c -d:release --mm:arc src/main.nim
   ```

## Usage

Run the program with width and height parameters:

```bash
./main <width> <height>
```

For example, to generate a 1920x1080 image:

```bash
./main 1920 1080
```

The output will be saved as `mandelbrot.qoi` in the current directory.

## How It Works

1. **Initialization**: Sets up Vulkan instance, device, and compute queue
2. **Resource Creation**: Creates storage buffers for image data and uniform buffers for dimensions
3. **Pipeline Setup**: Creates compute pipeline with compiled SPIR-V shader
4. **Execution**: Dispatches compute workgroups to calculate Mandelbrot iterations for each pixel
5. **Color Mapping**: Applies a cosine-based color palette to iteration counts
6. **Output**: Transfers computed RGBA data back to CPU and saves as QOI image

## Shader Details

The compute shader (`shaders/mandelbrot.comp.glsl`) implements the Mandelbrot set calculation:

- Uses workgroup sizes configurable via specialization constants (default 32x32)
- Performs up to 128 iterations per pixel
- Applies early termination when escape condition is met
- Maps iteration counts to colors using a 3D cosine palette

## Debugging

- Define `vkDebug` for Vulkan validation layers
- Define `useRenderDoc` for frame capture support
- Shader includes debug printf for development

## License

Public Domain

## Credits

Based on the Vulkan Mandelbrot Generator example by hudiyu123.
