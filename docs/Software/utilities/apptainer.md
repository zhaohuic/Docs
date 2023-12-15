---
title: Apptainer
---

Apptainer (formerly Singularity) s a container platform. It allows you to create and run containers that package up pieces of software in a way that is portable and reproducible. You can build a container using Apptainer on your laptop, and then run it on many of the largest HPC clusters in the world, local university or company clusters, a single server, in the cloud, or on a workstation down the hall. Your container is a single file, and you don’t have to worry about how to install all the software you need on each different operating system.



Apptainer was created to run complex applications on HPC clusters in a simple, portable, and reproducible way. First developed at Lawrence Berkeley National Laboratory, it quickly became popular at other HPC sites, academic sites, and beyond. Apptainer is an open-source project, with a friendly community of developers and users. The user base continues to expand, with Apptainer now used across industry and academia in many areas of work.

Many container platforms are available, but Apptainer is focused on:

* Verifiable reproducibility and security, using cryptographic signatures, an immutable container image format, and in-memory decryption.
* Integration over isolation by default. Easily make use of GPUs, high-speed networks, parallel filesystems on a cluster or server by default.
* Mobility of computing. The single file SIF container format is easy to transport and share.
* A simple, effective security model. You are the same user inside a container as outside, and cannot gain additional privilege on the host system by default. Read more about Security in Apptainer.



## Use Cases
* BYOE: Bring Your Own Environment!
* Reproducible science
* Commercially supported code requiring a particular environment
* Static environments (software appliances)
* Legacy code on old operating systems
* Complicated software stacks that are very host specific
* Complicated work-flows that require custom installation and/or data

