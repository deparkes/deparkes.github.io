---
layout: post
title: Latex Thesis Publications List
date: 2015-06-30 21:21:58.000000000 +01:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- Latex
tags:
- latex
- latex thesis tips
- publications
- science
- thesis
- writing
author:
  display_name: deparkes
permalink: "/2015/06/30/latex-thesis-publications-list/"
---
If you're writing a large document like a <a href="{{site.baseurl}}/2015/05/20/thesis-writing-tips/">thesis </a>or a dissertation, Latex is probably the tool for the job. In this post I use the <a href="https://www.ctan.org/pkg/natbib?lang=en">natbib </a>and <a href="https://www.ctan.org/pkg/bibunits?lang=en">bibunits </a>packages to insert a list of your publications into your thesis.

<h1>Step 1. Set up Your Tex File</h1>
First of all we need to sort out the tex file. We're going to split up the tex file into two bibliography sections using the <a href="https://www.ctan.org/pkg/bibunits?lang=en">bibunits </a>package.
The first bibliography section will be a special one for just our list of publications.
The second one will be the standard bibliography environment in which all of our standard thesis or dissertation references are found.
<h2>Creat a "bibunit" to Contain Our Publications</h2>
First let's take a look at the "bibunit" containing our list of publications.
In the simplest case, we just need something like this, which looks for a bibliography file called 'publications.bib'.

```latex
\begin{bibunit}[plain]
% The \nocite{*} command simply lists all of the references found in the
% bibliography file, without a corresponding reference number in the text.
\nocite{*}
% Here publications refers to our "publications.bib" file containing our
% publications list. Change it to the path to your publications list file
\putbib[publications]
\end{bibunit}
```
Which produces an output very similar to the standard references section, only in the position given by the \putbib{} command.
<strong>Note that you have to build the bibunit bibliographies separately for them to work properly (see step 2, below)</strong>

| ![Basic publication list]({{site.baseurl}}/assets/2015/06/publicationlist_basic-300x121.png) |
|:--:|
| *Basic publication list * |

<h2>Improve the Appearance of the Reference List</h2>
This list of references looks fine, but I wanted to make a couple of changes to make it more of a list of publications.
<h3>Remove Enumeration</h3>
Firstly I removed the reference numbers with the command

```latex
\makeatletter
\renewcommand\@biblabel[1]{}
\makeatother
```

<h3>Change the Title</h3>
Secondly I wanted to change the title from "References" to something a bit more distinctive:

```latex
\renewcommand{\bibsection}{\large \textbf{\begin{center}
Publications
\end{center}}}
% Note: \bibsection is specific to natbib, so you will have
% to look around for how to name your reference environment
% if you use another bibliography package.
```

These changes leave our publications section looking like:

| ![Nicer publications]({{site.baseurl}}/assets/2015/06/Nicer-publications1-1024x252.png) |
|:--:|
| *Nicer publications* |

<h2>The Normal Publication Environment</h2>
Finally we'll sort out our standard bibliography environment.
```latex
% list all of the references in the References bibtext file
\nocite{*}
\bibliographystyle{unsrt}
\renewcommand{\bibname}{References}
% below, "references" is our bib file containing references cited in
% our thesis or dissertation change it to the path to your reference file
\bibliography{references}
```

<h2>Bring it all together - a working example</h2>
Pulling this all together (along with some place-holder text) we get (you can download this example <a href="https://gist.github.com/deparkes/3df4da19de3359dd0a1a59a59f9936cf">here</a>):

```latex
\documentclass{article}
\usepackage{natbib}
\usepackage{bibunits}
\begin{document}
% bibunit to list our publications
\begin{bibunit}[plain]
\renewcommand{\bibsection}{\large \textbf{\begin{center}
Publications
\end{center}}}
\makeatletter
\renewcommand\@biblabel[1]{}
\makeatother
\def\bibfont{\small}
%list all the references in the publications bibtex file
\nocite{*}
\putbib[publications]
\end{bibunit}
\section{Section 1}
Thesis content \dots
% list all of the references in the References bibtext file
\nocite{*}
\bibliographystyle{unsrt}
\renewcommand{\bibname}{References}
\bibliography{references}
\end{document}
```

Which gives us an output of:

| ![bibtex - publication list example output]({{site.baseurl}}/assets/2015/06/publicationlist1-1024x590.png) |
|:--:|
| *bibtex - publication list example output* |

<h1>Step 2. Build Your Tex File</h1>
You may well already be aware that when you build a latex document you need to build it in several stages to correctly generate and use the relevant bibliography files:
latex mydoc
bibtex mydoc
latex mydoc
latex mydoc
When you use the bibunits package you need to build the bibliography for each bibliography unit (as well as the 'standard' bibliography).
<h2>Build Using Texmaker</h2>
Here are steps for doing correctly building the document using <a href="https://www.xm1math.net/texmaker/">texmaker</a>.
Other graphical packages probably operate in a similar way. If you prefer to build your documents via the command line, you might want to check out the <a href="https://www.ctan.org/pkg/bibunits?lang=en">bibunits documentation</a> for further information.
To build the bibunit bibliography we go to options -&gt; configure texmaker and find the biblatex command box. In here you need to enter "bibtex bu1.aux", as shown below.

| ![bibtex - bu1 annotate]({{site.baseurl}}/assets/2015/06/bibtex-bu1-annotate.png) |
|:--:|
| *bibtex - bu1 annotate* |

Click ok and then run through the standard bibliography building steps of build, bibliography, build, build. You should now be able to see your publications in your document.

Finally we need to sort out our standard bibliography. To do this we need to go back to the configure texmaker window and enter "bibtex %" in the bibtex command box (below).


| ![bibtex - normal annotate]({{site.baseurl}}/assets/2015/06/bibtex-normal-annotate.png) |
|:--:|
| *bibtex - normal annotate* |


Now when we go through our build process (build, bibliography, build, build) and view the output we should have both the publications list and the standard bibliography.
It shouldn't matter which way round we build the bibliographies, as long as we do both. I found it easier though to just do the bibunit bibliography once, and then leave texmaker set up for the standard bibliography - which could well change frequently as references are added and removed.

