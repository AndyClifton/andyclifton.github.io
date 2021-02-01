---
title: "Running XeLaTeX using GitHub Actions"
date: 2020-11-10
excerpt: GitHub actions allow you to use continuous integration to build LaTeX documents from your GitHub repositories
featured-image: /images/2020/11/github-actions-xelatex.png
permalink: /posts/2020/11/github-actions-xelatex/
tags:
  - Software development
  - LaTeX
---

While developing our open science course, I hit upon a question: how I could keep my material up-to-date? What happens in a year or two when the latex code has updated and my local installation has become a bit old? And how do I avoid using yet another online platform?

I've been playing recently more and more with GitHub, and wondered if I could do some kind of continuous integration (CI) to build my material. This should be possible; GitHub offers _actions_, which allow users to trigger events when they upload new code to a repository. The possibilities are almost [endless](https://github.com/features/actions), as you can run a virtual machine that can execute arbitrary scripts.

## The scenario
My goal is to create a PDF using XeLaTeX. 

I need to do this for my [https://github.com/LIKE-ITN/OpenScienceTrainingCourse/](open science training course), which is a mix of seminars, workshops, self-study, and assignments.

Each seminar has its own directory, which includes all of the images, etc. need to generate the PDF and notes. For each seminar I need to generate a PDF presentation from _main.tex_.

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
│   │   ├── main.tex
│   │   ├── section
│   │   │   ├── closing.tex
│   │   │   ├── course-details.tex
│   │   │   ├── covid-19.tex
│   │   │   └── introductions.tex
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
I would like to be able to choose which PDFs get (re)generated. This means that ideally, I would set up my process so that I could just change one or two commands when I need to compile new material.

Also, I am running XeLaTeX. This just seems to be unavoidable for the PDFs from beamer that need non-standard fonts.

## The solution
I decided to split my CI process into two:

1. A _workflow file_ to configure the action. This would handle things like setting up the virtual machine, installing LaTeX, and doing the pull / push from GitHub.
2. A _shell file_ to manage compiling the LaTeX.

### The GitHub workflow file
GitHub actions use a workflow file to configure the CI process. These are stored in _.github/workflows/workflow_n.yaml_ where *workflow_n* can be anything that makes sense.

First, we need to decide when to execute the workflow. I decided to do this every time there was a new version of my files, to avoid getting out of sync. This is set up in the first part of my *workflow_1.yaml* file:

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

The next step is to set up a job to build the PDFs. This runs on a linux virtual machine. I decided to run it on the latest build. This may cause trouble with dependencies long-term, but we'll deal with that another day.

<pre>
# A workflow run is made up of one or more jobs that can run sequentially or in parallel
jobs:
  build_PDFs:
    # The type of runner that the job will run on
    runs-on: ubuntu-latest

</pre>

Then I wanted to get a fairly complete LaTeX version installed, and get my code downloaded. We'll do that in two steps. First, let's get a LaTeX installation and then install the recommended LaTeX packages:

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

Then, we can get the repository downloaded.

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

The biggest problem with these workflows is **debugging** them. You can help yourself by putting in lots of steps and using the [GitHub interface](https://docs.github.com/en/free-pro-team@latest/actions/managing-workflow-runs/viewing-workflow-run-history) to see what works (or fails). If you have any problems beyond that, I suggest searching Stackoverflow.

### The shell script
I use _[latexmk](https://ctan.org/pkg/latexmk/?lang=en)_ to simplify the process of building the PDF from the latex source. _latexmk_ will iteratively run LaTeX until the document compiles and so is ideally suited to headless tasks like this.

The script itself is nothing fancy; just make sure I am in the right directory, and off we go:

**build_beamer.sh**
<pre>
#!/bin/bash

cd 07_seminar4/beamer
latexmk -f -xelatex main.tex
latexmk -c
cd ~
</pre>

### Using latexmk

The first call `latexmk -f -xelatex main.tex` just runs XeLaTeX on the _main.tex_ file.

The final `latexmk -c` in the shell script, cleans up the directory.

To make this work we need one last file, called *.latexmkrc*. This stores some preferences for _latexmk_. You can put this in the current working directory.

**.latexmkrc**
<pre>
$clean_ext = 'synctex.gz synctex.gz(busy) run.xml tex.bak bbl bcf fdb_latexmk run tdo %R-blx.bib nav snm xdv'
</pre>

See [this answer](https://tex.stackexchange.com/a/83386/29222) on tex.stackexchange.com for more information.

## The result
The workflow above takes about 4 minutes to run on GitHub and spits out new PDFs. It's fairly reliable but could be improved, for example by using caching between commits to avoid spinning up a new machine every time.

You can see the whole thing in use as part of my [open science course](https://github.com/LIKE-ITN/OpenScienceTrainingCourse).


{% include image.html image-url="/images/2020/11/github-actions-xelatex.png" shadow=true caption='It works! Results from the actions page on GitHub.' alt="It works! Results from the actions page on GitHub." %}
