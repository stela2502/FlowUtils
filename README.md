# FlowUtils Apptainer Image

This repository provides an Apptainer/Singularity image for **Flow Cytometry / FACS analysis** using a modern Python environment including:

- FlowKit  
- FlowUtils  
- FlowIO  
- fcsparser  
- UMAP-learn  
- HDBSCAN  
- matplotlib / seaborn  
- scikit-learn  
- JupyterLab  

The image is built from `FlowUtils.def` and deployed on COSMOS/COSMOS‑SENS using the provided `Makefile` and module‑file generator.

---

## Features

### ✔ Complete FACS Analysis Environment
The container includes:

- Reading & parsing of FCS files (`flowio`, `flowkit`, `fcsparser`)
- Compensation, gating, and transformation tools
- Clustering (`hdbscan`) and dimensionality reduction (`umap-learn`)
- JupyterLab interface for interactive analysis
- Full scientific Python stack (NumPy, SciPy, Pandas, Matplotlib)

### ✔ Fully Reproducible Environment
The Apptainer image isolates all dependencies so your results are fully reproducible across systems, including COSMOS compute nodes.

### ✔ Optional JupyterLab Support
The default `%runscript` starts:

```
jupyter lab --ip=0.0.0.0 --no-browser --allow-root
```

This allows graphical workflow development and FCS exploration inside the image.

---

## Building the Image

The included `Makefile` automates:

- Creating or updating the sandbox  
- Building the `.sif` image  
- Deploying to the shared COSMOS software directory  
- Creating a matching Lua module file for use via `module load`  

### Build everything from scratch:

```bash
make
```

### Or build directly from the definition file:

```bash
make direct
```

### Rebuild sandbox only:

```bash
make restart
```

### Clean sandbox + image:

```bash
make clean
```

---

## Deployment on COSMOS

Currently the image is deployed to:

```
/scale/gr01/shared/common/software/FlowUtils/<version>/
```

And the module file is generated in:

```
/scale/gr01/shared/common/modules/FlowUtils/<version>.lua
```

You can change this deploy target in the Makefile.

Once deployed:

```bash
module load FlowUtils/1.0
```

This automatically sets valid bind paths depending on what exists on the machine:

- `/local`
- `/projects`
- `/scale`
- `/sw`

The module then launches:

```
singularity run -B <valid mounts> /path/to/FlowUtils_v1.0.sif
```

Starting JupyterLab inside the container.

---

## Using the Image

After loading the module:

```bash
module load FlowUtils/1.0
```

you can open JupyterLab from a compute node, or any terminal allowed to open ports:

```
srun --pty bash
jupyter lab --ip=0.0.0.0 --no-browser --allow-root
```

Then connect via SSH port forwarding:

```
ssh -L 8888:<node>:8888 user@cosmos
```

---

## File Structure

```
FlowUtils.def           # Apptainer definition file
Makefile                # Build + deploy automation
generate_module.sh      # Creates COSMOS Lua module
FlowUtils/              # Sandbox during build
FlowUtils_v1.0.sif      # Final image
modules/                # (Local) module file output
```

---

## Notes

- Python caches and unused documentation are stripped to reduce image size.
- Locale and UTF‑8 support included for consistent numeric formatting.
- Additional FACS‑specific Python packages may be added as needed.

---

## Author

**Stefan Lang**  
Bioinformatics & Single‑Cell Analysis  
(Flow cytometry, VR analytics, HPC pipelines)

