## CUDA Quantum `target` 
A `target` is a specification of the desired platform and simulator / QPU. It can be specified in C++ as a compile time flag in C++ and in Python as a runtime flag. Alteratively, it can also be specified within the application code. 

### Simulation backends
- state-vector (`cuStateVec`) 
- density-matrix (`dm`) 
- tensor-network (`cuTensorNet`)

### Hardware backends
- CPU only   
- Single GPU   
- Multi-GPU
- Multi-QPU

### Targets
- `default`
 	- qpp, CPU-based and multithreaded
        - In C++, `nvq++ ghz_state.cpp -o a.out`
        - In Python, `python3 ghz_state.py` 
- `nvidia` 
	- custatevec with single-GPU
        - In C++, `nvq++ --target nvidia ghz_state.cpp -o a.out`
        - In Python, `python3 --target nvidia ghz_state.py`  
- `nvidia-mqpu` 
	- custatevec with multi-QPU, realized through GPUs acting as virtul QPUs.
        ```
        $ python --target nvidia-mqpu distribute_hamiltonian.py
        ```
- `nvidia-mgpu` 
	- Allows for Multi-Node, Multi-GPU distribution of the state vector using  custatevec.
        ```
        $ nvq++ --target nvidia-mgpu ghz.py -o a.out
        $ mpirun -np 2 ./a.out
        ```
- `density-matrix-cpu` 
	- CPU-only multithreaded density matrix emulation
- `quantinuum` \
        - `--target quantinuum`
- `ionq` 
- more!

To print a list of all the targets that are available for you on your machine:

```
import cudaq

targets = cudaq.get_targets()

for t in targets:
     print(t)
```



