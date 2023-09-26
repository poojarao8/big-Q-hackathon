# ORNL Workshop


## Running CUDA Quantum for non-OLCF systems
The easiest way to get started with CUDA Quantum is via the public Docker images. These images are available for `x86_64` (or `AMD64`) and `aarch64` CPU architectures. Depending on whether you have an NVIDIA GPU or not, you’ll also want to pull a specific tag for these images. 
 
`ghcr.io/nvidia/cuda-quantum:latest`  
 
To pull the image, you will need to install [docker](https://www.docker.com/) and then run `docker pull <image_name>`.
For instructions on how to run the CUDA Quantum container, refer to [this webpage](https://nvidia.github.io/cuda-quantum/latest/install.html#docker-image).
 
CUDA Quantum programs run natively via backend-extensible circuit simulators. The most performant of these require an NVIDIA GPU (e.g. V100, A100, H100, A6000, A4000, etc.). If you do not have access to such a GPU (e.g. on your Macbook), then you will not be able to target these backends. If you have access to a remote workstation with an NVIDIA GPU that you can access during the hackathon, that would be best.

## Targets
A `--target <target-name>` flag can be specified at compilation for `C++` and at runtime for `Python`, which is a combination of the desired platform and simulator / QPU. 
To get additional information on the simulators and backends, go to [TARGETS.md](TARGETSs.md).
