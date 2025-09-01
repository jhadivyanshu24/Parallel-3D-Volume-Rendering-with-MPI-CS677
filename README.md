# Parallel 3D Volume Rendering with MPI

An implementation of distributed ray casting for volume rendering using 3D domain decomposition and MPI.  
Designed for scalable rendering of large volumetric datasets like *Isabel_High_Resolution_Raw*.  

---

## Core Features

### Distributed 3D Domain Decomposition
- Partitions scalar volumetric data across MPI processes along X/Y/Z dimensions.
- Ensures balanced workload distribution for scalable rendering.

### Distributed Ray Casting
- Each MPI process performs local ray casting on its assigned subdomain.
- Supports front-to-back compositing with configurable ray step size.

### Distributed Image Composition
- Implements parallel binary-swap compositing to merge partial images across processes.
- Minimizes communication overhead during the final image stitching phase.

### Performance-Optimized
- Tracks distributed timing metrics:
  - Computation (local rendering)  
  - Communication (MPI sync)  
  - Total runtime
- Outputs:
  - Rendered image: `PX_PY_PZ.png`  
  - Performance logs for benchmarking

---

## Output Example
- Final composited image (saved as `PX_PY_PZ.png`)
- Performance log with computation and communication breakdown

---

## Requirements
- MPI (Message Passing Interface) implementation (e.g., OpenMPI, MPICH)  
- C/C++ compiler with MPI support  
- Volumetric dataset (e.g., `Isabel_High_Resolution_Raw`)  

---

## Run Instructions
```bash
# Compile
mpic++ volume_render.cpp -o volume_render

# Run with N processes
mpirun -np <N> ./volume_render <input_volume.raw> <output.png>
