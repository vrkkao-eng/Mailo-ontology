About Widoco output
===================
The purpose of Widoco is to reuse and integrate existing tools for documentation, plus the set of features listed below:
* Separation of the sections of your html page so you can write them independently and replace only those needed.
* Automatic annotation in RDF-a of the html produced.
* Association of a provenance page which includes the history of your vocabulary (W3C PROV-O compliant).
* Metadata extraction from the ontology plus the means to complete it on the fly when generating your ontology.
* Guidelines on the main sections that your document should have and how to complete them.

Widoco will create 3 different folders:
|
|-provenance (a folder including an html and RDF serialization of how the documentation page was created)
|-resources (folder with the different resources)
|-sections (folder with the different sections of the documentation, separated for easy editing. Just edit one and the main page will be updated)

Completing ontology metadata.
===================
Widoco uses the ontology metadata to update a configuration file. If you complete that configuration file (ended up widoco.conf), the tool will enhance your html with additional details, such as how to cite the document, previous revisions, icons with the licence, etc.

Browser issues
==========
The result of executing Widoco is an html file. We have tested it in Mozilla, IE and Chrome, and when the page is stored in a server all the browsers work correctly. If you view the file locally, we recommend you to use Mozilla Firefox (or Internet Explorer, if you must). Google Chrome will not show the contents correctly, as it doesn't allow  XMLHttpRequest without HTTP. If you want to view the page locally with Google Chrome you have two possibilities:

a) Place the file in a server and access it via its URL (for example, put it in dropbox and access through its public url).

b) Execute Chrome with the following commands :

(WIN) chrome.exe --allow-file-access-from-files,

(OSX) open /Applications/Google\ Chrome.app/ --args --allow-file-access-from-files

(UNX) /usr/bin/google-chrome --allow-file-access-from-files

Do you have a problem? open an issue at https://github.com/dgarijo/Widoco

## Changelog

### v5.2.0 (2026-09-10) — second corrective release
Completes the audit begun in v5.1.0, covering everything that release did not reach: the
ten cross-framework tensions, the principles and cases outside the trilogy, and the GDPR,
AI Act, MDR, Data Act and TSD provisions, plus the SHACL shapes. Coverage rises from 48 to
71 articles. Full account in the ontology's `rdfs:comment`.

- **Tensions**: none of the ten was sound. Four cited the wrong provision, two cited
  C-203/22 at the wrong paragraphs, and the instances used two incompatible modelling
  patterns, so cross-tension queries silently omitted a third of the set. Harmonised.
- **GDPR**: Art.22(3) attaches only to Art.22(2)(a) and (c), not (b) — material for medical
  AI on a national legal basis. Art.22(4) is a prohibition on basing such decisions on
  Art.9(1) data, not "enhanced protection". Art.22(1) restated in the words of the
  provision rather than pre-committing on the prohibition-versus-right question.
- **AI Act**: Art.86's right to explanation reaches only Annex III systems. Medical devices
  are high-risk by the Annex I route, so Art.86 and Art.26(11) do not apply to them; GDPR
  Arts.15(1)(h) and 22 carry the explanation duty alone. `HighRiskRoute` encodes this, and
  MDR Annex VIII Rule 11 — the classification rule that produces it — is added and linked.
  Art.13 addresses deployers, not affected persons.
- **TSD**: Art.5(a) is Charter Art.11 freedom of expression, not a data-subject information
  right. Art.1(2)(b), which preserves disclosure duties owed to authorities, was absent and
  is the correct anchor. Art.3 added (reverse engineering is lawful acquisition).
- **PLD**: Arts.4 and 7 were transposed; Art.5, the strict-liability rule, was missing.
- **EHDS**: six provisions added, including Art.52 (IP and trade secrets in secondary use)
  and Art.53(1)(e)(ii), which expressly permits secondary use for training and evaluating
  algorithms in medical devices and AI systems.
- **Data Act**: Art.3 is a design duty and Art.4 the access right, with different
  application dates; Art.17 is the request procedure, not public-emergency sharing.
- **Cases**: G 1/19 is a COMVIK inventive-step ruling and the Enlarged Board held that
  whether the simulated system is technical is *not* decisive; all three EPO instances
  re-anchored from EPC Art.52 to Arts.56/83/84. C-307/22 involves no AI. Two of sixteen
  cases now carry a verified medical-AI technology claim.
- **Shapes**: the v5.1.0 hierarchy fix inverted what target classes mean; three C-817/19
  shapes had drifted and all five now target `MedicalAISystem`.

**Not verified**: three CJEU cases lack ECLIs, deliberately not supplied from memory; three
UPC instances retain unverified assertions, flagged on the instances. No finding in either
corrective release has been reviewed by a second EU data-protection specialist.


- **v5.1.0 (2026-09-05)** — corrective release, five audit rounds. 1,690 triples.
  - **Case law.** All nine CJEU paragraph mappings across C-817/19, C-634/21 and C-203/22
    verified against the judgment texts; two substantive mischaracterisations corrected (the
    categorical health-status exclusion under the PNR Directive, and the treatment of the
    strict-necessity test). `citesPrecedent` graph repaired; T 1191/19 re-dated and its holding
    rewritten.
  - **Legislation.** Eleven citations corrected. EHDS renumbered from the COM(2022) 197
    proposal to Regulation (EU) 2025/327 as adopted (data permit Art.68, opt-out Art.71, secure
    processing environment Art.73, HealthData@EU Art.75, EHDS Board Art.92). PLD causation
    presumption moved to Art.10(4); DGA to Art.29. A systematic audit of all 48 `LegalArticle`
    individuals then found five further errors: PLD Art.4 (Definitions) had been recorded as
    the strict-liability provision (Art.5) and PLD Art.7 (Defectiveness) as the
    software-as-product definition (Art.4(1)); DGA Art.2 (Definitions) as the Chapter II re-use
    framework (Art.3); Data Act Art.15 (exceptional need) as trade-secret protection
    (Art.4(6)-(8)); and Data Act Art.17 (request procedure) as the B2G obligation (Art.14).
  - **Structure.** `AutomatedDecisionSystem` is now the superclass and `MedicalAISystem` its
    subclass, correcting an inverted hierarchy. Inclusion and encoding bases made explicit, so
    the graph distinguishes a court holding from the ontology designer's operationalisation of
    one. `hasResolutionStatus` declared — it had been in use on tension instances without ever
    being typed.
  - **New.** `PendingAmendment` vocabulary records proposed but unadopted legislative change
    without contaminating in-force numbering, carrying `statusVerifiedAsAt` so a status
    assertion is auditable rather than silently rotting. One instance is declared: the Digital
    Omnibus proposal on Data Act Chapter V (COM(2025) 837 final, 2025/0360(COD)), which would
    delete Arts 14 and 15 in favour of a new Art.15a.
  - **SHACL.** Parts IV and V added: citation chronology, citation target integrity, inclusion
    basis, technology-claim scope, encoding basis, precedence-level coherence.

- v5.0.3 (2026-08): `rdfs:comment` clarifying that `owl:versionIRI` values are stable citations,
  not resolvable URLs.
- v5.0.2 (2026-08-12): corrected ECLI for C-203/22 (Dun & Bradstreet Austria) — 2025:145 to
  2025:117.

## A note on validation

Every correction above was made by the author. The ontology has automated SHACL conformance
tests, and it passes them, but it has not been reviewed by independent legal experts. External
validation is planned and has not yet happened. Please read the conformance results as evidence
of internal consistency, not of legal correctness.

None of the five citation errors found in the final audit round was detectable by any SHACL
shape: each was a well-formed triple naming an article that genuinely exists. Detecting that
class of error would require storing the cited article heading alongside the citation, so that
a mismatch has something to disagree with. That is open work.

## Regenerating this documentation

This folder is WIDOCO output. Two cautions, both observed in practice:

1. WIDOCO re-serialises the ontology and **inflates the triple count** (1,690 became 1,912).
   After regenerating, restore the canonical `ontology.ttl`, `.owl`, `.nt` and `.jsonld` and
   discard WIDOCO's versions.
2. WebVOWL counts `owl:equivalentClass` axiom nodes and `rdfs:Datatype` entries as classes, so
   `webvowl/data/ontology.json` reports 111 where the ontology declares 63. That is a rendering
   artefact. Do not edit the ontology to make the numbers agree.

Regenerating also **overwrites this file**, including the changelog above. Restore it afterwards.

## Changelog

### v5.2.0 (2026-09-10) — second corrective release
Completes the audit begun in v5.1.0: the ten cross-framework tensions, the principles and
cases outside the trilogy, the GDPR, AI Act, MDR, Data Act and TSD provisions, and the
SHACL shapes. Coverage 48 → 71 articles, 1,690 → 1,859 triples. Full account in the
ontology's `rdfs:comment`.

- **Tensions**: none of the ten was sound. Four cited the wrong provision; two cited
  C-203/22 at the wrong paragraphs; the instances used two incompatible modelling patterns,
  so cross-tension queries silently omitted a third of the set.
- **GDPR**: Art.22(3) attaches only to Art.22(2)(a) and (c), not (b). Art.22(4) is a
  prohibition on basing such decisions on Art.9(1) data, not "enhanced protection".
- **AI Act**: Art.86's right to explanation reaches only Annex III systems, so it does not
  apply to medical devices high-risk by the Annex I route. `HighRiskRoute` encodes this and
  MDR Annex VIII Rule 11 — the classification rule that produces it — is added and linked
  via `triggersRoute`. Art.13 addresses deployers, not affected persons.
- **TSD**: Art.5(a) is Charter Art.11 freedom of expression, not a data-subject information
  right. Art.1(2)(b) is the correct anchor for regulatory disclosure and was absent.
- **PLD**: Arts.4 and 7 were transposed; Art.5, the strict-liability rule, was missing.
- **EHDS**: six provisions added, including Art.52 and Art.53(1)(e)(ii), which expressly
  permits secondary use for training and evaluating algorithms in medical devices.
- **Data Act**: Art.3 is a design duty and Art.4 the access right; Art.17 is the request
  procedure, not public-emergency sharing.
- **Cases**: G 1/19 is a COMVIK inventive-step ruling; all three EPO instances re-anchored
  from EPC Art.52 to Arts.56/83/84. Two of sixteen cases carry a verified medical-AI claim.

**Not verified**: three CJEU cases lack ECLIs, deliberately not supplied from memory; three
UPC instances retain unverified assertions, flagged on the instances. No finding in either
corrective release has been reviewed by a second EU data-protection specialist.


- **v5.1.0 (2026-09-05)** — corrective release, five audit rounds. 1,690 triples.
  - **Case law.** All nine CJEU paragraph mappings across C-817/19, C-634/21 and C-203/22
    verified against the judgment texts; two substantive mischaracterisations corrected (the
    categorical health-status exclusion under the PNR Directive, and the treatment of the
    strict-necessity test). `citesPrecedent` graph repaired; T 1191/19 re-dated and its holding
    rewritten.
  - **Legislation.** Eleven citations corrected. EHDS renumbered from the COM(2022) 197
    proposal to Regulation (EU) 2025/327 as adopted (data permit Art.68, opt-out Art.71, secure
    processing environment Art.73, HealthData@EU Art.75, EHDS Board Art.92). PLD causation
    presumption moved to Art.10(4); DGA to Art.29. A systematic audit of all 48 `LegalArticle`
    individuals then found five further errors: PLD Art.4 (Definitions) had been recorded as
    the strict-liability provision (Art.5) and PLD Art.7 (Defectiveness) as the
    software-as-product definition (Art.4(1)); DGA Art.2 (Definitions) as the Chapter II re-use
    framework (Art.3); Data Act Art.15 (exceptional need) as trade-secret protection
    (Art.4(6)-(8)); and Data Act Art.17 (request procedure) as the B2G obligation (Art.14).
  - **Structure.** `AutomatedDecisionSystem` is now the superclass and `MedicalAISystem` its
    subclass, correcting an inverted hierarchy. Inclusion and encoding bases made explicit, so
    the graph distinguishes a court holding from the ontology designer's operationalisation of
    one. `hasResolutionStatus` declared — it had been in use on tension instances without ever
    being typed.
  - **New.** `PendingAmendment` vocabulary records proposed but unadopted legislative change
    without contaminating in-force numbering, carrying `statusVerifiedAsAt` so a status
    assertion is auditable rather than silently rotting. One instance is declared: the Digital
    Omnibus proposal on Data Act Chapter V (COM(2025) 837 final, 2025/0360(COD)), which would
    delete Arts 14 and 15 in favour of a new Art.15a.
  - **SHACL.** Parts IV and V added: citation chronology, citation target integrity, inclusion
    basis, technology-claim scope, encoding basis, precedence-level coherence.

- v5.0.3 (2026-08): `rdfs:comment` clarifying that `owl:versionIRI` values are stable citations,
  not resolvable URLs.
- v5.0.2 (2026-08-12): corrected ECLI for C-203/22 (Dun & Bradstreet Austria) — 2025:145 to
  2025:117.

## A note on validation

Every correction above was made by the author. The ontology has automated SHACL conformance
tests, and it passes them, but it has not been reviewed by independent legal experts. External
validation is planned and has not yet happened. Please read the conformance results as evidence
of internal consistency, not of legal correctness.

None of the five citation errors found in the final audit round was detectable by any SHACL
shape: each was a well-formed triple naming an article that genuinely exists. Detecting that
class of error would require storing the cited article heading alongside the citation, so that
a mismatch has something to disagree with. That is open work.

## Regenerating this documentation

This folder is WIDOCO output. Two cautions, both observed in practice:

1. WIDOCO re-serialises the ontology and **inflates the triple count** (1,690 became 1,912).
   After regenerating, restore the canonical `ontology.ttl`, `.owl`, `.nt` and `.jsonld` and
   discard WIDOCO's versions.
2. WebVOWL counts `owl:equivalentClass` axiom nodes and `rdfs:Datatype` entries as classes, so
   `webvowl/data/ontology.json` reports 111 where the ontology declares 63. That is a rendering
   artefact. Do not edit the ontology to make the numbers agree.

Regenerating also **overwrites this file**, including the changelog above. Restore it afterwards.
