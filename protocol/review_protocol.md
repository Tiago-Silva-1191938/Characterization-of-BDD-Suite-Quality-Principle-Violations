# Literature review protocol

Version: draft (not yet frozen)

This procedure is written into a protocol before the search starts.
Any later change is recorded in the change log, with its date and reason.

The state of the art is established in two parts: a systematic mapping of the literature (Part 1) and a survey of the tools found in it (Part 2).

## 1. Type of review

Part 1 is a systematic mapping study (scoping review) in the sense of Ralph and Baltes (2022).
Studies are selected through a systematic, replicable process and mapped into categories.
The aim is to describe the status of research and to locate the gap that this work addresses.

It is not a stand-alone secondary study; it supports a primary, empirical study.
A related-work discussion based on purposively selected papers would not be enough.
The claim that no prior study measures the prevalence or persistence of these violations is a statement about the literature.
It must therefore rest on a replicable selection.

## 2. Review questions

- **L1.** Which studies propose, operationalise or apply quality criteria, smells or metrics for BDD specifications, and which of them detect quality problems automatically?
- **L2.** In those studies, which quality notions, units of analysis (step, scenario, feature, suite), detection techniques, corpora, validation procedures and tools are used?
- **L3.** Has any study measured the prevalence of quality problems in BDD specifications on real projects, or their persistence over a project's history, in any framework or language?

## 3. Scope

The mapping covers the quality of BDD specifications, including duplication, smells, metrics, maintenance and refactoring.

Studies on the survival of code smells and test smells are background for RQ2.
Rio and Brito e Abreu (2023), the studies it cites and the studies that cite it are read and selected purposively.
They are not counted in the mapping.

Grey literature (blogs, style guides, tool documentation) is not part of the mapping.

## 4. Step 1: database search

### Sources

| Source | URL |
|---|---|
| Web of Science Core Collection (institutional access, from the campus network or through the VPN) | https://www.webofscience.com |
| ACM Digital Library (ACM Full-Text Collection) | https://dl.acm.org |
| IEEE Xplore | https://ieeexplore.ieee.org |
| arXiv | https://arxiv.org |

The first three supply peer-reviewed publications; arXiv supplies preprints.

### Fields, language and dates

- The search covers title, abstract and keywords. In arXiv, which has no keyword field, it covers title and abstract.
- Only publications in English.
- No lower date limit, since the BDD literature is recent.

### Search string

```
("behaviour driven development" OR "behavior driven development" OR Gherkin
 OR (Cucumber AND (scenario* OR "step definition*")))
AND
(quality OR smell* OR metric* OR duplicat* OR maintenance OR maintainab*
 OR refactor* OR evolution)
```

The string is written in generic form and is adapted to the syntax of each source.
Hyphenated forms are covered by the syntax of each source or added explicitly.
The bare acronym "BDD" is not used, because it also denotes binary decision diagrams.
"Cucumber" is restricted for a similar reason.

### Pilot

The string is piloted before use and adjusted until it retrieves:
- Binamungu et al. (2018), Binamungu et al. (2020) and Binamungu and Maro (2023), in at least one of the peer-reviewed sources;
- Mughal et al. (2026a), in arXiv.

### Recording

For each source, the final string in the syntax of that source, the search date and the number of records returned are recorded.
The string is not changed after screening starts.

## 5. Step 2: selection

The records from the four sources are merged and duplicates are removed.
Each record is then screened on title and abstract, and the remaining records on full text, against the criteria below.

**Inclusion (all must hold):**
- the record is a peer-reviewed paper or a preprint;
- it reports a method, an experiment or an evaluation;
- it concerns the quality of BDD specifications (quality criteria, smells, metrics, duplication, refactoring or maintenance of scenarios or steps).

**Exclusion (any is enough):**
- no technical or empirical content (editorials, position papers, tutorials);
- full text not accessible;
- not written in English;
- another version of a work already included. The peer-reviewed version is kept in preference to a preprint and, between versions of the same kind, the most complete one.

Every record receives one of three decisions: include, exclude, or exclude but borderline.
The reason is recorded for every exclusion made on full text and for every borderline case.

### Preprints

Preprints are not peer reviewed. They are included for three reasons:
- question L3 asks whether a measurement exists at all;
- a negative answer is only credible if the search also covers work not yet published;
- the closest recent studies are preprints.

They are handled as follows:
- when a peer-reviewed version of a preprint exists, that version is kept and the preprint is discarded;
- every included preprint is flagged as such in the extraction table;
- in the synthesis, peer-reviewed studies and preprints are shown separately;
- any conclusion that rests only on preprints is identified as such.

## 6. Step 3: snowballing

The start set is the included studies, together with Binamungu et al. (2020) and Binamungu and Maro (2023).
It is used for backward snowballing (their reference lists) and forward snowballing (the papers that cite them, obtained from Google Scholar).
This follows the hybrid strategy of Wohlin et al. (2022).
Forward snowballing from the 2023 mapping is what brings the review up to date.

New candidates go through Step 2.
Snowballing is repeated on the newly included studies until one full iteration adds no new included study.

## 7. Step 4: data extraction

The same fields are extracted from every included study into one table:
- reference and publication type (peer-reviewed or preprint);
- quality notion (principle, smell, attribute or metric) and its definition;
- unit of analysis;
- whether the notion is evaluated within a scenario or in relation to other scenarios;
- detection technique (manual, rule-based, lexical, embedding-based, execution-based, other);
- framework and language;
- corpus (number of projects, files and scenarios; single snapshot or history);
- validation (labelled data, number of raters, agreement, precision and recall);
- availability and licence of the tool;
- main findings and stated limitations.

## 8. Step 5: synthesis

The studies are classified by quality notion, scope of evaluation (within-scenario or relational) and type of evidence (definition only, snapshot measurement, longitudinal measurement).
A cross-table of these dimensions shows what has been studied and where the gap lies.
Question L3 is answered explicitly from it.
The cross-table distinguishes peer-reviewed studies from preprints.

## 9. Part 2: survey of tools

The candidates are the tools for analysing Gherkin specifications that are used or described in the mapped studies, plus the official Gherkin parser.
There is no open search of code repositories.

For each candidate, its repository and official documentation are consulted, because papers describe tools only as they were at publication.
The following are recorded: name, the mapped studies that use it, address, implementation language, current version, date of the last release, licence, maintenance status and date of access.

Each candidate is assessed against these criteria:
- support for current Gherkin syntax, including the `Rule` keyword;
- works on feature files without executing the tests;
- can run unattended over many repositories and commits;
- licence that allows reuse;
- at least one release in the 24 months before the date of access, or code simple enough to be adapted.

The result is a comparison table, with the choice justified.

## 10. Roles and checks

The student runs the searches, screens every record and extracts the data.

**Option chosen:** B (single reviewer). **Date:** 2026-10-23.
The student screens alone, and the limitation is declared (Section 13).

**Reason.** Option A requires at least two suitable LLMs, from different families and not small models, available free of charge.
Free tiers limit usage and can switch to smaller models when the limit is reached.
The same full-size models could therefore not be guaranteed for the whole screening at no cost.

Only the cases the student cannot resolve are discussed with the supervisor.

## 11. Records

The following are kept in the project repository, under version control:
- the protocol (`protocol/review_protocol.md`);
- for each search, the source, the string, the date, the number of records (`review/searches/search_log.csv`) and the exported records (`review/searches/raw/`);
- the screening sheet, with the decision and the reason for each record (`review/screening.csv`);
- the extraction table (`review/extraction.csv`);
- the comparison table of Part 2 (`tool_survey/tool_comparison.csv`).

The number of records at each stage is reported.

## 12. Update

The database search and the forward snowballing are repeated before the final submission.
New records go through the same steps.

## 13. Limitations

- Selection and extraction are done by a single reviewer.
- The database search is limited to four sources and to publications in English, which snowballing compensates only in part.
- Preprints are included although they are not peer reviewed.
- Grey literature is excluded, although practitioner sources were the origin of the principles.
- The survey of Part 2 is restricted to tools reported in the mapped studies and to the official parser.

## References

Binamungu, L. P., Embury, S. M., & Konstantinou, N. (2018). Detecting duplicate examples in behaviour driven development specifications. In *2018 IEEE Workshop on Validation, Analysis and Evolution of Software Tests (VST)* (pp. 6–10). IEEE. https://doi.org/10.1109/VST.2018.8327149

Binamungu, L. P., Embury, S. M., & Konstantinou, N. (2020). Characterising the quality of behaviour driven development specifications. In V. Stray, R. Hoda, M. Paasivaara, & P. Kruchten (Eds.), *Agile Processes in Software Engineering and Extreme Programming (XP 2020)* (LNBIP, Vol. 383, pp. 87–102). Springer. https://doi.org/10.1007/978-3-030-49392-9_6

Binamungu, L. P., & Maro, S. (2023). Behaviour driven development: A systematic mapping study. *Journal of Systems and Software, 203*, Article 111749. https://doi.org/10.1016/j.jss.2023.111749

Mughal, A. H., Fatima, N., & Bilal, M. (2026a). Deja vu at scale: Paraphrase-robust detection of duplicate Gherkin steps in behaviour-driven software testing with sentence-transformer embeddings and a 1.1M-step open benchmark [Preprint]. arXiv. https://arxiv.org/abs/2604.20462

Ralph, P., & Baltes, S. (2022). Paving the way for mature secondary research: The seven types of literature review. In *Proceedings of the 30th ACM Joint European Software Engineering Conference and Symposium on the Foundations of Software Engineering (ESEC/FSE ’22)* (pp. 1632–1636). ACM. https://doi.org/10.1145/3540250.3560877

Rio, A., & Brito e Abreu, F. (2023). PHP code smells in web apps: Evolution, survival and anomalies. *Journal of Systems and Software, 200*, Article 111644. https://doi.org/10.1016/j.jss.2023.111644

Wohlin, C., Kalinowski, M., Felizardo, K. R., & Mendes, E. (2022). Successful combination of database search and snowballing for identification of primary studies in systematic literature studies. *Information and Software Technology, 147*, Article 106908. https://doi.org/10.1016/j.infsof.2022.106908

## Change log

| Date | Section | Change | Reason |
|---|---|---|---|
