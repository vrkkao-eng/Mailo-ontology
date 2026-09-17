# MAILO — Medical AI Legal Ontology

An OWL 2 knowledge graph of EU regulatory obligations bearing on medical AI systems, with SHACL
constraints that make a subset of those obligations machine-checkable.

**Current release: v5.2.3** · 1,946 triples · [`https://w3id.org/mailo#`](https://w3id.org/mailo)
· documentation: [`index-en.html`](https://vrkkao-eng.github.io/Mailo-ontology/index-en.html)

---

## What is in it

| | |
|---|---|
| Triples | 1,946 |
| OWL classes | 65 |
| Object / datatype properties | 43 / 39 |
| Legal articles | 76 |
| Regulatory frameworks | 12 |
| Cases | 16 (7 CJEU, 6 UPC, 3 EPO) |
| Encoded principles | 12 (11 *ratio*, 1 *obiter*) |
| Cross-framework tensions | 10 |
| SHACL node shapes | 19 |

**Eight core instruments** for medical AI: GDPR, MDR, AI Act, PLD, EHDS, DGA, Data Act, and the
Trade Secrets Directive. Four further frameworks are encoded as context rather than as
compliance targets: the EU Charter, the PNR Directive (the source of *Ligue des droits
humains*), the EPC and the UPCA.

**Case law** is encoded as `RatioDecidendi` individuals, principally the post-2023 automated
decision-making line — *Ligue des droits humains* (C-817/19), *SCHUFA Holding* (C-634/21) and
*Dun & Bradstreet Austria* (C-203/22) — together with *FT v DW* (C-307/22) and *Bara*
(C-201/14). *Schrems II* and *La Quadrature du Net* are present as precedent nodes without
encoded ratio.

## Files

| File | Format |
|---|---|
| [`docs/ontology.ttl`](docs/ontology.ttl) | Turtle |
| [`docs/ontology.owl`](docs/ontology.owl) | RDF/XML |
| [`docs/ontology.nt`](docs/ontology.nt) | N-Triples |
| [`docs/ontology.jsonld`](docs/ontology.jsonld) | JSON-LD |
| [`docs/mailo_shacl_shapes.ttl`](docs/mailo_shacl_shapes.ttl) | SHACL shapes |

All four serialisations carry identical content. `https://w3id.org/mailo` content-negotiates
between them.

## Design commitments

**In-force numbering only.** MAILO encodes the article numbering of the text currently in
force. Encoding proposal numbering as though it were adopted is what produced the EHDS errors
corrected in v5.1.0, when the graph still followed COM(2022) 197 after Regulation (EU) 2025/327
had superseded it.

**Pending change is declared, not ignored.** The mirror failure is a graph that looks settled
when it is not. `mailo:PendingAmendment` records a proposed amendment separately, with the
procedure reference, the proposed effect, and — critically — `statusVerifiedAsAt`, the date the
status was last checked. A legislative status without a verification date cannot be audited.

**Holdings are distinguished from operationalisations.** Where a constraint restates what a
court decided, it says so. Where it is the ontology designer's machine-testable proxy for an
open-textured standard, it says that instead. The two are never silently merged. `EncodingBasis`
makes this queryable: of twelve encoded principles, eight are court holdings, three are the
designer's operationalisations, and one is a cross-instrument transposition that no court has
made.

**Why a case is present is recorded.** `InclusionBasis` states, for each of the sixteen cases,
whether it is here for its own subject matter, for a principle MAILO transposes to medical AI,
as procedural precedent, or as context. This matters because MAILO's method *is* transposition:
none of the three automated-decision judgments is a medical-AI dispute. C-817/19 concerns
passenger name records; C-634/21 and C-203/22 concern credit scoring. A criterion demanding
direct medical-AI subject matter would exclude the trilogy the ontology is built on.

**Some holdings are deliberately not encoded.** Where a judgment routes a question to a forum
without fixing a substantive outcome, no constraint is written. Encodability is treated as a
finding, not an obstacle.

## Validation status

The ontology passes its SHACL conformance tests, and every `LegalArticle`, case, principle and
cross-framework tension has now been checked against the official texts.

**It has not been externally validated.** All corrections to date were made by the author.
Independent expert review is planned but has not taken place. The conformance results are
evidence of internal consistency, not of legal correctness — please treat them that way. This
caveat carries more weight after v5.2.0 than before it: essentially every assertion checked in
that round required correction, and the checking was done the same way the original encoding
was, by one person without review.

Two findings from the audit are worth stating plainly, because together they bound what the
SHACL layer can do.

**Most of what was wrong was not machine-detectable.** The recurring defect was never a
malformed triple. It was a well-formed triple naming an article that genuinely exists, or citing
a paragraph range that genuinely exists, while saying something the source does not support.
Nothing in the graph disagreed with anything else. Two provisions had their normative character
inverted — a categorical prohibition recorded as curable by exception, an interpretive narrowing
recorded as invalidity — and two pairs of articles carried each other's content. Catching that
class of error needs a second, redundant representation of the same fact: storing the cited
article's heading or the cited paragraph's text alongside the citation. That work is open, and
it is the main reason the SHACL layer should not be read as a correctness guarantee.

**Where redundancy exists, detection follows.** The parts of the graph that *do* hold two
mutually constraining facts are the parts where errors were caught automatically. A citation to
a decision postdating the citing judgment, a `citesPrecedent` pointing at a blank node, an
article referenced but never declared — all surfaced from queries, and Parts IV and V of the
SHACL shapes now enforce them permanently. Each of those shapes was tested against the specific
defect that motivated it, not merely written.

## Release history

`https://w3id.org/mailo#` always dereferences the current release. Where a stable reference is
needed, cite the tag: each row below is an immutable snapshot.

| Version | Tag | Triples | SHACL node shapes |
|---|---|---|---|
| v5.2.3 | [`v5.2.3`](https://github.com/vrkkao-eng/Mailo-ontology/tree/v5.2.3) | 1,946 | 19 |
| v5.2.2 | [`v5.2.2`](https://github.com/vrkkao-eng/Mailo-ontology/tree/v5.2.2) | 1,945 | 19 |
| v5.2.1 | [`v5.2.1`](https://github.com/vrkkao-eng/Mailo-ontology/tree/v5.2.1) | 1,904 | 19 |
| v5.2.0 | [`5.2.0`](https://github.com/vrkkao-eng/Mailo-ontology/tree/5.2.0) | 1,859 | 19 |
| v5.1.0 | commit [`cc74e45`](https://github.com/vrkkao-eng/Mailo-ontology/tree/cc74e45477dfe541c5c0a849d9174122af053839) | 1,690 | 19 |

### v5.2.3 — canonical serialisation and residual consistency repair

Literal and metadata corrections only. No class, property, individual or SHACL constraint was
added, removed or altered.

**AI Act intervals** now follow the exclusive-end convention `[start, end)` used elsewhere in the
graph. `AIAct_v1_ProhibitedPractices` ends 2025-08-02 (was 2025-08-01) and
`AIAct_v2_GPAIModelObligations` ends 2026-07-27 (was 2026-07-31), so the three intervals abut
exactly: `[2025-02-02, 2025-08-02)`, `[2025-08-02, 2026-07-27)`, `[2026-07-27, …)`. The end values
had been written as inclusive last-days, which left a one-day and a four-day gap against the
following start dates — harmless to read, wrong to query.

**AILD withdrawal date.** The graph recorded 2025-02-10. That is when the Commission Work
Programme listed the intended withdrawal; the formal withdrawal followed on **6 October 2025**,
which is the operative date and is now recorded as such.

**Serialisations** regenerated from canonical Turtle and synchronised to `docs/`; all four graphs
verified isomorphic at 1,946 triples. `mailo_shacl_shapes.ttl` is untouched and keeps its own
version lineage.

### v5.2.2 — post-Omnibus correction and deferred modelling

Unlike v5.2.1, **this release does add a class and new individuals.** One class,
`mailo:EPOProceeding`; two `HighRiskRoute` individuals for the Annex I Section A and Section B
split; and five AI Act article individuals — Arts. 4a, 27, 43, 53 and 55. No object property and
no datatype property was added; those counts stand unchanged at 43 and 39.

**The headline is a legal change the graph had missed.** Article 1(9) of Regulation (EU)
2026/1744 deleted AI Act Art. 10(5); Article 1(6) inserted a new Art. 4a. This is not a
relocation. The legal basis for processing special categories of personal data for bias
detection and correction was lifted out of the high-risk training-data article into Chapter I,
and its personal scope was widened from providers of high-risk systems to deployers of
high-risk systems and to providers and deployers of other AI systems and models — on five
cumulative conditions, and creating no obligation to perform bias detection. Art. 4a is now an
article node and Art. 10 records the deletion, so a constraint still anchored to Art. 10(5) is
visibly without a source.

**The items v5.2.1 deferred are closed.** Annex I is no longer one set: `AnnexISectionARoute`
and `AnnexISectionBRoute` are declared, the MDR and IVDR are recorded as Section A legislation,
and MDR Annex VIII Rule 11 triggers the Section A route. Two things are worth keeping apart.
Applicability is set for the Art. 6(1)/Annex I branch as a whole: Art. 113 brings Chapter III
Sections 1–3 to it on 2 August 2028, a one-year deferral rather than the two years Annex III
received, and the provision does not key that date to Section A. What Section A status separately
determines is the conformity-assessment architecture, since it is the Section A legislation that
requires third-party assessment and that requirement is what Art. 43 addresses. Art. 43 carries the notified-body transition, where the second
subparagraph of Art. 43(3) sets 28 January 2028 while recital 18 describes eighteen months from
27 July 2026, which would fall on 27 January; the Article's date governs and both are recorded,
because a reader checking one against the other would otherwise suspect a transcription error.
Art. 27 is encoded as a provision, its FRIA date having been carried without it since v5.2.1.
Arts. 53 and 55 are added for temporal completeness; no constraint depends on the GPAI regime.

**Metadata and provenance.** The ECLIs for C-201/14, C-311/18 and C-511/18 were withheld in
v5.2.0 rather than supplied from memory — asserting an identifier from recall is the error class
that produced the original C-203/22 defect — and are now added, each checked against InfoCuria or
EUR-Lex and an independent secondary source, passing the citation-chronology constraint. The
misspelled `mailo:EPOProceding` is deprecated in favour of `mailo:EPOProceeding` and declared
equivalent, with instances typed against both; renaming a published IRI would break every
reference to it. `P_634_004` is marked unanchored, and the `art22ExceptionApplied` comment that
had presented that reading as a holding of C-634/21 is reworded. Two `triggeredBy` edges left
doubled by the v5.2.1 simplification are removed along with their orphaned amendment nodes, and
three dangling nodes are connected: Sanofi and Amgen as parties to `UPC_Sanofi_Amgen`, and
EP 3 435 866 to `UPC_Dexcom_Abbott`.

**Still open.** The unverified assertions on `UPC_10x_NanoString`, `UPC_Dexcom_Abbott` and
`UPC_Sanofi_Amgen`; the holding recorded for `P_Bara_001`; the conceptual confusion flagged on
`Tension_BlackBox_PatentProtection`, which treats patent protection as an incentive to secrecy
where a patent in fact requires disclosure; and independent expert review, which no finding in
any of the three corrective releases has received.

### v5.2.1 — factual consistency repair

A corrective release confined to instance-level facts. No class, property or SHACL shape was
added or altered, and no CJEU assertion was touched.

Two defects motivated it. The first was a representational split: the AI Act's article-level
assertions were attached to `mailo:AIAct` while its temporal versions were attached to
`mailo:AIAct_2024_1689`, with no relation between the two identifiers, so no query could reach
an applicable regulation version from an article. The same split was then found in the GDPR
representation. Both are now canonicalised, with the second identifier deprecated rather than
removed.

The second was a contradiction the graph held against itself. One part already recorded that
the AI limb of the Digital Omnibus had been adopted as Regulation (EU) 2026/1744, while the AI
Act timeline was still triggered by the provisional agreement of 7 May 2026 and still described
a conditional standards-availability mechanism that the adopted text does not contain. The
operative triggers now point to the adopted Regulation; the provisional agreement is retained
as legislative history and triggers nothing.

Four further corrections follow from the adopted text or from the original Regulation:
a version beginning 2 August 2028 had been flagged as the current one, and the current version
is now the post-Omnibus text in force from 27 July 2026, which records which text is in force
rather than asserting that the high-risk obligations apply; the Article 27 FRIA date moves from
2 August 2027 to 2 December 2027, scoped to Article 6(2) deployers; Chapters I and II are dated
to their application date of 2 February 2025 rather than to entry into force, leaving 1 August
2024 to 1 February 2025 deliberately uncovered because no provision applied in that interval;
and the original Annex III and Annex I high-risk dates, conflated in one version, are separated
to 2 August 2026 and 2 August 2027. `dcterms:date` was corrected on the AI Act and the PLD and
added to the MDR so that every EU instrument records the date of the act.

**This release does not implement temporal reasoning.** Application dates are regulation-version
metadata and are not evaluated at validation time. Modelling of the Omnibus's Annex I Section A
and Section B split, Articles 27 and 43, and the notified-body transitional period is deferred
to v5.2.2, which closes all four.

## Licence and citation

Released under [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/).

> Kao, C.-H. *MAILO — Medical AI Legal Ontology*, v5.2.3. https://w3id.org/mailo#

Developed at KU Leuven, Faculty of Engineering Science. Documentation generated with
[WIDOCO](https://github.com/dgarijo/Widoco); see [`docs/readme.md`](docs/readme.md) for
regeneration cautions.

Corrections and challenges to any encoded legal position are welcome — please open an issue.
