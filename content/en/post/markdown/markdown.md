---
# Documentation: https://wowchemy.com/docs/managing-content/

title: "Markdown how not to become crazy"
subtitle: "impossible"
summary: ""
authors: [Malkov Roman Sergeevich]
tags: []
categories: []
date: 2022-05-14T12:57:03+03:00
lastmod: 2022-05-14T12:57:03+03:00
featured: false
draft: false

# Featured image
# To use, add an image named `featured.jpg/png` to your page's folder.
# Focal points: Smart, Center, TopLeft, Top, TopRight, Left, Right, BottomLeft, Bottom, BottomRight.
image:
  caption: ""
  focal_point: ""
  preview_only: false

# Projects (optional).
#   Associate this post with one or more of your projects.
#   Simply enter your project's folder or file name without extension.
#   E.g. `projects = ["internal-project"]` references `content/project/deep-learning/index.md`.
#   Otherwise, set `projects = []`.
projects: []
---
## Co to jest?
Markdown (pronounced markdown) is a lightweight markup language designed to indicate formatting in plain text while maintaining human readability as much as possible, and suitable for machine conversion into advanced publishing languages ​​(HTML, Rich Text, and others).
To create a title, use the sign ( # ), for example:
1 # This is heading 1
2 ## This is heading 2
3 ### This is heading 3
4 #### This is heading 4
To make text bold, enclose it in double asterisks:
1 This text is **bold**.
To make text italic, enclose it in single asterisks:
1 This text is *italic*.
To make text bold and italic, enclose it in triple
asterisks:
1 This is text is both ***bold and italic***.
Quote blocks are created using the > symbol:
1 > The drought had lasted now for ten million years, and the reign of
the terrible lizards had long since ended. Here on the Equator, in
the continent which would one day be known as Africa, the battle
for existence had reached a new climax of ferocity, and the victor
was not yet in sight. In this barren and desiccated land, only the
small or the swift or the fierce could flourish, or even hope to
survive.
↪
↪
↪
↪
↪
↪
An unordered (bulleted) list can be formatted with asterisks or dashes:
1 - List item 1
2 - List item 2
3 - List item 3
To nest one list within another, indent the elements of the child list:
34 Lab 3. Markdown
1 - List item 1
2 - List item A
3 - List item B
4 - List item 2
An ordered list can be formatted with the appropriate numbers:
1 1. First instruction
2 1. Second instruction
3 1. Third instruction
To nest one list within another, indent the elements of the child list:
1 1. First instruction
2 1. Sub instruction
3 1. Sub-instruction
4 1.Second instruction
The Markdown syntax for an embedded link consists of a [link text] part representing the text of the hyperlink and a (file-name.md) part representing the URL or file name
which is referenced:
1 [link text](filename.md)
Markdown supports both embedding code snippets in a sentence and
placement between offers in the form of separate fenced blocks. Fenced
code blocks are an easy way to highlight syntax for code snippets. General
format of fenced code blocks:
1 ``` languages
2 your code goes in here
3 ```
Superscripts and subscripts:
𝐻2
written as
1H~2~O
2
ten
written as
1 2^10^
Intratext formulas are made similar to LaTeX formulas. For example, the formula
sin2
(𝑥) + cos2
(𝑥) = 1 will be written as
1 $\sin^2 (x) + \cos^2 (x) = 1$
Off formulas:
sin2
(𝑥) + cos2
(𝑥) = 1
{#eq:eq:sin2+cos2} with reference in text "See formula ([-@eq:eq:sin2+cos2])." written as
1 $$
2 \sin^2 (x) + \cos^2 (x) = 1
3 $$ {#eq:eq:sin2+cos2}
four
5 See formula ([-@eq:eq:sin2+cos2]).