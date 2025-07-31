---
name: Better debugging for Snakemake with a custom Panoptes branch
tools: [python]
order: 3
image: ../assets/figs/panoptes-branch.png
description: Panoptes is a great idea for monitoring Snakemake workflows, but it’s missing some critical features. I built a custom branch that helps surface job logs and makes debugging easier, especially when running pipelines on a cluster.
---

# Better debugging for Snakemake with a custom Panoptes branch 

**[Panoptes](https://github.com/panoptes-organization/panoptes)** is a server for monitoring the execution of [Snakemake](https://snakemake.readthedocs.io/) workflows in real time. If you’ve ever launched a long Snakemake pipeline and wished you could actually see what was going on, this tool is for you!

I love Snakemake, it’s my go-to for putting together quick bioinformatics pipelines, and it does a great job of keeping projects clean, reproducible, and scalable. However, debugging failures, especially on clusters, can be frustrating. You often have to dig around to find the right log file, and it’s not always obvious why something failed. That’s why panoptes seemed so promising, but unfortunately, development appears to have stalled, and it’s still missing a lot of what I think are key features.

That’s why I made this branch of panoptes:  
- 🔧 **[panoptes/better-job-data](https://github.com/nataquinones/panoptes/tree/better-job-data)** adds a few features that help me debug workflows more easily.

I might spend more time on this in the future and turn it into a proper pull request, but for now, it’s just my personal solution to a problem I kept running into. It seems like Snakemake 8 is heading in a different direction with its monitoring tools, so we’ll see whether this continues to be useful or if something new takes its place.

---

Specifically, this version allows you to:

- Get more information on the individual jobs
<img src="https://github.com/nataquinones/panoptes/raw/better-job-data/doc/img/workflow.png" width="100%"/>

- Filter jobs by rule, status, or wildcards
<img src="https://github.com/nataquinones/panoptes/raw/better-job-data/doc/img/search_rule.png" width="100%"/>

- View logs (stdout/stderr) directly in the Panoptes job view
<img src="https://github.com/nataquinones/panoptes/raw/better-job-data/doc/img/job.png" width="100%"/>

- Works locally or on clusters (tested on SLURM)
If you're on a cluster and want to monitor your pipeline from your local machine, I included detailed instructions for port forwarding and screen setup in the [README](https://github.com/nataquinones/panoptes/tree/better-job-data?tab=readme-ov-file#how-to-run-on-a-slurm-cluster).