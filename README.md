# MAILO — Medical AI Legal Ontology

An OWL 2 knowledge graph of EU regulatory obligations bearing on medical AI systems, with SHACL
constraints that make a subset of those obligations machine-checkable.

**Current release: v5.2.0** · 1,859 triples · [`https://w3id.org/mailo#`](https://w3id.org/mailo)
· documentation: [`index-en.html`](https://vrkkao-eng.github.io/Mailo-ontology/index-en.html)

---

## What is in it

| | |
|---|---|
| Triples | 1,859 |
| OWL classes | 64 |
| Object / datatype properties | 43 / 39 |
| Legal articles | 71 |
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

## Licence and citation

Released under [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/).

> Kao, C.-H. *MAILO — Medical AI Legal Ontology*, v5.2.0. https://w3id.org/mailo#

Developed at KU Leuven, Faculty of Engineering Science. Documentation generated with
[WIDOCO](https://github.com/dgarijo/Widoco); see [`docs/readme.md`](docs/readme.md) for
regeneration cautions.

Corrections and challenges to any encoded legal position are welcome — please open an issue.
