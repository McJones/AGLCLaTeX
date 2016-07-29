# AGLCLaTeX
A Biblatex style implementing the Australian Guide to Legal Citation

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

**ALGCLaTeX does not currently support sources referring to other sources.***

In compliance with the AGLC:

- Repeated citations print 'Ibid' and a pinpoint or other postnote, unless:
- the postnote is identical to the previous citation, or
- there are multiple sources in the previous footnote.

If the postnote is identical, only 'Ibid' is printed. If there are multiple sources in the previous footnote, the surname of the author or editor is printed, followed by ', above n' and the footnote number of the _first_ instance of that source, unless the AGLC requires to be printed in full. If the pinpoint is different, a pinpoint is printed. This requires the document to be compiled _twice_ after running Bibtex.

**AGLCLaTeX does not currently support short titles**

Dates for sources should be in ```YYYY-MM--DD``` format: ```Date = {2000-01-01}```. Individual authors and editors should be separated with 'and' (do not use commas, even for more than two authors): ```Author = {John Smith and Jane Doe}```. Corporate authors should be enclosed in double curly braces to prevent unintended splitting: ```Author: {{Department of Foreign Affairs and Trade}}```.

**AGLCLaTeX does not currently support the headings, titles or bibliography format of the AGLC**

## Domestic sources (legal)

### Cases

AGLCLaTex provides for several different types of cases, as covered by the AGLC:

- ```@case-au-volume``` - Reported cases in a report series arranged by volume.
- ```@case-au-year``` -Reported cases in a report series arranged by year (which may include volumes within that year).
- ```@case-au-mnc``` - Unreported cases with a medium neutral citation.
- ```@case-au-unreported``` - Unreported cases without a medium neutral citation.
- ```@arbitration``` - Domestic arbitrations.
- Administrative decisions that are reported or unreported should be cited as cases.

Refer to the AGLC for formatting rules. Note that:
- Administrative decisions typically use 'and' instead of 'v' to separate party names.
- Judges' names should conform with the AGLC rules.
- If necessary, additional information can be included in the postnote.

#### Reported decisions

```
@case-au-volume{tang2008,
Title  = {R v Tang}, % the case title
Year   = {2008}, % the year of the decision (not the year of publication)
Volume = {237}, % the volume of the report
Series = {CLR}, % the appreviation of the report series (eg, 'CLR' is 'Commonwealth Law Reports')
Pages  = {1}} % the page on which the decision starts (not a range)

@case-au-year{bakker1980,
Title  = {Bakker v Stewart},
Year   = {1980}, % the year of the volume in which the decision is reported
Series = {VR},
Pages  = {17}}
  
@case-au-year{rowe1976,
Title  = {Rowe v McCartney},
Year   = {1976},
Volume = {2}, % the individual volume in which the decision is reported (eg, this is volume 2 of the 1976 NSWLR)
Series = {NSWLR},
Pages  = {72}}
```

The ```Pages``` field can be replaced with a different identifier (such as a paragraph number) if that's how the reports are set out.

Both ```@case-au-volume``` and ```@case-au-year``` allow for the ```venue``` field, which may specify the court if relevant or necessary:

```
@case-au-year{aldrick2000,
Title  = {Aldrick v EM Investments (Qld) Pty Ltd},
Year   = {2000},
Volume = {2},
Series = {Qd R},
Pages  = {346},
Venue  = {Court of Appeal}}
```
  
#### Unreported decisions with a Medium Neutral Citation

```
@case-au-mnc{quarmby2009,
Title  = {Quarmby v Keating},
Date   = {2009-09-09}, % the date of the decision in YYYY-MM-DD
Venue  = {TASSC}, % the Unique Court Identifier
Number = {80}} % the judgment number
```
#### Unreported decisions without a Medium Neutral Citation

```
@case-au-unreported{barton1989,
Title  = {Barton v Chibber},
Venue  = {Supreme Court of Victoria}, % the court by which the decision was made
Author = {Hampel J}, % the judge or judges who made the decision
Date   = {1989-06-29}}
```

**AGLCLaTeX does not currently support case history**

#### Quasi-judicial decisions (administrative decisions and arbitrations)

Administrative decisions should cited as cases (ie, using ```@case-au-volume```, ```@case-au-year```, ```@case-au-mnc``` or ```@case-au-unreported```).

Arbitrations use the ```@arbitration``` entry type. Arbitrations may or may not have a title; if an arbitration does not the title can be safely omitted.

```
@arbitration{beckman1988,
Title  = {Beckman Instruments Inc v Overseas Private Investment Corporation}, % the title of the arbitration if given
Note   = {Award and Opinion}, % the stage of the arbitration or description of the award
Venue  = {American Arbitration Association Commercial Arbitration Tribunal}, % the forum or names of the arbitrators
Type   = {Case}, % the type of dispute (eg, case, dispute or award)
Number = {16 199 00209 87G}, % the number of the dispute (if applicable)
Date   = {1988-02-20}} % the date of the decision
```

```
@arbitration{sandline1998,
Title  = {Sandline International v Papua New Guinea},
Note   = {Award},
Venue  = {Sir Edward Somers, Sir Michael Kerr and Sir Daryl Dawson},
Date   = {1998-10-09}} % the date of the arbitration
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
Title  = {Celano v Swan}, % the title of the case
Venue  = {County Court of Victoria}, % the court in which the matter was heard
Number = {09/0867}, % the number of the matter (if applicable)
Author = {Judge Lacava}, % the judge or judges hearing the matter
Date   = {2009-08-27}} % the full date
```

```
@case-transcript-hca{ruhani2005,
Title  = {Ruhani v Director of Police},
Date   = {2005-04-19},
Number = {205}} % the number that follows 'HCA Trans' in the citation
```

#### Submissions in Cases

```
@case-submission{agcth2005,
Author    = {Attorney-General (Cth)}, % the party or person making the submission
Title     = {Outline of Submissions of the Attorney-General of the Commonwealth as Amicus Curiae}, % the submission title
Maintitle = {Human Society International Inc v Kyodo Senpaku Kaisha Ltd}, % the case title
Number    = {NSD 1519/2004}, % the proceeding number
Date      = {2005-01-25}} % the full date
```

#### Subsequent References

In accordance with the AGLC:
- 'Ibid' is used for all cases and related materials, and
- 'above n' is not used for cases and related materials.

### Legislative materials

#### Statutes (Acts of Parliament), Australian Constitutions, and Delegated Legislation

AGLCLaTeX uses the ```@act-au``` entry type for statutes, constitutions and delegated legislation:

```
@act-au{crimesact1958vic,
Title    = {Crimes Act},
Year     = {1958}, % the year, even if not included with the legislation
Location = {Vic}} % the abbreviated jurisdiction
```

```
@act-au{ausconstitution,
Title = {Australian Constitution}} % the AGLC states that more details are unnecessary for the Australian Constitution
```

```
@act-au{policeregs2003vic,
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
Author    = {Minister for Lands (WA)}, % the author of the notice (optional)
Title     = {\textit{Land Acquisition and Public Works Act 1902 --- Native Title Act 1993} (Commonwealth) --- Notice of Intention to Take Land for a Public Work}, % the title of the notice (optional)
Location  = {Western Australia}, % the jurisdiction of the gazette (eg, Commonwealth, New South Wales, Western Australia)
Maintitle = {Western Australian Government Gazette} % the title of the gazette
Number    = {27}, % the gazette number
Date      = {1997-02-18}, % the full date
Pages     = {1142}} % the starting page only
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

AGLCLaTeX uses the ```@bill-au``` entry type for bills, which are otherwise cited like regular legislation:

```
@bill-au{corpamendbill2005cth,
Title    = {Corporations Amendment Bill No 1},
Year     = {2005},
Location = {Cth}}
```

#### Explanatory Memoranda, Statements and Notes

AGLCLaTeX uses the ```@bill-au-exp``` entry type for explanatory memorada, statements and note, which are otherwise cited like regular legislation, but with the type of document specified:

```
@bill-au-exp{exphrcharter2006vic,
Type     = {Explanatory Memorandum},
Title    = {Charter of Human Rights and Responsibilities Bill},
Year     = {2006},
Location = {Vic}}
```

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

Unsigned article published in a journal arranged by volume:

```
@article-volume{mulr2002,
Type    = {Symposium},
Title   = {Contemporary Human Rights in Australia},
Year    = {2002},
Volume  = {26},
Journal = {Melbourne University Law Review},
Pages   = {251}}
```
