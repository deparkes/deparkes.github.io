---
layout: post
title: Markdown Contents Table
date: 2021-12-22 21:18:25.000000000 +00:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- Computing
tags:
- awk
- bash
- grep
- linux
- markdown
- regex
- sed
author:
  display_name: deparkes
permalink: "/2021/12/22/markdown-contents-table/"
---
The original inspiration for this post is <a href="https://medium.com/@acrodriguez/one-liner-to-generate-a-markdown-toc-f5292112fd14">this medium post</a> which shows how a single (long) command can generate a markdown contents table for GitHub. The command is specifically for GitHub as it relies on the auto-generated links that the site makes, rather than needing to add links manually.

In my post I wanted to a) see about making a similar command for Linux (rather than OSX) and b) understand in a bit more detail what exactly the elements of the command did.
If you want to just cut to the chase, here is the command:

```bash
grep -E "#{1,5} " input_file.md | \
sed -E 's/(#+) (.+)/\1:\2/g' | \
sed -E 's/\r$//g' | \
awk -F ":" '{x=$2; gsub(/#/, " ", $1); gsub(/ /, "-", $2); print $1 " - [" x "](" tolower($2) ")"}'
```

<h2>Markdown Contents Table</h2>
I'm going to build up the elements of the full command, which uses a pipeline of a few different tools.
Regex appears throughout, so if you are not familiar you may want to <a href="https://www.howtogeek.com/69451/how-to-use-basic-regular-expressions-to-search-better-and-save-time/">brush up</a>. <a href="https://regex101.com/">Online regex testing tools</a> can also be really useful to understand what is going on.
<h3>Example Input File</h3>
The starting point will be this simple markdown file, "simple.md".

```markdown
# Title
## Heading
Content
### Subheading with space
More content
Do not include this ### line
```


<h3>Find Heading Lines - grep</h3>
The first command uses <a href="https://www.howtogeek.com/496056/how-to-use-the-grep-command-on-linux/">grep</a> to find lines which start with between 1 and 5 hash symbols.

```bash
grep -E "^#{1,5} " simple.md
```

Running just this command on its own with our simple.md input file, we get the following output. Only lines which start with a hash symbol are included.

```
# Title
## Heading
### Subheading with space
```

<h3>Split Hash Symbols From Text - sed</h3>
Next we <a href="https://www.howtogeek.com/438882/how-to-use-pipes-on-linux/">pipe</a> the output of the grep command into <a href="https://www.howtogeek.com/666395/how-to-use-the-sed-command-on-linux/">sed</a>, which can be used to find and replace via the command line.

```bash
grep -E "#{1,5} " simple.md | sed -E 's/(#+) (.+)/\1:\2/g'
```

Find and replace in sed is done by 's/find/replace/g'
In this case the regex looks for two groups: the first is one or more # symbols. The second is one or more of any character.
The resulting groups are then output, separated by a ':' symbol. We can see that the results come out as the following.

```
#:Title
##:Heading
###:Subheading with space
```

<h3>Handling Windows Line Endings - sed</h3>
This second sed command is optional, or at least won't always be needed. In my case I was using a system which had files shared/mounted between both Linux and Windows which resulted in confusion about <a href="https://stackoverflow.com/questions/426397/do-line-endings-differ-between-windows-and-linux">line endings</a>.

```bash
grep -E "#{1,5} " simple.md | sed -E 's/(#+) (.+)/\1:\2/g' | sed -E 's/\r$//g'
```

The resulting output looks identical, but the line endings are now in the Linux style, which is important for the next command.

```
#:Title
##:Heading
###:Subheading with space
```

<h3>Printing the Final Output- awk</h3>
The final tool in the pipeline is <a href="https://www.howtogeek.com/562941/how-to-use-the-awk-command-on-linux/">awk</a>, a command-line text manipulation tool.

```bash
grep -E "#{1,5} " simple.md | \
sed -E 's/(#+) (.+)/\1:\2/g' | \
sed -E 's/\r$//g' | \
awk -F ":" '{x=$2; gsub(/#/, " ", $1); gsub(/ /, "-", $2); print $1 " - [" x "](" tolower($2) ")"}'
```

We specify the colon ':' as a field separator using the '-F' flag, so that the # symbols and text can be handled separately.
We begin by capturing the second field in a variable called 'x'. This allows us to refer back to the original, unmodified second field later.
We use gsub commands which allow find and replace within a single field in awk. The first gsub command converts # into ' '. The second gsub command converts any space between words in a heading or title to a hyphen.

I'm not sure why square brackets were included in the regex in the original medium post as they are <a href="https://thepugautomatic.com/2012/09/brackets-in-regular-expressions/">usually used</a> to provide multiple options to match. It may be that originally this had other things to replace with hyphen, such as underscores.
Finally we print:
- the modified first field (i.e. the spaces that replaced the # symbols)
- the original second field in square brackets (i.e. the heading text)
- the second field, with spaces replaced with hyphens and in lower case

```
  - [Title](title)
   - [Heading](heading)
    - [Subheading with space](subheading-with-space)
```

