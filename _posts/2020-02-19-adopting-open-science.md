---
title: 'What adopting open science means for you and your organization'
date: 2020-02-19
excerpt: This article discusses some of the goals, problems, and opportunities associated with implementing open science in a STEM organisation.
featured-image: /images/OpenScienceResearchInitiative-ResearchLifecycle.png
permalink: /posts/2020/02/adopting-open-science/
tags:
  - Open science
  - Productivity
  - Strategy
---

This article discusses some of the goals, problems, and opportunities associated with implementing open science in an organisation. That could be from 5 to 50,000 people across tech, engineering, education, or research. And by science, I mean anything from hardcore engineering to the natural sciences, to software development.

## Why you should implement open science
This depends on your viewpoint.
 - Internally: open science fosters collaborative and cooperative approaches to working. Those in turn lead to reduced costs by reducing wasted duplicate effort, better visibility of results, and more ability to reuse work elsewhere. It also can reduce reliance on key personnel and makes organisations more resilient.
 - Externally: organisations that believe in open science and have implemented some of the concepts discussed here, are easier to interface with. Given the choice between working with two organisations that are otherwise identical, the open organisation will tend to be the preferred partner. In other words, it can give you competitive advantage.

You can see open science as a pattern of behaviour to enable and support effective research, design, and deployment.

## But isn't open science only for publicly-funded research projects?
No. Part of the motivation for open science is to get better payback on public money. The same principles of cost saving that make it attractive for those projects, make it applicable for general work and also for projects that never see the light of day. For those reasons, open science should be a goal for everyone in science or engineering.

So, open science is applicable to us all.

## Challenge 1. The need for a clearer definition
Before you can implement open science, you need to communicate what open science is, and what's expected.

If in doubt, start with Wikipedia:

> Open science is the movement to make scientific research (including publications, data, physical samples, and software) and its dissemination accessible to all levels of an inquiring society, amateur or professional. (_Source: [Wikipedia](https://en.wikipedia.org/wiki/Open_science#:~:text=Open%20science%20is%20the%20movement,inquiring%20society%2C%20amateur%20or%20professional.)_)

And there's another from the EU-funded FOSTER project:

> Open Science is about extending the principles of openness to the whole research cycle, fostering sharing and collaboration as early as possible thus entailing a systemic change to the way science and research is done. (_Source: [FOSTER](https://www.fosteropenscience.eu/content/what-open-science-introduction)_)

Now that we have a definition, we need something to implement.

## Challenge 2. We don't know what to implement

Implementing open science means implementing policies and technical measures that allow barrier-free access to science. 

What this means depends on context, but I like this one that talks about how to implement open science as part of a project:

{% include image.html url="/images/OpenScienceResearchInitiative-ResearchLifecycle.png" caption='From "The Open Science Handbook" (Open Science and Research Initiative, 2014). Used under the Creative Commons Attribution 4.0 International Public License.' alt="Open Science applied to the project lifecycle" %}

This approach is fine if you are running a project-based organisation, which is relatively common in academia. But it doesn't work so well if you are constantly producing small reports or other "data". In that case, the goal is to make the data open.

## Challenge 3. How do we make data open?

You can make your data - measurement files, lab notebooks, reports, whatever - open by applying the "**FAIR Guiding Principles for scientific data management and stewardship**"[^FAIR]. Developed in 2016, the FAIR data principles support and enable the reuse of research data. The FAIR data principles are that data should be:

- **F**indable
- **A**ccessible
- **I**nteroperable
- **R**eusable.

Although the FAIR data principles were aimed at making data reusable by machines, they can also be applied to help make data more reusable by people.

How can these be applied in practice? In the paper[^FAIR], the FAIR principles are broken down further. I've shared them below with some additional ideas. You can also check out [go-fair.org](https://www.go-fair.org/fair-principles/) for more details.

### To be Findable:

|  | Action | Notes |
|------------------------|--------------------------------------------------|-----------|
| F1 | (Meta)Data are assigned a globally unique and persistent identifier | Get your data a Digital Object Identifier (DOI) |
| F2 | Data are described with rich metadata (defined by R1 below) | Define or adopt a metadata schema |
| F3 | Metadata clearly and explicitly include the identifier of the data it describes | Include the DOI of the data in the metadata |
| F4 | (Meta)data are registered or indexed in a searchable resource | Upload the metadata to a data repository -- e.g. a public repository like Zenodo or an organisation-hosted one like [DARUS](https://darus.uni-stuttgart.de/) -- and tag it with appropriate keywords. |

Another tip here is to associate all data with a data _producer_, typically a person. That person can also have an identifier - see e.g. ORCiD - so that data can be found through that person if their ORCiD is included in the metadata.

### To be Accessible:

|  | Action | Notes |
|------------------------|--------------------------------------------------|-----------|
| A1 | (meta)data are retrievable by their identifier using a standardized communications protocol | Use something like http(s) or ftp |
| A1.1 | the protocol is open, free, and universally implementable | avoid proprietary interfaces to data (even if they have been reverse engineered) |
| A1.2 | the protocol allows for an authentication and authorization procedure, where necessary | Although open science trends towards unfettered access, there are cases where it can be good to know who is accessing data and possibly implementing access control procedures |
| A2 | metadata are accessible, even when the data are no longer available | Place metadata and data in different records or different repositories. | 

### To be Interoperable:

|  | Action | Notes |
|------------------------|--------------------------------------------------|-----------|
| I1 | (meta)data use a formal, accessible, shared, and broadly applicable language for knowledge representation. | There are any number of ways to do this, for example with [RDF files](https://scigraph.springernature.com/ontologies/subjects/).  |
| I2 | (meta)data use vocabularies that follow FAIR principles | If you use a keyword, make sure that its drawn from an existing structure like [Nature's subjects _taxonomy_](https://www.nature.com/nature/browse-subjects). These are created from [a reference file](https://scigraph.springernature.com/ontologies/subjects/). |
| I3 | (meta)data include qualified references to other (meta)data| Link your (meta)data to other (meta)data. This helps make it better defined and understandable. |

### To be Reusable:

|  | Action | Notes |
|------------------------|--------------------------------------------------|-----------|
| R1 | meta(data) are richly described with a plurality of accurate and relevant attributes | This focuses on the ability of the user to judge if data are useful. The onus is on the data provider to give lots of descriptive data. |
| R1.1 | (meta)data are released with a clear and accessible data usage license | Without a license data are automatically under copyright, which limits reuse |
| R1.2 | (meta)data are associated with detailed provenance |  |
| R1.3 | (meta)data meet domain-relevant community standards | See comment to Nature's subject taxonomy in I2 |

If you'd like to dig into this in more detail, see [GO FAIR](https://www.go-fair.org/fair-principles/).

## Challenge 4. We can't be open because we are a commercial organisation

Well, you can still be open internally or within your teams. This might not mean publishing everything, but you can do other things that support open science. For example:

1. Start regular team meetings to make it easier for your team to identify what is happening
1. Use data and code repositories to make it easier for your team to share their work
1. Develop modular, reusable code and projects instead of behemoths
1. Work on you culture; make your teams a safe place to have and share ideas. Reward those who work to share their experience and expertise.
1. Create frameworks for sharing 

---

## Challenge 5. Change is not popular

You can imagine that open science potentially means changing how organisations work. It asks a lot of an organisation and can be disruptive. In some cases it may be completely opposite to existing ways of working. Therefore, you should expect that implementing the open science principles will not be easy.

But, the benefits are potentially huge. Given those challenges and the potential benefit, it's worth treating the adoption of open science as a strategic change and using appropriate tools. Some ideas for what that might mean in this context are:

1. Identify a small team to work on it
1. Figure out what success looks like - for example, an open publication coupled with complete data and code, might be a good target for an academic organisation. A startup might try something like publishing an SDK, or API.
1. Help your existing staff see themselves in productive, rewarding positions in any new organisation that you might be creating.
1. Provide training.
1. Identify and empower someone to be the champion of the process.
1. Identify and empower a technical lead or point-of-contact to help support the process.
1. Reward people for trying, and reward them for success.
1. Expect the first attempts to be unsatisfactory, but learn from them.
1. Run regular reviews.
1. Keep trying!

## Result: open science is tangible and progress is measurable

Rather than just being a philosophy, open science can be defined as a series of concrete, tangible activities. This opens the door for organisations in academia and private industry to adopt it, monitor their adoption, and ultimately profit from it.

_For more about open science, see my course on [GitHub](https://github.com/LIKE-ITN/OpenScienceTrainingCourse)_

[^FAIR]: Wilkinson, M., Dumontier, M., Aalbersberg, I. et al. The FAIR Guiding Principles for scientific data management and stewardship. Sci Data 3, 160018 (2016). [https://doi.org/10.1038/sdata.2016.18](https://doi.org/10.1038/sdata.2016.18)