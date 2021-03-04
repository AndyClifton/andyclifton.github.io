---
title: 'Making accessible PDFs from LaTeX'
date: 2021-03-04
excerpt: Is it possible to make a tagged PDF from LaTeX?
featured-image: /images/2021/03/accessibility_blurred.png
permalink: /posts/2021/03/latex-accessibility/
usemathjax: true
tags:
  - latex
  - accessibility
---

During my PhD I was introduced to the [$$\LaTeX$$ document preparation system](https://www.latex-project.org/) and got hooked on its ability to produce equations, cross references, manage bibliographies, and so-on. Like many people I have since used it for lots of other scientific documents, presentations, and journal articles. As it's basically a programming language, LaTeX really lends itself to these tasks.

## The need to create _accessible_ documents
When people interact visually with a document they unconsciously give that document a structure. That bit there is a heading, there's some text, and there's a figure, and an equation. Position on the page no longer matters, but reading order is inferred from headings. And when we read the equation, we give it meaning - for example, we might recognize that $$y = mx + c$$ defines a line. Similarly, we might see a picture and recognise a bird. These are examples of _structure_ (how the document is built up), _tagging_ (what elements are in the document), and _descriptions_ that explain text and non-text elements. 

You can now imagine that you could take the same document and abstract it into a structured tree with tags and descriptions. That document becomes machine-readable, sort of like xml.

This is really helpful, because machine-readable documents are inherently more _accessible_ as they can be adapted to different people's requirements. They can be read out loud by a screen reader, or they could be converted in to Braille, the font size could be increased, a [dyslexic-friendly font](https://www.dyslexiefont.com/en/typeface/) could be used, or any number of other changes.

Many countries now require the ability to access government documents using these alternative approaches (such as screen readers). This is sometimes referred to as "508 compliance" in the USA, and there are local equivalents elsewhere. Because PDF documents are the _de facto_ standard for shareable documents, this means that PDF documents have to be structured and tagged, and contain image descriptions. If you want to test a PDF to see what this means, try the [Free PDF Accessibility Checker (PAC 3)](https://www.access-for-all.ch/en/pdf-accessibility-checker.html)

Focussing on prose documents - articles, reports, and books - let's take a look at how LaTeX can produce accessible PDFs (or "tagged PDFs" or "structured PDFs" - you'll hear all three terms used interchangeably).

{% include image.html shadow=false image-url="/images/2021/03/accessibility_blurred.png" caption="Text isn't always easy to read. That's why we need to be able to create a structured, tagged PDF" alt="blurred text" %}

## Accessibility in LaTeX
Unfortunately LaTeX doesn't generate this structure or tagging directly. 

There's a nice description of what this would require by Ulrike Fischer in the [2020 TUGboat](https://www.tug.org/TUGboat/tb41-1/tb127fischer-accessible.pdf).

### Native LaTeX workflows

[Since about 2013](https://tex.stackexchange.com/questions/124291/revisiting-producing-structured-pdfs-from-latex) I have been trying to figure out a good solution to this. 

#### The accessibility package
Like any experienced LaTeX user, I figured there had to be a package for this.

I quickly found the `accessibility` package created by Babett Schalitz. This is a LaTeX package to generate structure and tagging. It was originally intended for KOMA-script documents. It works by  post-processing the document to recognise sections, text, etc., and write in the appropriate information to the PDF. It had a few bugs but seemed promising. Unfortunately it wasn't included in CTAN and the license was not clear.

In 2019 I took on the maintenance of the package with Babett's permission. I clarified the license, stuck it on Github, and [got it included in CTAN](https://ctan.org/pkg/accessibility?lang=en) so that other people can use it. I had started to nibble away at the issues but was only able to introduce sticking-plaster solutions. It was the proverbial whack-a-mole; fix something here, something breaks there. Unfortunately it really doesn't work with modern releases of LaTeX and probably can't, and so I was quickly reduced to [just collecting issues](https://github.com/AndyClifton/accessibility/issues). 

I spent some time in late 2019 and early 2020 trying to find out what the problems were, and looking for funding to get a professional developer to fix it. 

In 2020 I wrote to the CTAN folks:
> Based on feedback to the ‘accessibility’ package and discussions with a few folks, I’d like to discourage people from using the package any more. It’s evident that it’s not going to work in it’s current form, and I don’t have the skills or time to update it. I know the general concept is very important, and so I’m looking at getting support from various funding agencies to employ someone to completely refactor the code in a more future-proof fashion. I’ll coordinate this with the core LATEX Team once I have more solid ideas.

This can also be read as "it's broken, and I can't fix it with the resources I have".

#### The LaTeX project team to the rescue

Fortunately, in late 2020 the LaTeX project announced a [major initiative to make LaTeX produce structured and tagged PDFs](https://www.latex-project.org/news/2020/11/30/tagged-pdf-FS-study/). This built on a feasibility study done in collaboration with Adobe. It seems that this will be a wide-reaching, reliable solution to the problem, but it could take a while to arrive.

**This is great news**, and I am really pleased to see this progressing. Congratulations to the LaTeX team!

#### What next for the `accessibility` package?

However, it does mean that there is really no point in my continuing to work on `accessibility`. So, in early March 2021 I made the difficult decision to stop trying to fix up the package, and I have asked the CTAN maintainers to mark the package as unmaintained. If anyone would like to take it on, please [get in touch](https://github.com/AndyClifton/accessibility/issues).

----

So, what should a LaTeX user do while they wait for a solution? Here are some ideas.

## Structure and tagging in other 'tex versions
It seems that there may be a way to do this [in ConTeXt](https://tex.stackexchange.com/a/181285/29222). Unfortunately I am not a ConTeXt user so have no way to confirm if this works.

## Process the PDF
One solution is to [process a PDF in Adobe Acrobat to create a tagged PDF](https://helpx.adobe.com/acrobat/using/creating-accessible-pdfs.html). Acrobat will cost a few hundred dollars / Euros per year, but this may be much cheaper than your time to figure out an alternative approach.

There are also commercial solutions to processing PDFs for this. A quick check with your favourite search engine will reveal several options.

## Use Microsoft Word to generate your PDF
[Microsoft Word can generate a tagged PDF directly](https://support.microsoft.com/en-us/topic/create-accessible-pdfs-064625e0-56ea-4e16-ad71-3aa33bb4b7ed). You can then adjust the tagging yourself using Acrobat to fix any problems.

If this workflow is ok for you but you'd rather start in LaTeX, you can just export LaTeX to Microsoft Word using Pandoc and pick up your work there.

## Other approaches
What do you use? If you have any suggestions, please get in touch!

Alternatively, there are a bunch of questions on the [`accessibilty` tag](https://tex.stackexchange.com/questions/tagged/accessibility) on tex.stackexchange.com that need some answers :)