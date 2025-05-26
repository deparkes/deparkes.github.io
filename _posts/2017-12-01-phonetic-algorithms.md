---
layout: post
title: Phonetic Algorithms
date: 2017-12-01 15:00:44.000000000 +00:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- Data Science
tags:
- fuzzy matching
- Phonetic Algorithms
- soundex
- string match
author:
  display_name: deparkes
permalink: "/2017/12/01/phonetic-algorithms/"
---
Phonetic algorithms assist in comparing and matching words by their pronunciation, rather than just their spelling. Early phonetic algorithms were introduced to help <a href="https://www.census.gov/history/www/genealogy/decennial_census_records/soundex_1.html">analyse US census data</a>. Phonetic algorithms and other '<a href="https://en.wikipedia.org/wiki/Approximate_string_matching">fuzzy matching</a>' techniques have since played an essential part in many activities including <a href="https://www.sajari.com/search/synonyms">spelling correction</a>, <a href="https://www.datasciencecentral.com/profiles/blogs/fuzzy-matching-algorithms-to-help-data-scientists-match-similar">database record linkage</a> and <a href="https://stackoverflow.com/questions/12239236/google-fuzzy-search-a-k-a-suggestions-what-techniques-are-in-use">search recommendations</a>. This post looks at how phonetic algorithms works, their limitations, and some alternatives.
<h2><b>Phonetic Algorithms - using sound rather than spelling</b></h2>
Phonetic algorithms work by breaking down words into sounds rather than spellings. One of the most commonly used phonetic algorithms is '<a href="https://en.wikipedia.org/wiki/Soundex">Soundex</a>', which was created to help analyse US census data in the early 20th century. Other phonetic algorithms are often developments and enhancements of Soundex, and it can serve as an example of how phonetic algorithms work in general.

The Soundex algorithm encodes words (typically names) as a letter followed by three numerical digits. The numerical digit grouping is given by the <a href="https://en.wikipedia.org/wiki/Place_of_articulation">place of articulation</a> of the different sounds in English. For example, b, f, p and v are given the code number 1, while d and t are given the code number 3.

To build up the full Soundex for a word, the first letter is kept and then all vowel sounds (including h and w) are removed. There are then additional rules for dealing with duplicates and other special cases. The result is a letter plus three number code for original string. This simplified representation of language is what makes Soundex and other similar phonetic algorithms a powerful tool for comparing words.
<h3>Phonetic Encoding</h3>
You can <a href="http://resources.rootsweb.ancestry.com/cgi-bin/soundexconverter">try out Soundex</a> using an online Soundex encoder. Running Soundex on a word or phrase will produce a four-character code. Have a play around and you will see some of the potential pit falls with Soundex-type encoding.

You will see that 'Robert' and 'Ropert' yield the same Soundex code (R163), which would be useful if 'Ropert' was a miss-spelling of 'Robert'. Rupert also has the code 'R163', and Rupert is less likely to just be a miss-spelling of Robert so this could be an incorrect result.

Soundex codes also struggle with longer strings. Jones and Johnson give J520 and J525 respectively, which is fine. If we include those as surnames to distinguish between two people with the name 'Robert', the Soundex stops being useful. Robert Jones and Robert Johnson will still return the code R163, since the Soundex code only considers the first few characters of a string.

<h2>Limitations of Phonetic Algorithms</h2>
Phonetic algorithms can be immensely useful for document search and data matching. They do have their limitations though, particularly when it comes to cultural differences in sounds and Latinised spellings - phonetic algorithms are fairly crude, and very specific to the languages they were designed for, usually either English or German. 'Out of the box' phonetic algorithms are also vulnerable to typos and other input errors, and do not have ways to distinguish the closeness of matches.

<h3>Input Limitations</h3>
There are certain inputs to phonetic algorithms that can be particularly challenging. These include:
<ul>
<li>Dependence on initial letter (e.g. f vs. ph): Phonetic algorithms typically build a code based on the first letter of the name or word of interest. This approach can easily be thrown by names with different letters for the same sound: for example 'Katherine' (Soundex: K365) and 'Catherine' (Soundex: C365).</li>
<li>The limit to the number of characters in a Soundex code (four) means that longer words can share the same code, even if they are rather different.</li>
<li>In real-world data, initials are often used rather than the full name, such as 'JK Rowling' rather than 'Joanne Rowling'. A phonetic algorithm would struggle to match these two names.</li>
<li>Noise intolerance (typos): Phonetic algorithms are not inherently resilient to typos in words entered into a database. Some typos such as 'Carl' and 'Cral' might be identified, but typos like 'geoge' instead of 'george' yield very different results.</li>
</ul>
<h3>Cultural Issues</h3>
Phonetic algorithms are designed around the sounds in a particular language. Other cultural challenges include:
<ul>
<li>Name equivalences or nick names. For example Jack and John may be exchanged</li>
<li>Name Ordering. Not all cultures use the 'First-Middle-Last' name ordering. Inconsistency in how these were recorded in a database can easily fool a phonetic algorithm.</li>
<li>The vagaries of the English language mean that there are often silent consonants in a name or word. These name not be consistently recorded in the name records of interest. For example 'Dayton' or 'Deighton', 'Cryton' or 'Crighton', 'Sinjin' or 'St. John' and so on. The variations in how these names are recorded will confuse the phonetic algorithm.</li>
<li>Differences in Latin spelling. There can be a number of ways to write or spell names using latin characters and English sounds. This can also originate from difference in hearing, or understanding. Often names have been entered into a database having listened to someone say their name - this can add further complications if the name is misheard.</li>
<li>Names containing particles. It is quite common to have names which contain '<a href="https://en.wikipedia.org/wiki/Nobiliary_particle">particles</a>' or <a href="https://en.wikipedia.org/wiki/Arabic_definite_article">articles</a>. These are supplementary parts of name such as 'von', 'de', 'al'. It is quite common for these to omitted or combined with the rest of the name - this can</li>
</ul>
<h3>Process Limitations</h3>
There are also some limitations in how phonetic algorithms tend to work.
<ul>
<li>Unranked Returns: Phonetic algorithms do not usually have any concept of a similarity ranking. The only thing that matters is that the encoding is the same. It is often more useful to know which returned records are closest to the search term.</li>
<li>Poor Precision: The simplifying effect of Soundex-type phonetic algorithms can over simplify names to the point that the technique loses usefulness. Entering a few names into <a href="http://resources.rootsweb.ancestry.com/cgi-bin/soundexconverter">Soundex encoder</a> will quickly show that many irrelevant names are often returned. This erodes the efficiency of any follow-up searches or data processing.</li>
</ul>
<h2>More Advanced Phonetic Algorithms</h2>
Soundex is well known and widespread, but many developments have been implemented in more recent phonetic algorithms. It may be worth exploring some of these alternatives before looking elsewhere.

The New York State Identification and Intelligence System (<a href="http://en.wikipedia.org/wiki/NYSIIS" rel="nofollow">NYSIIS</a>) was introduced in 1970s as an improvement to Soundex. Key improvements included provision for Hispanic names and probability tables relating to the names expected in New York State at the time. The <a href="https://en.wikipedia.org/wiki/Daitch%E2%80%93Mokotoff_Soundex">Daitch-Mokotoff Soundex</a> was developed in the 1980s to deal better with Germanic and Slavic surnames. <a href="https://en.wikipedia.org/wiki/Metaphone">Metaphone</a> and <a href="https://en.wikipedia.org/wiki/Metaphone#Double_Metaphone">Double Metaphone</a> were developed from 1990s to 2000s and attempt to improve Soundex by using information about variations and inconsistencies in spellling. Another variant is the <a href="https://en.wikipedia.org/wiki/Match_rating_approach">Match Rating Approach</a>, which also provides a measure of how similar two names or words are.
