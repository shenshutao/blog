---
layout: splash
title: "NSCC Guide"
date:   2018-04-29 14:06:47 +0800
categories: machine learning
comments: true
share: true
published: true
---
* TOC
{:toc}

## Briefing 
NSCC (National Supercomputing Centre) Singapore is a free super computer resource for the students/staffs from NUS, NTU, SMU and SUTD.      
The steps below more for NUS.

## Create NSCC account
- go to https://www.nscc.sg/
- click "FOR NEW USERS **ENROLLMENT**" -> login -> select NUS -> login to school account -> Done ! You can see the NSCC User Portal.
- Setup your SSH Key or password (alternative) in the NSCC User Portal.
    + (if you choose SSH Key, for Mac users, you just copy the content and store in a file named id_rsa, throw in the ~/.ssh folder; for Win users, store as a file & configure in the putty.)

## If you are not in campus, you need use VPN!
For NUS student, please refer to [this PDF](https://nusit.nus.edu.sg/qat4/wp-content/uploads/downloads/nvpn/nVPN-config-guide-for-students.pdf). From https://nusit.nus.edu.sg/eguides/.     

## Connect to NSCC server
Check this [NSCC New User Guide](https://help.nscc.sg/wp-content/uploads/2017/06/NSCC_New_User_Starter_Guide_v0.1.pdf)    
```
ssh e0015130@nus.nscc.sg
```
You will see your remaining computing time... For new user is 100000 hrs. 

## Login! Check around
```
module available
git --version
```

## Upload a project
- You can connect to the server use FTP tools as Cyberduck/Mac or FileZilla/Win, then upload your project.
- You can download project from internet. 

## Prepare a PBS script ask for the computing resources
```
vi submit.pbs
    #!/bin/bash
    #PBS -k oe
    #PBS -q gpu
    #PBS -j oe
    #PBS -l select=1:ncpus=24:mem=80GB
    #PBS -l walltime=24:00:00
    #PBS -N resnet_bde
    #PBS -P Personal
    cd ${PBS_O_WORKDIR}
    module load python/2.7.12
    module load tensorflow/1.0+keras
    python custom_resNet.py > output_log.txt
```
[PBS SUB Details](https://www.nas.nasa.gov/hecc/support/kb/commonly-used-qsub-options-in-pbs-scripts-or-in-the-qsub-command-line_175.html)

## Submit job use PBS commands
```
qsub submit.pbs
```

You can use below PBS commands to add job, check job status or del job.
```
[e0015130@nus04 v7]$ qsub submit.pbs 
6841177.wlm01
[e0015130@nus04 v7]$ qstat
Job id            Name             User              Time Use S Queue
----------------  ---------------- ----------------  -------- - -----
6841177.wlm01     resnet_spp       e0015130                 0 Q gpunormal       
[e0015130@nus04 v7]$ qdel 6841177.wlm01
[e0015130@nus04 v7]$ qstat
```
[Useful PBS commands](https://www.nas.nasa.gov/hecc/support/kb/commonly-used-pbs-commands_174.html)

## Done.
### Pros
- FREE for student ! Although got total computing time limit as 100000.00 hrs, not a bit issue,

### Cons
- Seems only can run 1 job at 1 time.
- Can not upgrade the Keras version, can use some newly added modle.
- Some time hard to get the job run due to a long queue.

## Sample Here !!!
After login to NSCC:
```
git clone https://github.com/shenshutao/deeplearning_sample.git
cd deeplearning_sample/
qsub submit.pbs
qstat
```



