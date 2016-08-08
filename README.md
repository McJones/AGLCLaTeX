# AGLCLaTeX
A Biblatex style implementing version 3 of the Australian Guide to Legal Citation

The Australian Guide to Legal Citation ('AGLC') is in my opinion one of the best and most flexible citation systems ever devised. This is despite its many detailed rules; in fact, it is probably the detail that contributes most to its flexibility, as it is very easy to find a close match for any source type.

It is the citation system I learned when I was in law school, and it is currently the most widely used system for legal citations in Australia. The AGLC is published by the Melbourne University Law Review Association, and is available from the [University of Melbourne website](http://law.unimelb.edu.au/mulr/aglc/about) as a read-only PDF and to purchase in hard or soft copy.

Almost all of this is original work, built from scratch simply by following the Biblatex documentation. Small parts have been taken from various forum posts where I ran into difficulty. The parts for storing previous footnote numbers (the cite:save bibmacro) and some code for printing only surnames for the above n citations were taken from [Will Hardy's](https://github.com/willhardy/aglc) attempt at implementing the AGLC, so thanks to him.

The decision to create an entirely new style from scratch was due to the complexity of the AGLC. None of the existing styles was particularly suitable to modify, and while I could have built upon one and _heavily_ modified it, it seemed easier to simply take full control. This allowed me to learn the workings of Biblatex in some considerable detail. Additionally, as far as I could tell, Will was the only other person to attempt this and publish the result, but he was working with version 2 of the AGLC rather than version 3 (and there have been significant changes and expansions), and did not attempt a 'complete' solution.

## Contents

- [General](#general)
- [Domestic sources](#domestic-sources)
  - [Cases](#cases)
  - [Legislative materials](#legislative-materials)
- [Secondary sources](#secondary-sources)
  - [Journal articles](#journal-articles)
  - [Books](#books)
  - [Other sources](#other-sources)
- [International materials](#international-materials)
  - [Treaties](#treaties)
  - [UN Materials](#united-nations-materials)
  - [ICJ and PCIJ](#international-court-of-justice-and-permanent-court-of-international-justice)
  - [International arbitral and tribunal decisions](#international-arbitral-and-tribunal-decisions)
  - [International criminal tribunals and courts](#international-criminal-tribunals-and-courts)

## General

AGLCLaTeX provides three basic citation commands:
- ```\cite{key2000}``` - creates a footnote for a single citation.
- ```\cites{key1}{key2}{key3}{etc}``` - creates a footnote for multiple citations.
- ```\textcite{key2000}``` - prints an in-text citation for a single citation.

### General format of footnotes

Full stops are automatically placed at the end of footnote citations.

```\cites{key1}{key2}{key3}{etc}``` will print each source in a footnote separated by a semicolon (';').

Pinpoint references should be enclosed in the postnote field: ```\cite[354]{key2000}```.

Pinpoints will usually be printed as they appear, and refer to page numbers. Some sources automatically convert the pinpoint to paragraph numbers in accordance with the AGLC (ie, the source doesn't include page numbers). To print paragraph numbers instead of page numbers (for sources that don't do this automatically) use the ```\para{}``` command: ```\cite[\para{354}]{key2000}```. If additional numbers follow, it may be necessary to include empty curly braces after the ```\para{}``` command: ```\cite[528, \para{57}{} n 6, 529 \para{64}]{key2000}```.

Spans of pinpoint references should be separated by two hyphens and no space:
- ```\cite[431--2]{key2000}``` - for page numbers.
- ```\cite[57--63]{key2000}``` - for sources that always refer to paragraph numbers by default.
- ```\cite[\para{57--63}]{key2000}``` - to use paragraphs with a source that uses page numbers by default.
- ```\cite[312--13 \para{15--18}]{key2000}``` - to use pages and paragraphs with a source that uses page numbers by default.

### Introductory signals

Introductory signals such as 'See', 'See, eg,' and 'See also' should be enclosed in the prenote field: ```\cite[See][293]{key2000}```. Note that if no pinpoint is included, an empty set of square brackets should be included after the prenote, otherwise the prenote will be taken to be the postnote: ```\cite[See, eg,][]{key2000}```.

### Sources referring to other sources

AGLCLaTeX provides four citation commands for sources referring to other sources:

- ```\quoting{key1}{key2}``` - where the first source quotes the second source,
- ```\quotedin{key1}{key2}``` - where the first source is quoted in the second source,
- ```\citing{key1}{key2}``` - where the first source refers to the second source, and
- ```\citedin{key1}{key2}``` - where the first source is referred to in the second source.

These are used like ```\cites``` and all support prenotes for introductory signals and postnotes for pinpoints.

Note that these should only be used for two sources. Citing more than two sources in this way is currently not supported and will produce incorrect results.

### Subsequent references

In compliance with the AGLC:

- Repeated citations print 'Ibid' and a pinpoint or other postnote, unless:
- the postnote is identical to the previous citation, or
- there are multiple sources in the previous footnote.

If the postnote is identical, only 'Ibid' is printed. If there are multiple sources in the previous footnote, the surname of the author or editor is printed, followed by ', above n' and the footnote number of the _first_ instance of that source, unless the AGLC requires to be printed in full. If the pinpoint is different, a pinpoint is printed. This requires the document to be compiled _twice_ after running Bibtex.

**AGLCLaTeX does not currently support short titles**

Dates for sources should be in ```YYYY-MM--DD``` format: ```Date = {2000-01-01}```. Individual authors and editors should be separated with 'and' (do not use commas, even for more than two authors): ```Author = {John Smith and Jane Doe}```. Corporate authors should be enclosed in double curly braces to prevent unintended splitting: ```Author: {{Department of Foreign Affairs and Trade}}```.

**AGLCLaTeX does not currently support the headings, titles or bibliography format of the AGLC**

## Domestic sources

### Cases

AGLCLaTex provides for several different types of cases, as covered by the AGLC:

- ```@case-gen-volume``` - for reported cases in a report series arranged by volume,
- ```@case-gen-year``` - for reported cases in a report series arranged by year (which may include volumes within that year),
- ```@case-gen-mnc``` - for unreported cases with a medium neutral citation,
- ```@case-gen-unreported``` - for unreported cases without a medium neutral citation, and
- ```@arbitration``` - for domestic arbitrations.

Administrative decisions that are reported or unreported should be cited as cases.

Refer to the AGLC for formatting rules. Note that:
- administrative decisions typically use 'and' instead of 'v' to separate party names,
- judges' names should conform with the AGLC rules, and
- if necessary, additional information can be included in the postnote.

#### Reported decisions

- _R v Tang_ (2008) 237 CLR 1.

```
@case-gen-volume{tang2008,
Title  = {R v Tang},
Year   = {2008},
Volume = {237},
Series = {CLR},
Pages  = {1}}
```

- _Bakker v Stewart_ [1980] VR 70.

```
@case-gen-year{bakker1980,
Title  = {Bakker v Stewart},
Year   = {1980},
Series = {VR},
Pages  = {17}}
```

- _Rowe v McCartney_ [1976] 2 NSWLR 72.

```
@case-gen-year{rowe1976,
Title  = {Rowe v McCartney},
Year   = {1976},
Volume = {2},
Series = {NSWLR},
Pages  = {72}}
```

The ```Pages``` field can be replaced with a different identifier (such as a paragraph number) if that's how the reports are set out.

Both ```@case-gen-volume``` and ```@case-gen-year``` allow for the ```venue``` field, which may specify the court if relevant or necessary:

- _Aldrick v EM Investments (Qld) Pty Ltd_ [2000] 2 Qd R 346 (Court of Appeal).

```
@case-gen-year{aldrick2000,
Title  = {Aldrick v EM Investments (Qld) Pty Ltd},
Year   = {2000},
Volume = {2},
Series = {Qd R},
Pages  = {346},
Venue  = {Court of Appeal}}
```

#### Unreported decisions with a Medium Neutral Citation

- _Quarmby v Keating_ [2009] TASSC 80 (9 September 2009).

```
@case-gen-mnc{quarmby2009,
Title  = {Quarmby v Keating},
Date   = {2009-09-09},
Venue  = {TASSC},
Number = {80}}
```

#### Unreported decisions without a Medium Neutral Citation

- _Barton v Chibber_ (Unreported, Supreme Court of Victoria, Hampel J, 29 June 1989).

```
@case-gen-unreported{barton1989,
Title  = {Barton v Chibber},
Venue  = {Supreme Court of Victoria},
Author = {Hampel J},
Date   = {1989-06-29}}
```

#### Case history

AGLCLaTeX supports two citation commands for affirmed and reversed decisions:

- ```\affirmed{key1}{key2}``` - where the first source was affirmed (upheld) by the second source, and
- ```\reversed{key1}{key2}``` - where the first source was reversed by the second source.

These are used like ```\cites``` and both support prenotes for introductory signals and postnotes for pinpoints.

Note that these should only be used for two sources. Citing more than two sources in this way is currently not supported and will produce incorrect results.

#### Quasi-judicial decisions (administrative decisions and arbitrations)

Administrative decisions should cited as cases (ie, using ```@case-gen-volume```, ```@case-gen-year```, ```@case-gen-mnc``` or ```@case-gen-unreported```).

Arbitrations use the ```@arbitration``` entry type. Arbitrations may or may not have a title; if an arbitration does not the title can be safely omitted.

```
@arbitration{beckman1988,
Title  = {Beckman Instruments Inc v Overseas Private Investment Corporation},
Note   = {Award and Opinion},
Venue  = {American Arbitration Association Commercial Arbitration Tribunal},
Type   = {Case},
Number = {16 199 00209 87G},
Date   = {1988-02-20}}
```

```
@arbitration{sandline1998,
Title  = {Sandline International v Papua New Guinea},
Note   = {Award},
Venue  = {Sir Edward Somers, Sir Michael Kerr and Sir Daryl Dawson},
Date   = {1998-10-09}}
```

```
@arbitration{nai1930,
Note   = {Final Award},
Venue  = {Netherlands Arbitration Institute},
Type   = {Case},
Number = {1930},
Date   = {1999-10-12}}

```

**AGLCLaTeX does not currently support arbitrations reported in other sources (eg, reported series and books).**

#### Transcripts of proceedings

AGLCLaTeX provides for two kinds of court transcripts:

- ```@case-transcript``` - for citing court transcripts in general, and
- ```@case-transcript-hca``` - for citing High Court of Australia transcripts _from July 2003 onwards_.

If appropriate, the speaker's name can be included in the postnote alongside the pinpoint.

High Court of Australia transcripts are cited very similarly to unreported decisions with Medium Neutral Citations.

```
@case-transcript{celano2009,
Title  = {Celano v Swan},
Venue  = {County Court of Victoria},
Number = {09/0867},
Author = {Judge Lacava},
Date   = {2009-08-27}}
```

```
@case-transcript-hca{ruhani2005,
Title  = {Ruhani v Director of Police},
Date   = {2005-04-19},
Number = {205}}
```

#### Submissions in Cases

```
@case-submission{agcth2005,
Author    = {Attorney-General (Cth)},
Title     = {Outline of Submissions of the Attorney-General of the Commonwealth as Amicus Curiae},
Maintitle = {Human Society International Inc v Kyodo Senpaku Kaisha Ltd},
Number    = {NSD 1519/2004},
Date      = {2005-01-25}}
```

#### Subsequent References

In accordance with the AGLC:
- 'Ibid' is used for all cases and related materials, and
- 'above n' is not used for cases and related materials.

### Legislative materials

#### Statutes (Acts of Parliament), Australian Constitutions, and Delegated Legislation

AGLCLaTeX uses the ```@act-gen``` entry type for statutes, constitutions and delegated legislation:

```
@act-gen{crimesact1958vic,
Title    = {Crimes Act},
Year     = {1958},
Location = {Vic}}
```

```
@act-gen{ausconstitution,
Title = {Australian Constitution}}
```

```
@act-gen{policeregs2003vic,
Title    = {Police Regulations},
Year     = {2003},
Location = {Vic}}
```

#### Quasi-Legislative Materials

AGLCLaTeX provides for several different types of quasi-legislative materials, as covered by the AGLC:

- ```@gazette``` - government gazettes,
- ```@govt-order``` - orders and rulings of government instrumentalities and officers,
- ```@non-govt-order``` - legislation delegated to non-government entities, and
- ```@practice-direction``` - court practice directions and practice notes.

Gazette notices can specify an author and a notice title, or neither.

Gazette notice with author and title:

```
@gazette{gaz1997cth,
Author    = {Minister for Lands (WA)},
Title     = {\textit{Land Acquisition and Public Works Act 1902 --- Native Title Act 1993} (Commonwealth) --- Notice of Intention to Take Land for a Public Work},
Location  = {Western Australia},
Maintitle = {Western Australian Government Gazette}
Number    = {27},
Date      = {1997-02-18},
Pages     = {1142}}
```
Gazette with notice title:

```
@gazette{gaz1989act,
Title     = {Australian Capital Territory Teaching Service},
Location  = {Australian Capital Territory},
Maintitle = {Australia Capital Territory Gazette},
Number    = {1},
Date      = {1989-05-24},
Pages     = {3}}
```

Gazette without author or notice title:

```
@gazette{gaz2004cth,
Location  = {Commonwealth},
Maintitle = {Gazette: Special},
Number    = {S 489},
Date      = {2004-12-01}}
```

Orders and rulings of government instrumentalities and officers

```
@govt-order{ato2005,
Author = {{Australian Taxation Office}},
Title  = {Income Tax: Carrying on a Business as a Professional Artist},
Number = {TR 2005/1},
Date   = {2005-01-12}}
```

Legislation delegated to non-government entities:

```
@non-govt-order{asx2010,
Institution = {Australian Securities Exchange},
Title       = {Listing Rules},
Date        = {2010-01-11}}
```

Court practice directions and practice notes:

```
@practice-direction{hcapd2006,
Institution = {High Court of Australia},
Type        = {Practice Direction},
Number      = {3 of 2006},
Title       = {Amendment of Practice Directio No 1 of 2000},
Date        = {2006-09-05}}
```

#### Bills

AGLCLaTeX uses the ```@bill-gen``` entry type for bills, which are otherwise cited like regular legislation:

```
@bill-gen{corpamendbill2005cth,
Title    = {Corporations Amendment Bill No 1},
Year     = {2005},
Location = {Cth}}
```

#### Explanatory Memoranda, Statements and Notes

AGLCLaTeX uses the ```@bill-gen-exp``` entry type for explanatory memorada, statements and note, which are otherwise cited like regular legislation, but with the type of document specified:

```
@bill-gen-exp{exphrcharter2006vic,
Type     = {Explanatory Memorandum},
Title    = {Charter of Human Rights and Responsibilities Bill},
Year     = {2006},
Location = {Vic}}
```

#### Legislative history

AGLCLaTeX provides for seven different types of commands designed for legislative history. These can be used, if appropriate, for other sources:

- ```\asamendedby{key1}{key2}``` - where the first source is as amended by the second source,
- ```\lateramendedby{key1}{key2}``` - where the first source was later amended by the second source,
- ```\amending{key1}{key2}``` - where the first source is amending the second source,
- ```\asrepealedby{key1}{key2}``` - where the first source was repealed by the second source,
- ```\repealing{key1}{key2}``` - where the first source is repealing the second source,
- ```\asinsertedby{key1}{key2}``` - where the first source was inserted by the second source, and
- ```\inserting{key1}{key2}``` - where the first source is inserting the second source.

These are used like ```\cites``` and all support prenotes for introductory signals and postnotes for pinpoints.

Note that these should only be used for two sources. Citing more than two sources in this way is currently not supported and will produce incorrect results.

#### Subsequent References

In accordance with the AGLC:
- 'Ibid' is used for all legislation and related materials, and
- 'above n' is not used for legislation and related materials.

## Secondary Sources

### Journal Articles

AGLCLaTeX provides for two kind of academic journal article:

- ```@article-volume``` - articles published in journals arranged by volume, and
- ```@article-year``` - articles published in journals arranged by year.

These are substantially the same in terms of database entries. They may or may not include an article type (for unsigned articles), an issue number or a URL:

Article published in a journal arranged by volume:

```
@article-volume{kenyon1998,
Author  = {Andrew Kenyon},
Title   = {Problems with Defamation Damages?},
Year    = {1998},
Volume  = {24},
Journal = {Monash University Law Review},
Pages   = {70}}
```

Article published in a journal arranged by year:

```
@article-year{dockray1985,
Author  = {Martin Dockray},
Title   = {Why Do We Need Adverse Possession?},
Year    = {1985},
Journal = {Conveyancer and Property Lawyer},
Pages   = {272}}
```

Unsigned article published in a journal arranged by volume:

```
@article-volume{hlr2005,
Type    = {Note},
Title   = {Unfixing \textit{Lawrence}},
Year    = {2005},
Volume  = {118},
Journal = {Harvard Law Review},
Pages   = {2858}}
```

Article with issue number:

```
@article-volume{masters2008,
Author  = {Jeremy Masters},
Title   = {Easing the Parting},
Year    = {2008},
Volume  = {82},
Issue   = {11},
Journal = {Law Institute Journal},
Pages   = {68}}
```

Forthcoming article:

```
@article-year{foster2009,
Author  = {Michelle Foster},
Title   = {\textit{Non-Refoulement} on the Basis of Socio-Economic Deprivation: The Scope of Complementary Protection in International Human Rights Law},
Year    = {2009},
Journal = {New Zealand Law Review},
Pages   = {(forthcoming)}}
```

Article published in parts:

```
@article-year{gooderson1966pt2,
Author  = {R N Gooderson},
Title   = {Claim of Rights and Dispute of Title},
Part    = {1},
Year    = {1966},
Journal = {Cambridge Law Journal},
Pages   = {216}}
```

Article published in an electronic journal with pages:

```
@article-volume{lewins2006,
Author  = {Kate Lewins},
Title   = {What's the \textit{Trade Practices Act} Got to Do with It? Section 74 and Towage Contracts in Australia},
Year    = {2006},
Volume  = {13},
Issue   = {1},
Journal = {eLaw Journal: Murdoch University Electronic Journal of Law},
Pages   = {58},
URL     = {https://elaw.murdoch.edu.au/archives/issues/2006/1/eLaw_Lewins_13_2006_05.pdf}}
```

Article published in an electronic journal without pages:

```
@article-volume{vancaenegem1996,
Author  = {William van Caenegem},
Title   = {Copyright Liability for the Playing of ``Music on Hold'' --- \textit{Telstra Corporation Ltd v Australasian Prforming Rights Association Ltd}},
Year    = {1996},
Volume  = {2},
Journal = {High Court Review},
URL     = {http://www.austlii.edu.au/au/journals/HCRev/1996/9.html}}
```

Symposia:

```
@article-volume{mulr2002,
Type    = {Symposium},
Title   = {Contemporary Human Rights in Australia},
Year    = {2002},
Volume  = {26},
Journal = {Melbourne University Law Review},
Pages   = {251}}
```

### Books

AGLCLaTeX provides for three kinds of book-type entries:

- ```@book``` - books with authors or editors (or both),
- ```@chapter``` - chapters in edited books, and
- ```@translated-book``` - books which have been translated into English.

'et al' is automatically added where there are four or more authors or editors. '(ed)' or '(eds') are automatically after the editor(s) name(s).

#### Books with authors, editors, or both

Book with author, title, publisher and year:

```
@book{dworkin1968,
Author    = {Ronald Dworkin},
Title     = {Law's Empire},
Publisher = {Harvard University Press},
Year      = {1968}}
```

Book with authors, title, publisher, edition and year:

```
@book{castan2004,
Author    = {Sarah Joseph and Jenny Schultz and Melissa Castan},
Title     = {The International Covenant on Civil and Political Rights: Cases, Materials, and Commentary},
Publisher = {Oxford University Press},
Edition   = {2},
Year      = {2004}}
```

Book with editor, title, publisher and year:

```
@book{frey1985,
Editor    = {R G Frey},
Title     = {Utility and Rights},
Publisher = {Basil Blackwell},
Year      = {1985}}
```

Book with editors, title, publisher and year:

```
@book{neyers2007,
Editor    = {Jason W Neyers and Erika Chamberlain and Stephen G A Pitel},
Title     = {Emerging Issues in Tort Law},
Publisher = {Hart Publishing},
Year      = {2007}}
```

Book specifying year of first publication and year of edition:

```
@book{hobbes1909,
Author    = {Thomas Hobbes},
Title     = {Leviathan},
Publisher = {Clarendon Press},
Origyear  = {1651},
Year      = {1909}}
```

Book specifying year of first publication, year of edition and volume:

```
@book{hale1971vol1,
Author    = {Sir Matthew Hale},
Title     = {Historia Placitorum Coronae},
Publisher = {London Professional Books},
Origyear  = {1736},
Year      = {1971},
Volume    = {1}}
```

Book with revised edition:

```
@book{cohn1968,
Author    = {E J Cohn and W Zdzieblo},
Title     = {Manual of German Law},
Publisher = {Oceana Publications},
Edition   = {2},
Type      = {revised},
Year      = {1968}}
```

#### Chapters in edited books

These are cited almost exactly the same as for books, but ```title``` refers to the title of the chapter, and ```booktitle``` refers to the title of the book:

```
@chapter{russell2008,
Author    = {Meg Russell},
Title     = {Reform of the House of Lords: Lessons for Bicameralism},
Editor    = {Nicholas Aroney and Scott Prasser and J R Nethercote},
Booktitle = {Restraining Elective Dictatorship: The Upper House Solution?},
Publisher = {University of Western Australia Press},
Year      = {2008}}
```

#### Translated books

Translated books are essentially the same as regular books, but require extra fields:

```
@translated-book{sartre1958,
Author     = {Jean-Paul Sartre},
Title      = {Being and Northingness: An Essay on Phenomenological Ontology},
Translator = {Hazel E Barnes},
Publisher  = {Methuen},
Year       = {1958},
Origtitle  = {L'Entre et le N\'{e}ant},
Origyear   = {1953}}
```

### Other Sources

#### Government Documents

AGLCLaTeX provides for nine kinds of government documents:

- ```@hansard``` - for parliamentary debates/Hansard,
- ```@parl-paper``` - for parliamentary papers,
- ```@parl-research-paper``` - for parliamentary research papers,
- ```@parl-comm-rep``` - for parliamentary committee reports,
- ```@digest``` - for bills digests and alert digests,
- ```@parl-comm-evidence``` - for evidence to parliamentary committees,
- ```@royal-comm-rep``` - for Royal Commission reports,
- ```@lrc-rep``` - for Law Reform Commission reports, and
- ```@debate``` - for Australian Constitutional Convention Debates.

Parliamentary debates/Hansard:

```
@hansard{hansard2008cth,
Location = {Commonwealth},
Venue    = {Senate},
Date     = {2008-06-18}}
```

```
@hansard{hansard2006vic,
Location = {Victoria},
Venue    = {Legislative Assembly},
Date     = {2006-05-04}}
```

Parliamentary papers:

```
@parl-paper{cthparlpaper211,
Location = {Commonwealth},
Title    = {Australia's Aid Program in the Pacific: Joint Standing Committee on Foreign Affairs, Defence and Trade},
Number   = {211},
Year     = {2007}}
```

Parliamentary research papers, notes and briefs:

```
@parl-research-paper{bennet2008,
Author      = {Scott Bennett},
Title       = {The Rise of the Australian Greens},
Type        = {Research Paper},
Number      = {8},
Institution = {Parliamentary Library},
Venue       = {Parliament of Australia},
Year        = {2008}}
```

```
@parl-research-paper{robertson2007,
Author      = {Jeffrey Robertson},
Title       = {North Korean Nuclear Issues and the Role of Parliamentary Diplomacy},
Type        = {Research Note},
Number      = {23},
Institution = {Parliamentary Library},
Venue       = {Parliament of Australia},
Year        = {2007}}
```

Parliamentary committee reports:

```
@parl-comm-rep{lrcparl2009,
Institution = {Law Reform Committee},
Venue       = {Parliament of Victoria},
Title       = {Inquiry into Alternative Dispute Resolution and Restorative Justice},
Year        = {2009}}
```

```
@parl-comm-rep{slcrc2006,
Institution = {Senate Legal and Constitutional References Committee},
Venue       = {Parliament of Australia},
Title       = {Administration and Operation of the Migration Act 1958},
Year        = {2006}}
```

Bill digests and alert digests:

```
@digest{sscsb2007,
Author = {Senate Standing Committee for the Scrutiny of Bills},
Venue  = {Parliament of Australia},
Type   = {Alert Digest},
Number = {9 of 2007},
Date   = {2007-08-13}}
```

```
@digest{lrcparl2008,
Author = {Legislation Review Committee},
Venue  = {Parliament of New South Wales},
Type   = {Legislation Review Digest},
Number = {13 of 2008},
Date   = {2008-11-10}}
```

Evidence to parliamentary committees:

```
@parl-comm-evidence{sscfadt2007,
Institution = {Senate Standing Committee on Foreign Affairs, Defence and Trade},
Venue       = {Parliament of Australia},
Location    = {Canberra},
Date        = {2007-02-26}}
```

Royal Commission reports:

```
@royal-comm-rep{rcadc1991,
Location    = {Commonwealth},
Institution = {Royal Commission into Aboriginal Deaths in Custody},
Title       = {National Report},
Year        = {1991}}
```

Law Reform Commission reports:

```
@lrc-rep{vlrc2008,
Institution = {Victorian Law Reform Commission},
Title       = {Civil Justice Review},
Type        = {Report},
Number      = {14},
Year        = {2008}}
```

```
@lrc-rep{lrc1980,
Institution = {Law Reform Commission},
Title       = {Reform of Evidence Law},
Type        = {Discussion Paper},
Number      = {16},
Year        = {1980}}
```

Australian Constitutional Convention Debates:

```
@debate{ordafc1897,
Title    = {Official Record of the Debates of the Australasian Federal Convention},
Location = {Sydney},
Date     = {1897-09-02}}
```

```
@debate{ornacd1897,
Title    = {Official Report of the National Australasian Convention Debates},
Location = {Adelaide},
Date     = {1897-03-29}}
```

#### Submissions to public inquiries

```
@submission{mobil2007,
Author      = {Mobil Oil Australia},
Number      = {25},
Institution = {Australian Competition and Consumer Commission},
Title       = {Inquiry into the Price of Unleaded Petrol},
Date        = {2007-07-27}}
```

```
@submission{hrlrc2009,
Author      = {Human Rights Law Resource Centre},
Number      = {21},
Institution = {Senate Standing Committee on Legal and Constitutional Affairs},
Venue       = {Parliament of Australia},
Title       = {Inquiry into the Anti-Terrorism Laws Reform Bill 2009},
Date        = {2009-09-11}}
```

```
@submission{vacc2005,
Author      = {Victorian Automobile Chamber of Commerce},
Institution = {Road Safety Committee},
Venue       = {Parliament of Victoria},
Title       = {Inquiry into Driver Distraction},
Date        = {2005-10}}
```

```
@submission{aida2008,
Author      = {Australian Indigenous Doctors' Association},
Number      = {187},
Institution = {Northern Territory Emergency Response Review},
Date        = {2008-08-22}}
```

#### Legal encyclopedia

```
@legal-encyclopedia{halsburys2009,
Publisher = {LexisNexis},
Booktitle = {Halsbury's Laws of Australia},
Volume    = {5},
Date      = {2009-05-25},
Title     = {235 Insurance},
Chapter   = {2 General Principles}}
```

```
@legal-encyclopedia{lawbook2000,
Publisher = {Lawbook},
Booktitle = {The Laws of Australia},
Date      = {2000-08-31},
Title     = {24 International Trade},
Chapter   = {2 Foreign Investment}}
```

#### Looseleaf services

```
@looseleaf{civprocvicvol1,
Publisher = {LexisNexis Butterworths},
Title     = {Civil Procedure: Victoria},
Volume    = {1},
Version   = {Service 231}}
```

```
@looseleaf{jacobsvol1r5,
Author    = {Marcus S Jacobs},
Publisher = {Thomson Reuters},
Title     = {International Commercial Arbitration in Australia: Law and Practice},
Volume    = {1},
Version   = {Release 5}}
```

```
@looseleaf{cchintl68108,
Publisher = {CCH International},
Title     = {Japan Business Law Guide},
Volume    = {1},
Version   = {68-1-08}}
```

```
@looseleaf{carter2009,
Author    = {J W Carter},
Publisher = {LexisNexis},
Title     = {Carter on Contract},
Date      = {2009-01-10}}
```

#### Newspaper articles

Newspaper articles provide the ```URL``` field, which should only be used for electronic newspaper articles. ```Journal``` is used for the title of the newspaper, and ```title``` for the title of the article.

Print article with author:

```
@newspaper{howard2006,
Author   = {Stephen Howard and Billy Briggs},
Title    = {Law Lords Back School's Ban on Islamic Dress},
Journal  = {The Herald},
Location = {Glasgow},
Date     = {2006-03-23}}
```

Print article with section:

```
@newspaper{hunter2009,
Author   = {Abigail Hunter},
Title    = {He Stole My Son, Now I'm Alone in Hell},
Chapter  = {Times2},
Journal  = {The Times},
Location = {London},
Date     = {2009-12-03}}
```

Print article without author:

```
@newspaper{afr2006,
Title    = {Fury at WA Council Plan},
Journal  = {The Australian Financial Review},
Location = {Sydney},
Date     = {2006-05-01}}
```

Editorial:

```
@newspaper{theage2004,
Type     = {Editorial},
Title    = {Medicare by Name, No Longer by Nature},
Chapter  = {News},
Journal  = {The Age},
Location = {Melbourne},
Date     = {2004-03-12}}
```

Letter to the editor:

```
@newspaper{healy2002,
Author   = {Rose Healy},
Type     = {Letter to the Editor},
Journal  = {The Herald Sun},
Location = {Melbourne},
Date     = {2002-06-10}}
```

Electronic newspaper article:

```
@newspaper{tomazin2009,
Author   = {Farrah Tomazin},
Title    = {Kinder Wages Breakthrough},
Journal  = {The Age},
Location = {online},
Date     = {2009-05-19},
URL      = {http://www.theage.com.au/national/education/kinder-wages-breakthrough-20090519-bcwh.html}}
```

#### Television and radio transcripts

```
@transcript{abcnrlawrep2009,
Publisher = {ABC Radio National},
Title     = {Inventions: Who Owns Them?},
Maintitle = {The Law Report},
Date      = {2009-09-08},
URL       = {http://www.abc.net.au/rn/lawreport/stories/2009/2678819.htm#transcript}}
```

#### Film and audiovisual recordings

```
@film{jacobson1996,
Title     = {Calling the Ghosts: A Story About Rape, War and Women},
Author    = {Mandy Jacobson and Karmen Jelincic},
Publisher = {Bowery Productions},
Year      = {1996}}
```

```
@film{mulligan1962,
Title     = {To Kill a Mockingbird},
Author    = {Robert Mulligan},
Publisher = {Brentwood Productions},
Year      = {1962}}
```

#### Press and media releases

```
@pressrelease{dod2009,
Author = {Department of Defence (Cth)},
Title  = {Highest East Timorese Honour for Army Officers},
Type   = {Media Release},
Number = {MSPA 172/09},
Date   = {2009-05-22},
```

```
@pressrelease{asx2009,
Author = {Australian Stock Exchange},
Title  = {ASX Group Monthly Activity Report --- April 2009},
Type   = {Media Release},
Date   = {2009-05-05},
URL    = {http://www.asx.com.au/about/pdf/ma050509_monthly_activity_report_april09.pdf}}
```

#### Working papers

```
@workingpaper{tapking2004,
Author      = {Jens Tapking and Jing Yang},
Title       = {Horizontal and Vertical Integration in Securities Trading and Settlement},
Type        = {Working Paper},
Number      = {245},
Institution = {Bank of England},
Date        = {2004}}
```

```
@workingpaper{memmott2008
Author      = {Paul Memmott and Peter Blackwood},
Title       = {Holding Title and Managing Land in Cape York --- Two Case Studies},
Type        = {Research Discussion Paper},
Number      = {21},
Institution = {Bank of England},
Date        = {2004}}
```

```
@workingpaper{moser1998,
Author      = {Caroline O N Moser and Annika Tornqvist and Bernice van Bronkhorst},
Title       = {Mainstreaming Gender and Development in the World Bank: Progress and Recommendations},
Type        = {Report},
Institution = {World Bank},
Date        = {1998}}
```

```
@workingpaper{howe2006,
Author      = {John Howe and Ingrid Landau},
Title       = {``Light Touch'' Labour Regulation by State Governments in Australia: A Preliminary Assessment},
Type        = {Working Paper},
Number      = {40},
Institution = {Centre for Employment and Labour Relations Law, The University of Melbourne},
Date        = {2006-12},
URL         = {http://papers.ssrn.com/sol3/papers.cfm?abstract_id=961528}}
```

#### Theses

```
@thesis{muller2005,
Author      = {Denis Joseph Andrew Muller},
Title       = {Media Accountability in a Liberal Democracy --- An Examination of the Harlot's Prerogative},
Type        = {PhD Thesis},
Institution = {The University of Melbourne},
Year        = {2005}}
```

```
@thesis{champsaur2005,
Author      = {Am\'{e}lie Champsaur},
Title       = {The Regulation of Credit Rating Agencies in the US and the EU: Recent Initiatives and Proposals},
Type        = {LLM Thesis},
Institution = {Harvard University},
Year        = {2005},
URL         = {http://www.law.harvard.edu/ programs/about/pifs/education/sp19.pdf}}
```

#### Conference papers

Also accepts the ```URL``` field.

```
@conference{orford2008,
Author      = {Anne Orford},
Title       = {Roman Law and the Godly Imperium in England's New Worlds},
Venue       = {the Workshop on the Theo-Political Renaissance},
Location    = {Department of English, Cornell University},
Date        = {2008-04-25}}
```

#### Speeches

```
@speech{french2009,
Author      = {Chief Justice Robert French},
Title       = {Native Title --- A Constitutional Shift?},
Venue       = {JD Lecture Series},
Location    = {The University of Melbourne},
Date        = {2009-03-24},
URL         = {http://www.hcourt.gov.au/publications_05.html}}
```

#### Interviews

Interviews conducted by the author, or by someone else, are both cited using ```@interview```. Note that the field ```Author``` refers to the interviewer, and ```Commentator``` refers to the intervieee. Where interviews are conducted by the author of the work in which they are being cited, the ```Author``` field should be omitted in accordance with the AGLC. Either the location or the type of interview may be included (but do not use both).

```
@interview{dunn2005,
Commentator = {Philip Dunn},
Location    = {Melbourne},
Date        = {2005-10-19}}
```

```
@interview{roxon2005,
Commentator = {Nicola Roxon, Shadow Attorney General},
Type        = {Doorstop Interview},
Date        = {2005-11-02}}
```

```
@interview{oakes2005,
Author      = {Laurie Oakes},
Commentator = {John Howard, Prime Minister of Australia},
Type        = {Television Interview},
Date        = {2005-10-30}}
```

#### Written correspondence

The ```Author``` field refers to the writer of the correspondence, and the field ```Holder``` refers to the recipient. The ```URL``` field is supported.

```
@correspondence{barrington2001,
Type   = {Email},
Author = {Jonathon Barrington},
Holder = {Deborah Horowitz},
Date   = {2001-05-17}}
```

```
@correspondence{deloitte2008,
Type   = {Letter},
Author = {Deloitte Touche Tohmatsu},
Holder = {Opes Primes Clients},
Date   = {2008-04-01},
URL    = {http://www.deloitte.com.au/media/docs/OpesPrime_groupcircular.pdf}}
```

#### Internet materials

AGLCLaTeX provides for two types of Internet materials not already covered above:

- ```@online``` - for webpages and materials on the Internet generally, and
- ```@blog``` - for blogs and forum posts.

Note that for webpages, etc, if the name of the author is the same as the website name, the website name is to be omitted in accordance with the AGLC. The date may also be omitted if unavailable. The field ```Organization``` takes the website name.

```
@online{boe2010,
Author       = {Board of Examiners},
Title        = {Admission Requirements},
Date         = {2010-02-18},
Organization = {Council of Legal Education},
URL          = {http://www.lawadmissions.vic.gov.au}}
```

```
@online{dcsgwa,
Author       = {Department of Corrective Services, Government of Western Australia},
Title        = {Victim-Offender Mediation},
URL          = {http://www.correctiveservices.wa.gov.au/victim-services/victim-offender-mediation/}}
```

```
@online{who1997,
Author = {World Health Organisation},
Title  = {Violence Against Women: A Priority Health Issue},
Date   = {1997},
URL    = {http://www.who.int/gender/violence/prioreng/en/}}
```

For blogs and forums, the ```Author``` field refers to the author of the individual post, the ```Editor``` field to the author of the blog or forum. If there is no apparent regular author, ```Editor``` can be omitted.

```
@blog{gans2008,
Author       = {Jeremy Gans},
Title        = {The \textit{Charter} vs Eviction},
Editor       = {Jeremy Gans},
Organization = {Charterblog: Analysis of Victoria's Charter of Human Rights},
Date         = {2008-07-12},
URL          = {http://charterblog.wordpress.com/2008/07/12/the-charter-vs-eviction}}
```

#### Subsequent references

In accordance with the AGLC:

- 'Ibid' is used for all other sources, and
- 'above n' is used for all other sources, except:
  - parliamentary debates/Hansard,
  - evidence to parliamentary committees,
  - Australian constitutional convention debates,
  - interviews, and
  - written correspondence.

## International materials

### Treaties

AGLCLaTeX provides for three kinds of treaties:

- ```@treaty-volume``` - for treaties published in a treaty series organised by volume (eg, UNTS),
- ```@treaty-year``` - for treaties published in a treaty series organised by year (eg, ATS), and
- ```@treaty-number``` - for treaties published in a treaty series organised by sequential order (eg, CETS).

Each also accepts the same four types:

- ```Type = {open-if}``` - for open multilateral treaties which are in force,
- ```Type = {open-nif}``` - for open multilateral treaties which are not yet in force,
- ```Type = {closed-if}``` - for closed treaties which are in force, and
- ```Type = {closed-nif}``` - for closed treaties which are not yet in force.

AGLCLaTeX implements the complicated rules that the AGLC sets out for each in chapter 7. It's unnecessary to repeat those rules, but to explain the operation:

- ```Type = {open-if}``` and ```Type = {open-nif}``` will print 'opened for signature DD MM YYYY' where appropriate.
- ```Type = {closed-if}``` and ```Type = {closed-nif}``` will print 'signed DD MM YYYY' where appropriate.
- ```Type = {open-if}``` and ```Type = {closed-if}``` will print '(entered into force DD MM YYYY)' where appropriate.
- ```Type = {open-nif}``` and ```Type = {closed-nif}``` will print '(not yet in force)' where appropriate.

The ```Origdate``` field is used for the _date of conclusion_ of the treaty (ie, the date it was signed). The ```Date``` field is used for the _entry into force date_.

The entry into force date will _always_ be later than the date of conclusion, unless the treaty was signed and entered into force at the same time. If a treaty is not yet in force, the ```Date``` field can be safely omitted.

In the case of treaties that were concluded and entered into force on the same date, repeat the date in both the ```Origdate``` and ```Date``` fields. This will then print '(signed and entered into force DD MM YYYY)' where appropriate.

The ```Author``` field contains the parties to the treaty, but should be omitted if there are more than three, and should be separated by en-dashes (in LaTeX, --) in accordance with the AGLC. Parties should also be omitted if named in the title of the treaty.

For treaties published in a series arranged by year, the year should be put in the ```Volume``` field.

The ```Pages``` field should be used for the starting page _only_ of the treaty where relevant.

Illustrated examples are given below.

- _Treaty on the Non-Proliferation of Nuclear Weapons_, opened for signature 1 July 1968, 729 UNTS 161 (entered into force 5 March 1970).

```
@treaty-volume{npt1968,
Title    = {Treaty on the Non-Proliferation of Nuclear Weapons},
Type     = {open-if},
Origdate = {1968-07-01},
Volume   = {729},
Series   = {UNTS},
Pages    = {161},
Date     = {1970-03-05}}
```

- _Agreement regarding the Transfer of the Administration of Justice in the Territories of Northern Slesvig_, Denmark–Germany, signed 12 July 1921, 8 LNTS 397 (entered into force 17 January 1922).

```
@treaty-volume{slesvig1921,
Title    = {Agreement regarding the Transfer of the Administration of Justice in the Territories of Northern Slesvig},
Author   = {Denmark--Germany},
Type     = {closed-if},
Origdate = {1921-07-12},
Volume   = {8},
Series   = {LNTS},
Pages    = {397},
Date     = {1922-01-17}}
```

- _Statute of the International Renewable Energy Agency_, opened for signature 26 January 2009, [2009] ATNIF 23 (not yet in force).

```
@treaty-year{sirea2009,
Title    = {Statute of the International Renewable Energy Agency},
Type     = {open-nif},
Origdate = {2009-01-26},
Volume   = {2009},
Series   = {ATNIF},
Number   = {23}}
```

- _Agreement Relating to Co-operation on Antitrust Matters_, Australia–United States of America, 1369 UNTS 43 (signed and entered into force 29 June 1982).

```
@treaty-volume{antitrust1982,
Title    = {Agreement Relating to Co-operation on Antitrust Matters},
Author   = {Australia--United States of America},
Type     = {closed-if},
Origdate = {1982-06-29},
Volume   = {1369},
Series   = {UNTS},
Pages    = {43},
Date     = {1982-06-29}}
```

- _Convention on Cybercrime_, opened for signature 23 November 2001, ETS No 185 (entered into force 1 July 2004).

```
@treaty-number{coc2004,
Title    = {Convention on Cybercrime},
Type     = {open-if},
Origdate = {2001-11-23},
Series   = {ETS},
Number   = {185},
Date     = {2004-07-01}}
```

#### Subsequent references

In accordance with the AGLC:
- 'Ibid' is used for treaties, and
- 'above n' is not used.

### United Nations materials

#### Constitutive document

The _Charter of the United Nations_ should be cited using the ```@act-gen``` entry type:

```
@act-gen{uncharter,
Title = {Charter of the United Nations}}
```

```\cite[art 51]{uncharter}``` will produce '_Charter of the United Nations_ art 51.'

**AGLCLaTeX does not currently support other United Nations materials**

### International Court of Justice and Permanent Court of International Justice

#### Constitutive and basic documents

The _Statute of the International Court of Justice_ and _Statute of the Permanent Court of International Justice_ should be cited using the ```@act-gen``` entry type:

```
@act-gen{icjstatute,
Title = {Statute of the International Court of Justice}}
```

```
@act-gen{pcijstatute,
Title = {Statute of the Permanent Court of International Justice}}
```

Rules of court for both the ICJ and PCIJ are cited using the ```@rulesofcourt``` entry type:

```
@rulesofcourt{icj1978,
Institution = {International Court of Justice},
Date        = {1978-04-14}}
```

```
@rulesofcourt{pcij1922,
Institution = {Permanent Court of International Justice},
Date        = {1922-03-24}}
```

#### Reported decisions

AGLCLaTeX provides for both International Court of Justice and Permanent Court of International Justice decisions:

- ```@case-icj-reported``` - for International Court of Justice decisions, and
- ```@case-pcij-reported``` - for Permanent Court of International Justice decisions.

The first three fields of each are the same:

- ```Title``` takes the case name and if applicable the parties' names, which should go in parentheses,
- ```Type``` takes the phase or type of the decision (eg, 'Judgment', 'Jurisdiction' or 'Advisory Opinion'), and
- ```Year``` takes the year of the volume of the report series.

ICJ cases have one additional field:

- ```Pages``` takes the starting page only of the case.

PCIJ cases have two additional fields:

- ```Series``` takes the letter of the series (either 'A', 'B' or 'A/B'), and
- ```Number``` takes the number of the decision.

```
@case-icj-reported{easttimor1995,
Title = {East Timor (Portugal v Australia)},
Type  = {Judgment},
Year  = {1995},
Pages = {90}}
```

```
@case-icj-reported{westernsahara1975,
Title = {Western Sahara},
Type  = {Advisory Opinion},
Year  = {1975},
Pages = {12}}
```

```
@case-pcij-reported{mavrommatis1924,
Title  = {Mavrommatis Palestine Concessions (Greece v United Kingdom)},
Type   = {Jurisdiction},
Year   = {1924},
Series = {A},
Number = {2}}
```

#### Reported pleadings and other documents originating in ICJ and PCIJ proceedings

AGLCLaTeX provides for reported pleadings and similar documents in both ICJ and PCIJ proceedings:

- ```@icj-pleading-reported``` - for documents from the International Court of Justice, and
- ```@pcij-pleading-reported``` - for documents from the Permanent Court of International Justice.

Both use the ```Title``` field for the title of the document, and ```Maintitle``` for the title of the proceedings. ```Maintitle``` should be in the same format as the title for cases: ```Maintitle = {Title (Parties)}``` or ```Maintitle = {Title (Advisory Opinion)}```. The ```Year``` field takes the year of the volume (preferred) or the year of the decision (if the year of the volume is unavailable). The ```Pages``` field takes the starting page only of the document.

```@icj-pleading-reported``` can also take the volume number cited, which is in Roman numerals, in the ```Volume``` field.

```@pcij-pleading-reported``` can take the number and part (if applicable) of the document in the ```Number``` and ```Part``` fields.

```
@icj-pleading-reported{denmark1962,
Title     = {Written Statement of the Government of the Kingdom of Denmark},
Maintitle = {Certain Expenses of the United Nations (Advisory Opinion)},
Year      = {1962},
Pages     = {137}}
```

```
@icj-pleading-reported{glennon1986,
Title     = {Questions Put to Professor Glennon by Judge Schwebel},
Maintitle = {Military and Paramilitary Activities in and against Nicaragua (Nicaragua v United States of America)},
Year      = {1986},
Volume    = {V},
Pages     = {78}}
```

```
@pcij-pleading-reported{hbm1925,
Title     = {Memorial Filed by the Government of His Britannic Majesty},
Maintitle = {Treaty of Lausanne, Article 3, Paragraph 2 (Advisory Opinion)},
Year      = {1925},
Number    = {10},
Pages     = {198}}
```

```
@pcij-pleading-reported{budding1928,
Title     = {Speech by Dr Budding},
Maintitle = {Rights of Minorities in Upper Silesia (Germany v Poland)},
Year      = {1928},
Number    = {14},
Part      = {II},
Pages     = {20}}
```

#### Unreported decisions

```@case-icj-unreported``` is used for unreported decisions of the International Court of Justice. These are cited essentially the same as reported decisions; the differences are handled by AGLCLaTeX automatically. However, there are some slight differences:

```
@case-icj-unreported{icj2008-06-04,
Title  = {Certain Questions of Mutual Assistance in Criminal Matters (Djibouti v France)},
Type   = {Judgment},
Number = {136},
Date   = {2008-06-04}}
```

#### Unreported pleadings and other documents originating in ICJ proceedings

```@icj-pleading-unreported``` is used for unreported pleadings, etc, originating in ICJ proceedings.

It bears similarities to reported pleadings and unreported decisions: the ```Title``` is used for the title of the document and ```Maintitle``` is used for the title of the proceedings. Otherwise they are cited the same as unreported decisions:

```
@icj-pleading-unreported{icj2008-03-31,
Title     = {Application Instituting Proceedings},
Maintitle = {Aerial Herbicide Spraying (Ecuador v Colombia)},
Number    = {138},
Date      = {2008-03-31}}
```

### International arbitral and tribunal decisions

Unlike the AGLC, AGLCLaTeX does not differentiate between state-state and individual-state decisions by international arbitrations and tribunals. They are essentially cited the same way as Australian domestic cases. There are three entry types supported:

- ```@case-intl-volume``` - for reported decisions published in reports organised by volume,
- ```@case-intl-year``` - for reported decisions published in reports organised by year, and
- ```@case-intl-unreported``` - for unreported decisions.

Reported decisions support the ```Venue``` field which can be used for the name of the court or tribunal if it's not apparent from the report series (or simply for clarification).

Further, reported and unreported decisions of international criminal tribunals and courts should be cited using these same entry types: the AGLC prefers them to be cited in the same manner as unreported cases unless they are obscure and a reported version would aid retrieval. The ```Venue``` field should include both the court and the chamber if applicable (eg, ```Venue = {Special Court for Sierra Leone, Trial Chamber I}```.

There are no examples provided for ```@case-intl-year```, but ```@case-intl-volume``` and ```@case-intl-year``` take essentially the same fields; ```Volume``` is optional for reports organised by year.

Also note that like ICJ and PCIJ cases, these all use the ```Type``` field for the phase (or stage) of the proceedings, per the examples below.

- Reported state v state decision.

```
@case-intl-volume{bluefintuna2000,
Title  = {Southern Bluefin Tuna (Australia v Japan)},
Type   = {Jurisdiction and Admissibility},
Year   = {2000},
Volume = {39},
Series = {ILM},
Pages  = {1359}}
```

- Reported individual/investor v state decision.

```
@case-intl-volume{olguin2004,
Title  = {Olgu\'{i}n v Paraguay},
Type   = {Jurisdiction},
Year   = {2004},
Volume = {6},
Series = {ICSID Rep},
Pages  = {154}}
```

- Unreported state v state decision.

```
@case-intl-unreported{hoshinmaru2007,
Title  = {Hoshinmaru (Japan v Russia)},
Type   = {Judgment},
Venue  = {International Tribunal for the Law of the Sea},
Number = {14},
Date   = {2007-08-06}}
```

- Unreported individual/investor v state decision.

```
@case-intl-unreported{enron2004,
Title  = {Enron Corporation v Argentina},
Type   = {Jurisdiction},
Venue  = {ICSID Arbitral Tribunal},
Number = {ARB/01/3},
Date   = {2004-01-14}}
```

- General international criminal tribunal or court decision.

```
@case-intl-unreported{sesay2009,
Title  = {Prosecutor v Sesay},
Type   = {Sentencing Judgment},
Venue  = {Special Court for Sierra Leone, Trial Chamber I},
Number = {SCSL-04-15-T},
Date   = {2009-04-08}}
```

- Reported international criminal tribunal or court decision.

```
@case-intl-unreported{blaskic1997,
Title  = {Prosecutor v Bla\v{s}ki\v{c}},
Type   = {Objection to the Issue of Subpoenae Duces Tecum},
Year   = {1997},
Volume = {110},
Series = {ILR},
Pages  = {688},
Venue  = {International Criminal Tribunal for the Former Yugoslavia, Appeals Chamber}}
```

### International criminal tribunals and courts

#### Basic documents

In accordance with the AGLC, constitutive documents should be cited in accordance with the appropriate rules (eg, treaty or UN resolution).

#### Cases

Refer to [international arbitral and tribunal decisions](#international-arbitral-and-tribunal-decisions) above.

**AGLCLaTeX does not currently support other international materials**

## Foreign domestic materials

### Canada

#### Cases

Canadian cases, administrative decisions and arbitrations should be cited the same as the respective Australian materials (see examples above), using:

- ```@case-gen-volume``` - for reported cases in a report series arranged by volume,
- ```@case-gen-year``` - for reported cases in a report series arranged by year (which may include volumes within that year),
- ```@case-gen-mnc``` - for unreported cases with a medium neutral citation,
- ```@case-gen-unreported``` - for unreported cases without a medium neutral citation, and
- ```@arbitration``` - for domestic arbitrations.

**AGLCLaTeX does not currently support other Canadian materials**

### China

**AGLCLaTeX does not currently support Chinese materials**

### France

**AGLCLaTeX does not currently support French materials**

### Germany

**AGLCLaTeX does not currently support German materials**

### Hong Kong

#### Cases

Hong Kong cases, administrative decisions and arbitrations should be cited the same as the respective Australian materials (see above).

**AGLCLaTeX does not currently support other Hong Kong materials**

### Malaysia

#### Cases

Malaysian cases, administrative decisions and arbitrations should be cited the same as the respective Australian materials (see above), except ```@case-gen-mnc``` should _not_ be used for any decisions (use ```case-gen-unreported``` for unreported decisions instead).

**AGLCLaTeX does not currently support other Malaysian materials**

### New Zealand

#### Cases

New Zealand cases, administrative decisions and arbitrations should be cited the same as the respective Australian materials (see above), except for Maori Land Court, Maori Appellate Court and Waitangi Tribunal decisions (currently unsupported).

**AGLCLaTeX does not currently support other New Zealand materials**

### Singapore

#### Cases

New Zealand cases, administrative decisions and arbitrations should be cited the same as the respective Australian materials (see above).

**AGLCLaTeX does not currently support other Singaporean materials**

### South Africa

#### Cases

South African cases, administrative decisions and arbitrations should be cited the same as the respective Australian materials (see above).

**AGLCLaTeX does not currently support other Singaporean materials**

### United Kingdom

#### Cases

United Kingdom cases, administrative decisions and arbitrations should be cited the same as the respective Australian materials (see above), except for Scottish cases reported in a report series organised by year (currently unsupported).

In accordance with the AGLC: when citing a nominate report (published under the name of the reporter between 1537 and 1865) this should be accompanied with a citation of the _English Reports_ ('ER') or _Revised Reports_ ('RR'). This can be done using the ```\cites``` command and chaining two citations back-to-back, albeit with some complexity. This is currently untested, but should work. They can also therefore take separate pinpoints (but postnotes to follow the whole should go in the postnote of the second entrykey.

Example: ```\cites{russel1661a}{russel1661b}``` should print: _Russel v Lee_ (1661) 1 Lev 86; 83 ER 310 in accordance with the following entries.

```
@case-gen-volume{russel1661a,
Title  = {Russel v Lee},
Year   = {1661},
Volume = {1},
Series = {Lev},
Pages  = {86}}

@case-gen-volume{russel1661b,
Volume = {83},
Series = {ER},
Pages  = {310}}
```

Likewise, ```\cites[345]{janvrin1861a}[336 (Lord Kingsdown)]{janvrin1861b}``` should print: _Janvrin v De La Mare_ (1861) 14 Moo 334, 345; 15 ER 332, 336 (Lord Kingsdown). Entries for this example have been omitted.

**AGLCLaTeX does not currently support other United Kingdom materials**

### United States of America

#### Cases

AGLCLaTeX provides for both reported and unreported US cases:

- ```@case-us-reported```, and
- ```@case-us-unreported```.

There are relatively complex rules with regard to jurisdiction and court name, which can be found in the AGLC 24.1.5. The basic rules are:

- Do not include the name of the court if citing a decision of the US Supreme Court.
- Courts of Appeals should be referred to by number ('1st Cir', '2nd Cir'), except the DC Circuit ('DC Cir') and Federal Circuit ('Fed Cir').
	- When citing numbered circuits, use the ```\nth``` command to enclose the number to make it an ordinal: ```Venue = {\nth{1} Cir}```.
- Federal District Court decisions should have an abbreviated form of the district (but not division) and the state abbreviation, such as:
	- 'D Del' --- (District of Delaware).
	- 'CD Cal' --- (Central District of California).
	- 'ED Mo' --- (Middle District of New Hampshire).
- State Courts should have an abbreviated form of the jurisdiction (ie, state) followed by the conventional abbreviated name of the court, unless the jurisdiction is apparent from the title of the report series (omit the jurisdiction) or it is the highest court in the state (omit the court name):
	- _Brogdon v State_, 467 SE 2d 598 (**Ga Ct App**, 1996).
	- _Poire v CL Peck/Jones Brothers Construction Corporation Inc_, 46 Cal Rptr 2d 631 (**Ct App**, 1995).
	- _Burr v Maclay Rancho Water Co_, 98 P 260 (**Cal**, 1908).

```
@case-us-reported{bush2004,
Title  = {Bush v Schiavo},
Volume = {885},
Series = {So 2d},
Pages  = {336},
Venue  = {Fla},
Year   = {2004}}
```

Note that for citations of US Supreme Court decisions prior to 1875 (prior to volume 90 US), a parallel citation should be included of the early American report series in parentheses in the ```Series``` field. 

```
@case-us-reported{winchester1804,
Title  = {Winchester v Hackley},
Volume = {6},
Series = {US (2 Cranch)},
Pages  = {342},
Year   = {1804}}
```

Unreported cases must specify the type of docket or reference number (eg, 'Civ No' or 'No') in accordance with the decision:

```
@case-us-unreported{redhat2004,
Title  = {Red Hat Inc v The SCO Group Inc},
Venue  = {D Del},
Number = {Civ No 03-772-SLR},
Date   = {2004-04-06}}
```