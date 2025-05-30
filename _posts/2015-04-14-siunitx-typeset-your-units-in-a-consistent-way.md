---
layout: post
title: siunitx - typeset your units in a consistent way
date: 2015-04-14 18:34:36.000000000 +01:00
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
author:
  display_name: deparkes
permalink: "/2015/04/14/siunitx-typeset-your-units-in-a-consistent-way/"
---
<h1>The siunitx Latex Package</h1>
When you're writing your thesis or dissertation it can be important to be consistent with how you typeset them. The siunitx Latex package helps you typeset units consistently by automatically setting things like spacing, unit symbols and prefixes.
<h3><a href="https://texdoc.net/texmf-dist/doc/latex/siunitx/siunitx.pdf">Download the documentation for siunitx</a></h3>
<h3><a href="https://www.ctan.org/pkg/siunitx?lang=en">Visit the CTAN site</a></h3>
Here are some examples for how you might use it:
```latex
\SI{0.5}{\tesla}
\SI{4}{\micro \metre}
\SI{20}{\kilo \electronvolt}
\SI{100}{\nano \metre}
\num{e-3}
\num{10}
```

Which when compiled looks like:

| !["siunitx examples]({{site.baseurl}}/assets/2015/04/siunitx_example.png) |
|:--:|
| *siunitx example* |
