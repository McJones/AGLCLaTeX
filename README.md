# AGLCLaTeX
An Biblatex AGLC style for LaTeX.

For general stylistic matters, refer to version 3 of the Australian Guide to Legal Citation.

## General

AGLCLaTeX provides three citation commands:
- ```\cite``` - creates a footnote for a single citation.
- ```\cites``` - creates a footnote for multiple citations.
- ```\textcite``` - prints an in-text citation for a single citation.

Full stops are automatically placed at the end of footnote citations.

Pinpoint references should be enclosed in the postnote field: ```\cite[354]{key2000}```.

Pinpoints will usually be printed as they appear, and refer to page numbers. Some sources automatically convert the pinpoint to paragraph numbers in accordance with the AGLC (ie, the source doesn't include page numbers). To print paragraph numbers instead of page numbers (for sources that don't do this automatically) use the ```\para{}``` command: ```\cite[\para{354}]{key2000}```. If additional numbers follow, it may be necessary to include empty curly braces after the ```\para{}``` command: ```\cite[528, \para{57}{} n 6, 529 \para{64}]{key2000}```.

Spans of pinpoint references should be separated by two hyphens and no space:
- ```\cite[431--2]{key2000}``` - for page numbers.
- ```\cite[57--63]{key2000}``` - for sources that always refer to paragraph numbers by default.
- ```\cite[\para{57--63}]{key2000}``` - to use paragraphs with a source that uses page numbers by default.
- ```\cite[312--13 \para{15--18}]{key2000}``` - to use pages and paragraphs with a source that uses page numbers by default.

Introductory signals such as 'See', 'See, eg,' and 'See also' should be enclosed in the prenote field: ```\cite[See][293]{key2000}```. Note that if no pinpoint is included, an empty set of square brackets should be included after the prenote, otherwise the prenote will be taken to be the postnote: ```\cite[See, eg,][]{key2000}```.
