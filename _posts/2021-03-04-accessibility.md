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

During my PhD I was introduced to the [\LaTeX document preparation system](https://www.latex-project.org/) and got hooked on its ability to produce equations, cross references, manage bibliographies, and so-on. Like many people I have since used it for lots of other scientific documents, presentations, and journal articles. As it's basically a programming language, LaTeX really lends itself to these tasks.

## The need to create _accessible_ documents
When people interact visually with a document they unconsciously give that document a structure. That bit there is a heading, there's some text, and there's an equation. And when we read the equation, we give it meaning - for example, we might recognize that $$y = mx + c$$ defines a line. These are examples of _structure_ (how the document is built up), _tagging_ (what elements are in the document), and _descriptions_ that explain text and non-text elements. Position on the page no longer matters, but reading order is important.

You can now imagine that you could take the same document and abstract it into a structured tree with tags and descriptions. That document becomes machine-readable, sort of like xml.

This is really helpful, because machine-readable documents are inherently more _accessible_; they can be read out loud by a screen reader and so can be accessed by anyone who cannot read; they can be read out, or they could be converted in to Braille, the font size could be increased, or any number of other changes.

The ability to access government documents using these alternative approaches is now a requirement in many countries. In practical terms this means that documents have to be accessible, i.e., structured and tagged, and containing image descriptions.

Focussing on prose documents - articles, reports, and books - let's take a look at how this question of tagged and structured PDFs is dealt with by LaTeX.

## Accessibility in LaTeX
Unfortunately LaTeX doesn't generate this structure or tagging directly. 

There's a nice description of what this would require by Ulrike Fischer in the [2020 TUGboat](https://www.tug.org/TUGboat/tb41-1/tb127fischer-accessible.pdf).

### Native LaTeX workflows

[Since about 2013](https://tex.stackexchange.com/questions/124291/revisiting-producing-structured-pdfs-from-latex) I have been trying to figure out a good solution to this. 

#### The accessibility package
I quickly found the `accessibility` package created by Babett Schalitz. This is a LaTeX package intended to generate structure and tagging. It was originally intended for KOMA-script documents. It works by basically post-processing the document to recognise sections, text, etc., and write in the appropriate information to the PDF. It had a few bugs but seemed promising. Unfortunately it wasn't included in CTAN and the license was not clear.

In 2019 I took on the maintenance of the package with Babett's permission. I clarified the license, stuck it on Github, and [got it included in CTAN](https://ctan.org/pkg/accessibility?lang=en) so that other people can use it. I had started to nibble away at the issues but was only able to introduce sticking-plaster solutions. It was the proverbial whack-a-mole; fix something here, something breaks there. Unfortunately it really doesn't work with modern releases of LaTeX and probably can't, and so I was quickly reduced to [just collecting issues](https://github.com/AndyClifton/accessibility/issues). 

I spent some time in late 2019 and early 2020 trying to find out what the problems were, and looking for funding to get a professional developer to fix it. 

In 2020 I wrote to the CTAN folks:
> Based on feedback to the ‘accessibility’ package and discussions with a few folks, I’d like to discourage people from using the package any more. It’s evident that it’s not going to work in it’s current form, and I don’t have the skills or time to update it. I know the general concept is very important, and so I’m looking at getting support from various funding agencies to employ someone to completely refactor the code in a more future-proof fashion. I’ll coordinate this with the core LATEX Team once I have more solid ideas.

This can also be read as "it's broken".

{% include image.html shadow=false image-url="/images/2021/03/accessibility_blurred.png" caption="Text isn't always easy to read. That's why we need to be able to create a structured, tagged PDF" alt="blurred text" %}


#### The LaTeX project team to the rescue

Fortunately, in late 2020 the LaTeX project announced a [major initiative to make LaTeX produce structured and tagged PDFs](https://www.latex-project.org/news/2020/11/30/tagged-pdf-FS-study/). This built on a feasibility study done in collaboration with Adobe.

**This is great news**, and I am really pleased to see this progressing. Congratulations to the LaTeX team!

However, it does mean that there is really no point in my continuing to work on `accessibility` and I have asked the CTAN maintainers to mark the package as unmaintained.

----

So, what should a LaTeX user do while they wait for a solution? Here are some ideas.

## Accessibility in other 'tex versions
It seems that there may be a way to do this [in ConTeXt](https://tex.stackexchange.com/a/181285/29222). Unfortunately I am not a ConTeXt user so have no way to confirm if this works.

## Create structures in the PDF
One solution is to [process a PDF in Adobe Acrobat to create a tagged PDF](https://helpx.adobe.com/acrobat/using/creating-accessible-pdfs.html). There are also commercial solutions to processing PDFs for this. A quick check with your favourite search engine will reveal several options.

## Use Microsoft Word and Adobe Acrobat
It is possible to use Microsoft Word and Adobe Acrobat to generate a tagged PDF. Usefully, you can then adjust the tagging yourself to fix any problems. Word and Acrobat will cost a few hundred dollars / Euros per year, but this may be much cheaper than your time to figure out an alternative approach. If this workflow is ok for you, you can just export the LaTeX to Microsoft Word using Pandoc and pick up your work there.

## Other approaches
What do you use? If you have any solutions, please get in touch! Alternatively, there are a bunch of questions on the [`accessibilty` tag on tex.stackexchange.com that need some answers](https://tex.stackexchange.com/questions/tagged/accessibility)!