# RayTracer

![Language](https://img.shields.io/badge/Language-C%2B%2B17-00599C?logo=cplusplus)
![Graphics](https://img.shields.io/badge/Graphics-Vulkan-AC162C?logo=vulkan)
![Build](https://img.shields.io/badge/Build-Premake5-orange)
![Status](https://img.shields.io/badge/Status-Active-success)

<!-- PROJECT LOGO -->
<br />
<div align="center">
  <a href="https://github.com/Eduardo79Silva/RayTracer">
    <img src="images/demo.png" alt="Demo"  width="60%" height="30%">
  </a>
  


  <p align="center">
    Raytracer with denoiser for rendering spheres.
    <br />
    <br />
    <a href="https://github.com/Eduardo79Silva/RayTracer">
      <img src="images/emissive.png" alt="Emissive" width="60%" height="30%">
    </a>
    <br />
    Emissive materials showcase
  </p>

</div>

**A CPU-based path tracing renderer with real-time preview capabilities.**

This ray tracer implements physically-based rendering techniques including global illumination, material systems, and progressive accumulation. Built with modern C++ and Vulkan for display, it demonstrates low-level graphics programming and rendering algorithm implementation.

## Quick Start

```bash
./scripts/Setup.bat
# Open generated solution and build
```

## Why This Implementation

Path tracing produces photorealistic images through physically accurate light simulation, but requires significant computation. This renderer balances quality and performance through progressive accumulation and parallel execution. The architecture separates rendering logic from presentation, enabling experimentation with different algorithms without display system changes.

## Features

**Rendering Capabilities**
- Path tracing with multiple bounce indirect lighting
- Physically-based material system with roughness and metallic properties
- Emission materials for light sources
- Progressive accumulation for noise reduction
- Real-time camera controls with orbit and WASD movement
- Parallel rendering using execution policies

**Technical Systems**
- Ray-sphere intersection tests with early exit optimization
- Camera system with perspective projection and ray generation
- Scene graph supporting multiple objects and materials
- Frame accumulation buffer for temporal anti-aliasing
- ImGui integration for runtime parameter adjustment

## Getting Started

Once you've cloned, run `scripts/Setup.bat` to generate Visual Studio 2022 solution/project files. Once you've opened the solution, you can run the WalnutApp project to see a basic example (code in `WalnutApp.cpp`).


### Prerequisites

- [Visual Studio 2022](https://visualstudio.com) (not strictly required, however included setup scripts only support this)
- [Vulkan SDK](https://vulkan.lunarg.com/sdk/home#windows) (preferably a recent version)

### 3rd party libaries
- [Dear ImGui](https://github.com/ocornut/imgui)
- [GLFW](https://github.com/glfw/glfw)
- [stb_image](https://github.com/nothings/stb)
- [GLM](https://github.com/g-truc/glm) (included for convenience)

### Usage

**Camera Controls**
- Right Mouse Button: Rotate camera
- WASD: Move camera position
- Q/E: Move camera up/down

**Settings Panel**
- Accumulate: Toggle progressive refinement
- Reset: Clear accumulation buffer
- Render: Force single frame render

**Scene Panel**
- Adjust sphere positions and radius
- Modify material properties including albedo, roughness, metallic, and emission
- Changes automatically reset accumulation

## Technical Implementation

**Ray Generation**  
The camera system precalculates ray directions for each pixel using inverse projection matrices. This approach amortizes matrix operations across frames, improving performance during accumulation passes.

**Intersection Testing**  
Sphere intersection uses the quadratic formula to solve ray-surface equations. The discriminant calculation enables early rejection of misses before computing actual hit distances. The closest intersection across all objects determines the visible surface.

**Path Tracing Algorithm**  
Each ray bounces multiple times, accumulating light contributions from emission sources and sky color. Diffuse reflection uses random hemisphere sampling based on surface normals. The renderer applies Russian roulette termination for unbiased energy conservation.

**Material System**  
Materials define surface properties through albedo color, roughness values, and emission parameters. The roughness value controls reflection distribution, while emission creates light-emitting surfaces. These properties integrate into the path tracing calculations for physically plausible results.

**Parallel Execution**  
The renderer uses C++ execution policies to distribute pixel calculations across CPU threads. Each pixel operates independently, enabling efficient parallelization without synchronization overhead.

**Accumulation Strategy**  
Progressive refinement averages multiple samples per pixel over time. The frame index tracks accumulation depth, and camera movement triggers automatic reset. This approach reduces noise while maintaining interactive response.

## System Architecture

The codebase separates concerns through distinct components:

**Renderer** handles pixel iteration, ray tracing, and image buffer management  
**Camera** manages view transforms, projection, and ray direction generation  
**Scene** stores object and material collections with indexing  
**Walnut Framework** provides Vulkan abstraction and ImGui integration

This separation enables independent testing and modification of rendering algorithms without affecting application infrastructure.

## Technology Stack

- C++17 with STL algorithms and execution policies
- Vulkan for GPU-accelerated display
- GLM for vector and matrix mathematics
- ImGui for real-time parameter controls
- Premake5 for cross-platform build configuration

## Project Status

**Current Implementation**  
The ray tracer supports multiple objects, materials with emission, and parallel rendering with progressive accumulation. Camera controls enable interactive exploration of rendered scenes.

**Potential Extensions**
- BVH acceleration structure for complex scenes
- Importance sampling for faster convergence
- Additional primitive types beyond spheres
- Texture mapping and normal mapping support
- GPU compute shader implementation for increased performance

## Development Context

This project demonstrates competency in graphics programming fundamentals including ray-geometry intersection, camera mathematics, and rendering algorithms. The implementation prioritizes code clarity and extensibility while maintaining reasonable performance through parallel execution.

The architecture supports experimentation with advanced techniques such as different sampling strategies, material models, and acceleration structures without requiring significant refactoring.

## Building from Source

The project uses Premake5 for build configuration. Supported platforms include Windows with Visual Studio 2022.

```bash
scripts/Setup.bat
```

The Walnut framework dependency provides Vulkan abstraction and UI components. All required libraries are referenced through the vendor directory structure.

## License

Copyright 2025. All rights reserved.
