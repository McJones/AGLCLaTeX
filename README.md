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
Title  = {R v Tang},
Year   = {2008},
Volume = {237},
Series = {CLR},
Pages  = {1}}

@case-au-year{bakker1980,
Title  = {Bakker v Stewart},
Year   = {1980},
Series = {VR},
Pages  = {17}}
  
@case-au-year{rowe1976,
Title  = {Rowe v McCartney},
Year   = {1976},
Volume = {2},
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
Date   = {2009-09-09},
Venue  = {TASSC},
Number = {80}}
```
#### Unreported decisions without a Medium Neutral Citation

```
@case-au-unreported{barton1989,
Title  = {Barton v Chibber},
Venue  = {Supreme Court of Victoria},
Author = {Hampel J},
Date   = {1989-06-29}}
```

**AGLCLaTeX does not currently support case history**

#### Quasi-judicial decisions (administrative decisions and arbitrations)

Administrative decisions should cited as cases (ie, using ```@case-au-volume```, ```@case-au-year```, ```@case-au-mnc``` or ```@case-au-unreported```).

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

AGLCLaTeX uses the ```@act-au``` entry type for statutes, constitutions and delegated legislation:

```
@act-au{crimesact1958vic,
Title    = {Crimes Act},
Year     = {1958},
Location = {Vic}}
```

```
@act-au{ausconstitution,
Title = {Australian Constitution}}
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
