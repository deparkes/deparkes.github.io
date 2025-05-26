---
layout: post
title: String Comparison Techniques
date: 2020-06-21 08:48:33.000000000 +01:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- Data Science
tags:
- natural language processing
- nlp
- string
author:
  display_name: deparkes
permalink: "/2020/06/21/string-comparison-techniques/"
---
String comparison is important for topics such as <a href="https://en.wikipedia.org/wiki/Natural_language_processing">natural language processing</a> and <a href="https://en.wikipedia.org/wiki/Record_linkage">record linkage</a>.  This post gives a few examples of string comparison techniques that you may wish to consider.
<h1>String Comparison Techniques</h1>
Each of these string comparison techniques makes different assumptions or simplifications. You may wish to try several techniques or use a hybrid approach which combines several metrics together to make an overall comparison.
<h2>Edit Distance - Levenshtein Distance</h2>
<a href="https://en.wikipedia.org/wiki/Levenshtein_distance">Levenshtein distance</a> is an example of an '<a href="https://en.wikipedia.org/wiki/Edit_distance">edit distance</a>' metric. It shows you how many changes (deletions, insertions, or substitutions) you would need to make to string 'A' to get it to equal string 'B'.
Try out  this interactive example:
<div>
<a href="https://planetcalc.com/1720/" data-lang="en" data-code="" data-colors="#263238,#435863,#090c0d,#fa7014,#fb9b5a,#c25004" data-v="3389">PLANETCALC, Levenshtein Distance</a><script src="https://embed.planetcalc.com/widget.js?v=3389"></script>
</div>
<h2>Similarity Coefficient - Jaccard Index</h2>
The <a href="https://en.wikipedia.org/wiki/Jaccard_index">Jaccard Index</a> is also known as the 'intersection over union' measure and is applicable to any <a href="https://en.wikipedia.org/wiki/Set">set</a>, not just string comparison. For string comparison the words or individual characters in a string are represented as a 'set' before the index is computed.
The intersection is the number of words or characters that are the same in both strings (sets). The union is the combination of all words or characters in both strings (sets).
Try out this interactive example:
<div><a href="https://planetcalc.com/1663/" data-lang="en" data-code="" data-colors="#263238,#435863,#090c0d,#fa7014,#fb9b5a,#c25004" data-v="3389">PLANETCALC, Jaccard / Tanimoto Coefficient</a></div>
<h2>Phonetic Algorithm - Soundex</h2>
<a href="https://en.wikipedia.org/wiki/Soundex">Soundex</a> is an example of a '<a href="https://deparkes.co.uk/2017/12/01/phonetic-algorithms/">phonetic algorithm</a>'. It works be reducing words down to a simplified approximation of the essential sounds that make them up. Soundex and other phonetic algorithms are frequently used for comparing names where there may be different spellings for the same or similar names.
For example 'Steven' and 'Stephen' both become 'S315', so would be regarded as having an identical sound.
<a href="https://gist.github.com/shawndumas/1262659">See the code for an implementation of the soundex algorithm</a>
