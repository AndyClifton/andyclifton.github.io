---
title: "GitHub Actions - XelaTeX"
date: 2020-11-10
excerpt: "How to keep latex documents up-to-date using GitHub actions<br/><img src='/images/OpenScience-Seminar1-500W.png' style='border: 1px solid;'>"
permalink: /posts/2020/11/github-actions-xelatex/
tags:
  - software development
  - LaTeX
---

While developing our open science course, I hit upon a question: how I could keep my material up-to-date? What happens in a year or two when the latex code has updated and my local installation has become a bit old? And how do I avoid using yet another online platform?

I've been playing recently more and more with GitHub, and wondered if I could do some kind of continuous integration (CI) to build my material. This should be possible; GitHub offers _actions_, which allow users to trigger events when they upload new code to a repository. The possibilities are almost [endless](https://github.com/features/actions), as you can run a virtual machine that can execute arbitrary scripts.

## The scenario
Let's do all of this with reference to the material in https://github.com/LIKE-ITN/OpenScienceTrainingCourse/.

There are a lot of files in there, but there is at least some structure. Each seminar has its own directory, which includes all of the images, etc. need to generate the PDF and notes:

<pre>
.
├── 00_handbook
│   └── readme.md
├── 01_seminar1
│   ├── beamer
│   │   ├── beamercolorthemeuniS.sty
│   │   ├── beamerouterthemeuniS.sty
│   │   ├── beamerthemeuniS.sty
│   │   ├── images
│   │   │   ├── 1280px-FAIR_data_principles.jpg
│   │   │   ├── ...
│   │   │   └── xkcd_2294.png
│   │   ├── main.pdf
│   │   ├── main.png
│   │   ├── main.tex
│   │   ├── readme.md
│   │   ├── section
│   │   │   ├── closing.tex
│   │   │   ├── course-details.tex
│   │   │   ├── covid-19.tex
│   │   │   └── introductions.tex
│   │   ├── unilogo.pdf
│   │   └── unilogo_w.pdf
│   ├── notes
│   │   └── readme.md
│   └── readme.md
├── 02_selfstudy1
│   └── readme.md
...
├── LICENSE
├── readme.md
└── scripts
    └── build_beamer.sh

</pre>

## The constraints
I would like to be able to choose which PDFs get (re)generated. This means that ideally, I would set up my action so that I could just change one or two commands when I need to compile new material.

Also, I am running XeLaTeX. This just seems to be unavoidable for the PDFs from beamer.

## The solution
I decided to split my CI into two:

1. A file to configure the workflow. This would handle things like setting up the virtual machine, installing LaTeX, and doing the pull / push from GitHub.
2. A shell file to manage compiling the LaTeX.

### The GitHub workflow
GitHub actions use a workflow file to trigger and run the CI. These are stored in _.github/workflows/workflow_n.yaml_ where *workflow_n* can be anything that makes sense.

First, we decide when to execute the workflow. I decided to do this every time there was a new version of my files, to avoid getting out of sync. This is set up in the first part of my *workflow_1.yaml* file:

**workflow_1.yaml**
<pre>
name: run_beamer

# Controls when the action will run. Triggers the workflow on push or pull request
# events but only for the main branch
on:
  push:
    branches: [ master ]
  pull_request:
    branches: [ master ]

</pre>

The next step is to set up a job to build the PDFs. This runs on a linux virtual machine. I decided to run it on the latest build. This may cause trouble long-term...

<pre>
# A workflow run is made up of one or more jobs that can run sequentially or in parallel
jobs:
  build_PDFs:
    # The type of runner that the job will run on
    runs-on: ubuntu-latest

</pre>

Then I wanted to get a fairly complete latex version installed, and get my code downloaded. We'll do that in two steps. First, let's get a latex installation:

<pre>
    # Steps represent a sequence of tasks that will be executed as part of the job
    steps:
      
      - uses: xu-cheng/texlive-action/full@v1

      - name: update texlive
        run: |
          sudo apt-get update -y
          sudo apt-get install -y texlive-xetex
          sudo apt-get install -y latexmk
          sudo apt-get install -y texlive-lang-german
          sudo apt-get install -y texlive-fonts-recommended
          sudo apt-get install -y texlive-fonts-extra
</pre>

Then, we can get the code downloaded.

<pre>
      # Checks-out your repository under $GITHUB_WORKSPACE, so your job can access it
      - uses: actions/checkout@v2
      - name: Pull
        run: |
          git config user.name github-actions
          git config user.email github-actions@github.com
          git pull      
</pre>

Now we can execute our arbitrary code:

<pre>
      # Runs a set of commands using the runners shell
      - name: Run beamer script
        run: |
          sh ./scripts/build_beamer.sh
</pre>

And the last step is to push the results back to my GitHub repository.

<pre>
      - name: Commit
        run: |
          git add .
          git diff-index --quiet HEAD || git commit -m "action generated new PDFs using beamer"
          git push
</pre>

The biggest problem with these workflows is **debugging** them. You can help yourself by putting in lots of steps and using the [GitHub interface](https://docs.github.com/en/free-pro-team@latest/actions/managing-workflow-runs/viewing-workflow-run-history) to see what works (or fails). If you have any problems beyond that, I suggest searching stackoverflow.

### The shell script
I use `latexmk` to simplify the process of building the PDF from the latex source. The script itself is nothing fancy; just make sure I am in the right directory, and off we go:

**build_beamer.sh**
<pre>
#!/bin/bash

cd 07_seminar4/beamer
latexmk -f -xelatex main.tex
latexmk -c
cd ~
</pre>

### Using latexmk

The final `latexmk -c`  in the shell script about cleans up the directory.

To make this work we need one last file, `.latexmkrc`. You can put this in the current working directory.

<pre>
$clean_ext = 'synctex.gz synctex.gz(busy) run.xml tex.bak bbl bcf fdb_latexmk run tdo %R-blx.bib nav snm xdv'
</pre>

See [this answer](https://tex.stackexchange.com/a/83386/29222) on tex.stackexchange.com for more information.

## The result
The workflow above takes about 4 minutes to run on GitHub. It's fairly reliable but could be improved, for example by using caching between commits to avoid spinning up a new machine every time.

You can see the whole thing in use as part of my [open science course](https://github.com/LIKE-ITN/OpenScienceTrainingCourse).