# MAILO — Medical AI Legal Ontology

An OWL 2 knowledge graph of EU regulatory obligations bearing on medical AI systems, with SHACL
constraints that make a subset of those obligations machine-checkable.

**Current release: v5.1.0** · 1,690 triples · [`https://w3id.org/mailo#`](https://w3id.org/mailo)
· documentation: [`index-en.html`](https://vrkkao-eng.github.io/Mailo-ontology/index-en.html)

---

## What is in it

| | |
|---|---|
| Triples | 1,690 |
| OWL classes | 63 |
| Object / datatype properties | 39 / 39 |
| Legal articles | 48 |
| Regulatory frameworks | 12 |
| CJEU cases | 7 (5 with encoded ratio decidendi) |
| Encoded ratio decidendi | 11 |
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
open-textured standard, it says that instead. The two are never silently merged.

**Some holdings are deliberately not encoded.** Where a judgment routes a question to a forum
without fixing a substantive outcome, no constraint is written. Encodability is treated as a
finding, not an obstacle.

## Validation status

The ontology passes its SHACL conformance tests, and every `LegalArticle` has been checked
article-by-article against the official texts across five audit rounds.

**It has not been externally validated.** All corrections to date were made by the author.
Independent expert review is planned but has not taken place. The conformance results are
evidence of internal consistency, not of legal correctness — please treat them that way.

One finding from the audit is worth stating plainly, because it bounds what the SHACL layer can
do: none of the five citation errors found in the final round was machine-detectable. Each was
a well-formed triple naming an article that genuinely exists, so nothing in the graph disagreed
with anything else. Catching that class of error needs a second, redundant representation of
the same fact — storing the cited article's heading alongside the citation, for instance. That
work is open.

## Licence and citation

Released under [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/).

> Kao, C.-H. *MAILO — Medical AI Legal Ontology*, v5.1.0. https://w3id.org/mailo#

Developed at KU Leuven, Faculty of Engineering Science. Documentation generated with
[WIDOCO](https://github.com/dgarijo/Widoco); see [`docs/readme.md`](docs/readme.md) for
regeneration cautions.

Corrections and challenges to any encoded legal position are welcome — please open an issue.
