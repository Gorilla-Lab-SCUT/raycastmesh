# RayTracer

A CUDA Mesh RayTracer with BVH acceleration.
Copy from [here](https://github.com/ashawkey/raytracing), add face_id of mesh output.


### Install

```python
git clone https://github.com/Gorilla-Lab-SCUT/raycastmesh
cd raycastmesh
pip install .
```

### Usage

Example code:

```python
import numpy as np
import trimesh

import torch
import raycastmesh

# build BVH from mesh
mesh = trimesh.load('example.ply')
RT = raycastmesh.RayTracer(mesh.vertices, mesh.faces) # build with numpy.ndarray

# get rays
rays_o, rays_d = get_ray(pose, intrinsics, H, W) # [N, 3], [N, 3], query with torch.Tensor (on cuda)

# query ray-mesh intersection
intersections, face_normals, depth, face_ids = RT.trace(rays_o, rays_d) # [N, 3], [N, 3], [N,], [N,]
```

### Acknowledgement

* Credits to [Thomas Müller](https://tom94.net/)'s amazing [tiny-cuda-nn](https://github.com/NVlabs/tiny-cuda-nn) and [instant-ngp](https://github.com/NVlabs/instant-ngp)!
* Credits to [ashawkey](https://github.com/ashawkey/raytracing)