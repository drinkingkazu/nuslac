



# Storage space 

On each server machine, you typically have 4 types of space to work.

* `$HOME` ... 25GB space by default.
    * Network mounted = accessible from different machines.

* `/sdf/group/neutrino` ... global (network mounted) group space.
  * Network mounted = accessible from different machines
  * No purging policy. Keep your usage < 1TB (system does not enforce this limit) 
    * This is `$GROUP` in [official documentation](https://ondemand-dev.slac.stanford.edu/public/doc/#/getting-started?id=disk).
  * Create "your group space" and feel free to store files underneath.
  ```
  mkdir /sdf/group/neutrino/$USER
  ``` 

* `/scratch` ... global (network mounted) scratch space.
  * Network mounted = accessible from different machines
  * Purged approximately once a month. 
    * This is `$SCRATCH` in [official documentation](https://ondemand-dev.slac.stanford.edu/public/doc/#/getting-started?id=disk).
  * Create "your global scratch space" and feel free to store files underneath.
  ```
  mkdir /scratch/$USER
  ``` 
  
* `/lscratch/$USER` ... local RAID0 SSD space for fast read/write (no networking involved) **only on a batch worker node**.
  * Local disk = not accessible from different machines. **`sdf-login` nodes are not batch worker node.**
  * Files written in this space will be purged after you log out (i.e. per job).
  * This is `$LSCRATCH` in [official documentation](https://ondemand-dev.slac.stanford.edu/public/doc/#/getting-started?id=disk).
  

## Data transfer to SDF from outside
Data transfer to SDF should be done using an appropriate data transfer nodes. 
  - **Please do not transfer data via `scp` through `sdf-login.slac.stanford.edu`**.
  - If you want to use `scp`, use `sdf-dtn.slac.stanford.edu` (dtn stands for data transfer node).
  - You can also use `globus` to transfer data files (that would correctly use the right nodes underneath).


