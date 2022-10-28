# Overview
Computing resources are made available at SLAC Data Facility (SDF). The [official documentation of SDF](https://ondemand-dev.slac.stanford.edu/public/doc/#/getting-started) is available though it is also under development still as of September 2020. This page provides a complementary (and a bit of duplicate) documentation to the official SDF one with an aim to guide neutrino users. In particular this covers 4 categories...

* **Storage**: where is my space? where to keep my data files?
* **Softwares**: how can I set up a software stuck? how can I add more softwares?
* **Computing**: how to submit batch (=unattended, automated) job to run your computing script?

## Access via `ssh`
You can access to SDF either from a web-browser or a terminal. These methods are complementary to each other in strengthe, and you are encouraged to try both methods at least once.

  * From your laptop/desktop terminal, you can access SDF via [secure shell (SSH)](https://en.wikipedia.org/wiki/Secure_Shell). 
```
ssh $USER@sdf-login.slac.stanford.edu
```

