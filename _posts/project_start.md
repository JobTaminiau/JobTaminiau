---
title: "Data analysis project set up"
date: 2021-10-08T13:53:30-04:00
categories:
  - Scripts
tags:
  - python_code
  - Git
  - Git bash
  - Standardized project
---

To set up my research projects, I rely on the following protocol. 

1. Open Anaconda Prompt. Create a project-specific environment using 'conda create -n my-env (Where my-env is the name of the new environment).
2. Within Anaconda Prompt, navigate to the directory location of the project. Run cookiecutter https://github.com/drivendata/cookiecutter-data-science from root environment to initiate basic project folder structure.
3. Use conda activate my-env to switch to the newly created environment.
4. Install ploomber for workflow management in the new environment: conda install ploomber.
5. Create a pipeline.yaml file using atom that will describe the workflow of tasks (functions, notebooks, SQL, etc.).

Now that the basic project structure is in place, we can go ahead and commit it to a new Github repository.

1. Commit project to git using Git Bash. Open Git Bash, navigate to the appropriate directory. Run 'git init' in the directory of interest to initialize the repo.
2. Run git add . (with period) to add all the files in the directory to the repo.
3. Run git commit -m "girst commit" (-m allows for message).
4. Create a new repo on Github.com. 
5. In Git Bash, run git push https://[authentication key]@JobTaminiau/[repo name].git
