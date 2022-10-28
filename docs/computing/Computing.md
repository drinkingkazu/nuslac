# Computing
Any computing, no matter how light it is, should be done using a dedicated computing server.
NOPE! `sdf-login.slac.stanford.edu` is not a computing server :) so it's good not to work on that node.
This section briefly explains how to use [slurm](https://slurm.schedmd.com/documentation.html) with which you can access computing servers.

There are 3 ways to use slurm:
1. Interactive access through a terminal
2. Batch job submission
3. Interactive access through a web-browser (Jupyter)

## Interactive access through a terminal

One basic option is to access a computing resource interactively on a terminal. 
This would look literally like you are _logging (or ssh-ing) into a server dedicated for computing_.
For this, we use a `slurm` command `srun`. 

Take a look at the demo below.
BTW this movie is a magic: you can use your mouse to copy and paste typed commands from the movie for yourself to try at SDF :)

[![asciicast](https://asciinema.org/a/xjm8siU4p0hPLH005ktDoMhI9.svg)](https://asciinema.org/a/xjm8siU4p0hPLH005ktDoMhI9)

Let's decode this command:
```
srun --partition=neutrino --mem-per-cpu=20G --pty /bin/bash
```
* `--partition` specifies a group account through which you use computing tokens to request resource
* `--mem-per-cpu` specifies the amount of RAM memory per CPU you request (20G means 20 giga-byte) 
* `--pty` specifies what command to execute: here we execute `bash` interactive session
The number of CPU allocated is, by-default, 1.

Then you also saw another command to request a job with a GPU:
```
srun --partition=neutrino  --gpus geforce_rtx_2080_ti:1 --mem-per-cpu=20G --pty /bin/bash
```
* `--gpus geforce_rtx_2080_ti:1` requests `1` of NVIDIA RTX 2080 Ti GPUs for your job.

You mimght wonder:
* How much memory should I rquest?
* Does my job run indefinitely? What happens if I `exit`?
* etc. etc. ...
Look at the FAQ + [message kazu](mailto:kterao@slac.stanford.edu) or slack him if you have a question.

There are more option flags to better control the use of computing resource.
You learn more below where we try a batch job submission.

## Batch job submission

Once you finish developing your code, you may have a script that runs data processing by a single line of a command. 
You may not want to wait for this process to finish running in an interactive session.
This is when you want to use a __batch job submission__.

Here, let's practice an extremely simple batch job submission.
We will submit a batch job to execute `example.sh` script which contents is shown below.

```
#!/bin/bash
#SBATCH --partition=neutrino
#
#SBATCH --job-name=test
#SBATCH --output=job-%j.out
#SBATCH --error=job-%j.err
#
#SBATCH --ntasks=1
#SBATCH --cpus-per-task=4
#SBATCH --mem-per-cpu=5g
#
#SBATCH --time=10:00
#                                                                                                           
#SBATCH --gpus=geforce_rtx_2080_ti:1                             

uname -a
nvidia-smi
```

The script executes two commands: `uname -a` then `nvidia-smi`.
Respectively, these commands print out the name of a server where the process is running and the status of GPUs.

I submit this script by a simple command:
```
sbatch example.sh
```

[![asciicast](https://asciinema.org/a/532704.svg)](https://asciinema.org/a/532704)

Yep, it's that simple! 

Let's walk through the contents of `example.sh`.
* `#!/bin/bash` tells the terminal excution to use `/bin/bash` (i.e. "bash") interpreter to execute the script.
* `--job-name` specifies the name of this job (i.e. handy if you want to find your job in `squeue`)
* `--output` specifies a text file to contain the standard output from the script
* `--error` specifies a text file to contain the standard error from the script
* `--ntasks` specifies the number of task to run. You can set this to the number main process to run.
* `--cpus-per-task` specifies the number of hyperthreads (i.e. "virtual cores") to be allocated per task. Note our machines have 2 hyperthreads per physical CPU core. This should match with the number of parallel threads/processes run by your main script.
* `--mem-per-cpu` specifies the amount of RAM memory per hyperthread. `5g` means 5 GByte. This job will have 20 GByte memory total with 4 hyperthreads.
* `--time` specifies the maximum amount of time allocated for this job. When this time is reached, if the job is still running, the job will be terminated.
* `--gpus` specify the type and count of GPUs to be allocated.

Some of these flags already showed up in the example of an interactive session with `srun`. 
I hope this explains the gists of how to submit a slurm batch job.

## Interactive access through a web-browser (Jupyter)

This is probably the most popular way of accessing the computing resource (hence it comes at the end :D).

Click the thumbnail below and watch a [YouTube tutorial movie](https://youtu.be/NhigtAK2BGM)!

[![Youtube Movie](https://img.youtube.com/vi/NhigtAK2BGM/0.jpg)](https://www.youtube.com/watch?v=NhigtAK2BGM)


