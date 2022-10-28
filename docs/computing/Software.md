# Software stacks

* **Singularity**
  * At SLAC we recommend the use of a [Singularity container](https://sylabs.io/singularity/) to carry around and setup a software environment. Note if you are using `Open On-Demand`, your session lives inside a singularity container and you should not be following the instructions below. If you logged in using `ssh` or launching `slurm` job, this instruction is relevant.
  * Shared `Singularity` container images can be found at `/sdf/group/neutrino/images`.
  * If you aren't sure about `Singularity` or which container to use, you can just try:
  ```
  $> singularity exec --nv --bind /gpfs,/sdf,/scratch /sdf/group/neutrino/images/latest.sif bash
  ```
  * See the official documentation or [here](https://github.com/DeepLearnPhysics/playground-singularity/wiki) for getting started with `Singularity`.

* **CernVM File System (CVMFS)**
  * [CVMFS](https://cernvm.cern.ch/portal/filesystem) is also available at SLAC. Anyone who uses it should help documenting here.

