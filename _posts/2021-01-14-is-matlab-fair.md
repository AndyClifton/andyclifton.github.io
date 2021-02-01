---
title: 'Is MATLAB FAIR?'
date: 2021-01-14
draft: false
excerpt: Is code made with MATLAB - a proprietary programming language - appropriate for open science?
featured-image: /images/2021/01/hitesh-choudhary-D9Zow2REm8U-unsplash_800W.jpg
permalink: /posts/2021/01/is-matlab-fair/
tags:
  - Open science
  - Productivity
---

[MATLAB](https://www.mathworks.com/products/matlab.html) is a proprietary programming language used extensively for STEM applications. Because of its ease of use and favourable license conditions, its used a lot for teaching and academic research. 

But, as the open science movement grows, many people are moving away from MATLAB because it's proprietary. Does this make sense?

_N.B. I am not affiliated with the MathWorks (the creators of MATLAB) in any way._

## The basic principles of open science
Open science is the movement to make the process and results from science freely available for specialist and non-specialists. 

There are two main principles for openness that apply to using MATLAB for science. These are the FAIR principles[^FAIR], which refer to how data ("digital objects") can be made open:
- **F**indable: _data have identifiers and metadata_
- **A**ccessible: _data can be retrieved easily using free protocols_
- **I**nteroperable: _data use common languages or vocabularies_
- **R**eusable: _data have sufficient metadata and licensing that others can use them_.

The R<sup>5</sup> goals[^R5] refer to the characteristics that scientific code needs to have to support openness:
- **R1**: Re-runnable: _the code can be re-executed_
- **R2**: Repeatable: _the code should produce the same results every time you execute it_
- **R3**: Reproducible: _the code should give the same results as in a paper if other people use it_
- **R4**: Reusable: _the code should be easy to use, understand, and modify_
- **R5**: Replicable: _a clear algorithmic representation should be available so that the code can be implemented in another language_
  
Data that are FAIR, and codes that achieve the R<sup>5</sup> principles are very useful; they can be shared and reused easily, and make it easy to leverage other peoples' efforts. This is exactly what we need for open science.

## Why some people don't like MATLAB
There are a couple of problems that people have pointed out with MATLAB.
1. MATLAB costs money. So by coding in MATLAB, we exclude under-funded scientists or hobbyists who might have otherwise been able to use our code.
1. MATLAB changes every so often. Now at version R2020b, there have been at least annual updates to MATLAB for almost 40 years. While this means that users have updated functionality, it does make backward compatibility challenging.
1. MATLAB has a lot of toolboxes. These cost money and also have dependencies.
1. There's no way to define a MATLAB environment so that when we share code with someone else, they can actually use the exact same MATLAB environment. We can do this by running tests for versions in the code, but that's unusual. Any suggestions here would be very welcome!

This means that code written in MATLAB can only be shared with a limited community and can't run reliably on another machine. These seem to be the main reasons why MATLAB is perceived as _not good for open science_. But is this true?

{% include image.html image-url="/images/2021/01/hitesh-choudhary-D9Zow2REm8U-unsplash_800W.jpg" shadow=true caption="Just because a programming language is open source, that doesn't mean that it automatically enables open science" alt="a person holding a python sticky note" %}

## This is not a MATLAB problem
Let's be reasonable. While we've used MATLAB as the example, the same points we raised above are applicable to many other programming languages, not just MATLAB.

The real issue is that people don't know what the best practices are for making my data FAIR, or how to make code that supports the R<sup>5</sup> goals. These challenges have been known for a long time, and MathWorks - the creator of MATLAB - have been [working on solutions](https://de.mathworks.com/company/events/webinars/upcoming/the-use-of-matlab-in-open-science-3248333.html). There are a host of other education initiatives as well.

## So should you use MATLAB for open science?
Why not? If you already use it, you can think how to be FAIR and work with the R<sup>5</sup> goals, instead of learning a new programming language.

### Can MATLAB products be FAIR?
FAIR is about how you treat the data. There is nothing stopping you sharing your MATLAB code or data through a repository. You can add lots of metadata, get a Digital Object Identifier (DOI) for your code, and use community standards.

So, publish your stuff! Not publishing it all would be even worse!

### Does MATLAB support the R<sup>5</sup> goals?

The scripts that MATLAB uses are simple text files. These can be read by any text editor. Some toolboxes and parts of MATLAB might use compiled files. This means that often, other people can see and apply the algorithms even if they can't run it. It also helps that MATLAB code is often quite readable and it has extensive documentation.


There are also alternatives to sharing raw MATLAB code. You could share an executable or DLL, which might be easier to use on other machines. 

Publishing something in MATLAB also gives you a chance to engage with your community and ask if people would like to see the same algorithms implemented in a different programming language.

### What about the data?
MATLAB usually saves data in proprietary data formats. These files are hard (but not impossible) to read with anything but MATLAB, so don't really help implement open science. 

But, you don't have to use MATLAB data formats when you save things. You could opt to save simple text files, Common Data Format (CDF), or [many other file types](https://de.mathworks.com/help/matlab/import_export/supported-file-formats.html). You may also find that specific domains have developed MATLAB-compatible file formats.

Therefore, the use of MATLAB _per se_ does not work against open science. Instead, the choice of file format - by the person writing the code - is very important.

## New project, new code?
One possible solution to the challenges with MATLAB would be to use a different programming language. 

Python is often pointed to as a good alternative, partly because it is used for so many different things and is used commercially for big projects, and so there is a big need to make code written in Python conform to the R<sup>5</sup> goals. There are ways to package up code and environments so that they can be run reliably by another user. These include cloud-hosted Python notebooks, packages, docker or other images, various Python environment managers and all manner of homebrew approaches.

But badly written Python code is just as much of a problem as MATLAB to share and re-run. Don't expect Python to be a magic bullet.

## Planning, experience, and training matters more than the choice of code
Making data that is FAIR and writing code that lives up to the R<sup>5</sup> goals is as much about the person writing the code, as it is about the programming language.

If you know in advance that you are going to be sharing code or data, plan for it. Read up a bit on the ideas, and come up with strategies for implementing it. Talk to experts, and don't be afraid to get [training](https://github.com/LIKE-ITN/OpenScienceTrainingCourse/tree/master/03_seminar2).

Give it a try!

[^FAIR]: Wilkinson, M., Dumontier, M., Aalbersberg, I. et al. The FAIR Guiding Principles for scientific data management and stewardship. Sci Data 3, 160018 (2016). [https://doi.org/10.1038/sdata.2016.18](https://doi.org/10.1038/sdata.2016.18)

[^R5]: Benureau, F.C.Y. and Rougier, N.P. Re-run, Repeat, Reproduce, Reuse, Replicate: Transforming Code into Scientific Contributions. Front. Neuroinform (2018). [https://doi.org/10.3389/fninf.2017.00069](https://doi.org/10.3389/fninf.2017.00069)