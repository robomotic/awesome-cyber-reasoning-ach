# Bayesian Reasoning in Digital/Cyber Forensics

A curated (not exhaustive) collection of work that uses Bayesian reasoning or Bayesian networks (BNs) to evaluate competing hypotheses in digital and cyber forensics.

## Scope and notes

- Focus: digital forensics, network/cyber forensics, and legal-forensic Bayesian methods applicable to digital evidence.
- This list includes both direct case-model papers and methodological papers frequently reused in DFIR contexts.
- Some links point to publisher landing pages (may require institutional access).

## A. Core papers for competing-hypothesis evaluation

| # | Citation | Contribution | Link |
|---|---|---|---|
| A1 | Kwan, Chow, Law, Lai (2008), *Reasoning About Evidence Using Bayesian Networks* | Seminal BN model for a BitTorrent case; models sub-hypotheses and updates posterior belief from evidence. | [PDF](https://opendl.ifip-tc6.org/db/conf/ifip11-9/df2008/KwanCLL08.pdf) |
| A2 | Schneps et al. (2018), *Ranking the Impact of Different Tests on a Hypothesis in a Bayesian Network* | Ranks evidential tests by information impact on the main hypothesis in the BitTorrent BN. | [Article context](https://pmc.ncbi.nlm.nih.gov/articles/PMC7512417/) |
| A3 | Casey / Pollitt et al. (2021), *Quantitative evaluation of the results of digital forensic investigations* | Frames forensic conclusions via Bayes theorem, likelihood ratios, and competing hypotheses. | [Open access](https://pmc.ncbi.nlm.nih.gov/articles/PMC8112825/) |
| A4 | JDFSL admissibility-oriented paper (citing Kwan et al.) | Connects Bayesian belief networks to credibility, traceability, and legal admissibility of digital evidence. | [PDF](https://commons.erau.edu/cgi/viewcontent.cgi?article=1180&context=jdfsl) |
| A5 | Fenton, Neil, Berger (2016), *Using Bayesian networks to guide the assessment of new evidence in legal cases* | General legal BN framework reusable for prosecution-vs-defence digital evidence scenarios. | [Open access](https://pmc.ncbi.nlm.nih.gov/articles/PMC4930139/) |

## B. Network/cyber forensics BN models

| # | Citation | Contribution | Link |
|---|---|---|---|
| B1 | Liu et al., *A Probabilistic Network Forensics Model for Evidence Analysis* (NIST/IFIP stream) | BN over attack-path hypotheses; incorporates false-positive rates and multi-source evidence. | [NIST PDF](https://tsapps.nist.gov/publication/get_pdf.cfm?pub_id=919693) |
| B2 | NIST project page / CSRC hosted PNFM document | Supporting publication/distribution path for probabilistic network forensics model. | [CSRC PDF](https://csrc.nist.gov/CSRC/media/Projects/Measuring-Security-Risk-in-Enterprise-Networks/documents/pnfm_evidence-analysis.pdf) |
| B3 | GMU-hosted PNFM copy | Alternate hosted copy for the same model family. | [GMU PDF](https://mason.gmu.edu/~cliu6/papers/AProbabilisticNetworkForensicM.pdf) |
| B4 | Nisioti et al. (2022/2023), *Forensics for multi-stage cyber incidents* | Survey covering probabilistic reasoning for reconstructing and comparing incident scenarios. | [ScienceDirect](https://www.sciencedirect.com/science/article/pii/S2666281722001615) |
| B5 | Nisioti et al. mirror/open PDF | Open PDF version of the above survey. | [PDF](https://researchprofiles.herts.ac.uk/files/34402091/1_s2.0_S2666281722001615_main.pdf) |

## C. Implementation-oriented references

| # | Reference | Why useful for implementation | Link |
|---|---|---|---|
| C1 | Pappaterra (2018), BN-based online threat detection | Practical mapping from attack-tree scenarios to BN reasoning in detection workflows. | [Thesis/PDF](http://www.diva-portal.org/smash/get/diva2:1335798/FULLTEXT01.pdf) |
| C2 | Murray (2016), *Memory Forensics Triage* | Probabilistic triage ideas for prioritizing forensic artefacts. | [Thesis/PDF](https://www.westminster.ac.uk/sites/default/public-files/general-documents/rohan-murray-a-memory-forensics-triage-thesis.pdf) |
| C3 | Digitalforensics.com PNFM summary | Practitioner-facing summary of probabilistic network forensics workflow. | [Article](https://www.digitalforensics.com/blog/articles/a-probabilistic-network-forensic-model-for-evidence-analysis/) |
| C4 | BayesForensics repository | Example codebase relevant to Bayesian forensic experimentation. | [GitHub](https://github.com/mittalgovind/BayesForensics) |
| C5 | Korb & Nicholson, *Bayesian Artificial Intelligence* | Foundational BN modeling/inference concepts for building robust CPTs and sensitivity analysis. | [Semantic Scholar entry](https://www.semanticscholar.org/paper/Bayesian-Artificial-Intelligence-Korb-Nicholson/0150254af6d36b4e8eef503da2b6c25d16870ffb) |
| C6 | ACM DOI entry (recent) | Additional contemporary source to check for up-to-date BN-forensics techniques. | [DOI page](https://dl.acm.org/doi/10.1145/3769126.3769231) |
| C7 | Related recent ScienceDirect article | Potentially adjacent work for extending the literature set. | [ScienceDirect](https://www.sciencedirect.com/science/article/pii/S2666281725001635) |

## D. Practical implementation blueprint for cyber forensics tools

### 1) Model hypotheses and evidence

- Define top-level competing hypotheses (e.g., “attack path A occurred” vs alternatives).
- Define evidence nodes (alerts, logs, host artefacts, memory findings, timestamps).
- Connect causes to observations in a DAG (often derived from attack graphs/trees).
- Keep nodes at investigator-meaningful granularity (actions/scenarios, not only raw events).

### 2) Assign probabilities and uncertainty

- Build CPTs from expert elicitation when data are sparse.
- Learn/fit parameters where labeled historical data exist.
- Explicitly encode detector quality (false positives/false negatives).
- Run sensitivity analysis to identify assumptions that most affect posterior outcomes.

### 3) Select BN technology

- GUI/desktop ecosystems: Hugin, AgenaRisk, GeNIe/SMILE.
- Python ecosystems: `pgmpy`, `pyAgrum`, `pomegranate`, `pySMILE`.
- Large models may require approximate inference (sampling/loopy BP/variational methods).

### 4) Integrate in the DFIR pipeline

- Ingest evidence into a normalized case store.
- Map extracted artefacts to BN node states with deterministic rules.
- Re-run inference as new evidence arrives.
- Report posterior rankings and evidence influence (sensitivity/importance analysis).

### 5) How hypotheses are generated from a current alert or case

In practice, hypothesis generation is usually **hybrid**: templates + analyst customization + some automation.

#### Typical sources of hypotheses

- **Template libraries (most common starting point):**
	- Incident playbooks (phishing, ransomware, data exfiltration, insider misuse).
	- ATT&CK-aligned attack-path templates.
	- Prior case BN models (e.g., prosecution-vs-defence or attack-path alternatives).
- **Analyst-built hypotheses (always present):**
	- Case-specific alternatives that templates miss (maintenance activity, red-team traffic, misconfiguration, anti-forensics).
	- Legal/forensic framing for competing explanations (e.g., intentional act vs accidental/benign cause).
- **Semi-automated generation (emerging):**
	- Correlation engines and attack-graph generators propose candidate scenarios from alerts/log chains.
	- Automated mapping from alert metadata to pre-defined BN fragments.

#### Alert-to-hypothesis pipeline (operational)

1. **Trigger event arrives** (e.g., EDR alert, IDS sequence, suspicious login pattern).
2. **Classify alert context** (asset role, user role, business process, known change window).
3. **Select a base hypothesis template** (closest playbook/attack pattern).
4. **Instantiate competing hypotheses** for the case, typically including:
	 - malicious scenario(s),
	 - benign/administrative explanation,
	 - false-positive/sensor-error explanation.
5. **Attach case evidence nodes** (host artifacts, timeline checks, identity/logon traces, network indicators).
6. **Set priors/CPTs** from historical data + expert judgment + sensor FP/FN rates.
7. **Run BN inference and rank hypotheses** by posterior probability.
8. **Iterate as new evidence arrives** and track how rankings change over time.

#### Practical recommendation

- Treat templates as a starting scaffold, not a final model.
- Require analyst review before using posterior rankings for escalation or legal reporting.
- Keep an audit trail: template used, manual edits, CPT assumptions, and sensitivity results.

#### Example (single alert)

- **Alert:** unusual outbound transfer from finance host.
- **Competing hypotheses:**
	- H1: data exfiltration by compromised endpoint,
	- H2: legitimate scheduled backup/sync,
	- H3: tooling false positive.
- **Evidence updates:** process lineage, destination reputation, transfer timing, user session behavior, DLP signal quality.
- **Output:** posterior ranking of H1/H2/H3, plus top evidence items driving the result.

## F. Knowledge Graph vs Bayesian Belief Network for ACH

Both tools are used in cyber forensics and intelligence analysis to reason about hypotheses, but they represent and process uncertainty very differently.

### What is ACH?

Analysis of Competing Hypotheses (ACH) is a structured analytic technique that explicitly enumerates alternative explanations for an observed situation, maps evidence against each, and identifies which hypothesis best survives refutation.

**Origin:** It was developed by **Richards J. Heuer Jr.** at the **Central Intelligence Agency (CIA)** in the 1970s to reduce cognitive bias in intelligence analysis.
- **Key Reference:** Heuer, R. J. (1999). *Psychology of Intelligence Analysis*. Center for the Study of Intelligence, CIA. (Specifically Chapter 8).
- **Core concept:** We tend to look for evidence that confirms our favorite hypothesis; ACH forces us to look for evidence that *refutes* hypotheses.

Its methodology is widely adopted in DFIR, threat intelligence, and CTF analysis.

### Knowledge Graph (KG)

A KG represents entities (hosts, users, files, indicators, events) and their named relationships as a directed graph. It does **not** natively carry probability; it asserts facts and connections.

| Aspect | Knowledge Graph |
|---|---|
| Core data model | Nodes (entities) + edges (typed relationships) |
| Uncertainty handling | None natively; an entity/edge either exists or does not |
| Reasoning type | Logical/deductive (SPARQL, Cypher, OWL rules) |
| Hypothesis framing | Implicit: query patterns that match or fail to match |
| Strengths | Massive scale; fast entity linking; relationship traversal; provenance tracking |
| Limitations for ACH | Cannot assign or update probability over competing explanations; cannot propagate sensor FP/FN rates |
| Typical tools | Neo4j, ArangoDB, AWS Neptune, OpenCTI, MISP graphs |

### Bayesian Belief Network (BBN / BN)

A BN is a probabilistic graphical model: each node is a **discrete random variable** (a hypothesis or an observable) and each directed edge encodes a conditional probability. Inference propagates belief updates through the graph under evidence.

| Aspect | Bayesian Belief Network |
|---|---|
| Core data model | Nodes (variables with probability distributions) + edges (conditional dependencies) |
| Uncertainty handling | First-class: every node carries a probability distribution |
| Reasoning type | Probabilistic inference (belief propagation, VE, MCMC) |
| Hypothesis framing | Explicit: each hypothesis is a node with competing states (true/false/uncertain) |
| Strengths | Quantifies evidence strength; models FP/FN; updates posteriors incrementally; supports sensitivity analysis |
| Limitations | Small model size; requires CPTs; inference complexity grows with network size |
| Typical tools | Hugin, AgenaRisk, GeNIe, pgmpy, pyAgrum |

### Side-by-side comparison for ACH

| Criterion | Knowledge Graph | Bayesian Belief Network |
|---|---|---|
| Competing hypotheses | Matched via query patterns | Modelled as explicit probability nodes |
| Evidence integration | Assert presence/absence of edges | Update posterior probabilities via Bayes' rule |
| Sensor uncertainty | Not represented | Encoded as FP/FN conditional probabilities |
| Incremental updates | Add nodes/edges as new evidence arrives | Re-run inference; posteriors shift automatically |
| Auditability | Provenance and lineage naturally traceable | Sensitivity analysis shows which evidence drives conclusions |
| Legal defensibility | Strong for entity relationships, weak for probabilistic conclusions | Strong for quantifiable, probabilistic reasoning |
| Scale | Millions of entities/relationships | Tens to hundreds of nodes practical; thousands with approximate inference |

### Which to use for ACH in cyber forensics?

- **KG is the right tool** for evidence collection, entity linking, relationship discovery, and triage — it answers *what is connected to what*.
- **BN is the right tool** for hypothesis ranking, uncertainty quantification, and competing-explanation evaluation — it answers *how probable is each explanation given what we observed*.
- **Best practice**: use both together. Build a KG first to collect, normalize and link all case evidence, then project the relevant subgraph into a BN to perform formal ACH reasoning over competing hypotheses.

```
Alert/Case
     │
     ▼
Knowledge Graph ──────────── entity linking, relationship discovery, triage
     │
     │ project relevant facts
     ▼
Bayesian Network ──────────── hypothesis ranking, posterior probabilities, ACH
     │
     ▼
Analyst decision / report
```

### Relation to ACH stages

| ACH step | KG role | BN role |
|---|---|---|
| 1. List hypotheses | Source candidate scenarios from graph patterns | Define hypothesis nodes and states |
| 2. List evidence | Extract entities and relationships from KG | Map to observable nodes |
| 3. Assess diagnosticity | N/A | Compute Bayes factor / likelihood ratio per evidence item |
| 4. Refine hypotheses | Extend/prune graph | Add/remove nodes; re-run inference |
| 5. Draw conclusions | Subgraph visualisation | Rank by posterior; report sensitivity |

## G. Alternative Approaches: Formal Logic and Argumentation

Beyond probabilistic BNs, some research formalizes ACH using **symbolic logic** and **abductive reasoning** (e.g., Prolog, Datalog, Answer Set Programming). These approaches focus on structural consistency and validity rather than just probability.

### Key logic-based implementations

| # | Approach | Logic/Language | Core contribution | Citation/Ref |
|---|---|---|---|---|
| L1 | **Subjective Logic ACH** | Subjective Logic (Jøsang) | Replaces qualitative ACH scores with a calculus for uncertainty and trust; explicitly models "abductive conditionals." | [Pope & Jøsang (2005)](https://ieeexplore.ieee.org/document/1453775) |
| L2 | **Abductive Logic Programming (ALP)** | Prolog / ASP | Maps ACH to a logic program $(P, A, I)$ where hypotheses are *abducibles* $A$ that must entail observations $O$ without violating integrity constraints $I$. | [Kakas et al. (1992)](https://academic.oup.com/logcom/article/2/6/719/924823) |
| L3 | **Argumentation Frameworks** | Argumentation Logic (e.g., Gorgias) | Treat hypotheses as conflicting goals/claims; evidence "attacks" or "supports" arguments. Handles inconsistent evidence better than probability alone. | [Murukannaiah & Singh (2015)](https://ieeexplore.ieee.org/document/7307632) |
| L4 | **Hybrid Bayesian-Logic** | Probabilistic Prolog (ProbLog) | Fuses logical rules with probabilistic weights, effectively allowing ACH matrices to be reasoned over as a probabilistic program. | [Valtorta et al. (2005)](https://www.researchgate.net/publication/228833959_Extending_Heuer's_Analysis_of_Competing_Hypotheses_Method_to_Support_Complex_Decision_Analysis) |

### Prolog implementation concept

In a logic-based ACH (via ALP), you do not just "weigh" evidence; you solve for the set of hypotheses $\Delta$ such that:
1. $\Delta \cup \text{Rules} \models \text{Evidence}$ (Explanation)
2. $\Delta \cup \text{Rules} \nvDash \bot$ (Consistency)

```prolog
% Conceptual Prolog/ALP ACH schema
% 1. Abducibles (the row headers in ACH)
abducible(h_insider).
abducible(h_apt_compromise).

% 2. Background knowledge (the "if hypothesis, then expect evidence" rules)
expect(log_deletion) :- h_insider.
expect(beaconing) :- h_apt_compromise.

% 3. Integrity constraints (hypotheses inconsistent with facts or each other)
:- h_insider, h_apt_compromise.  % (If we assume mutually exclusive for this specific case)

% 4. Solve (Meta-interpreter)
% Find Deltas that explain observed evidence [log_deletion, beaconing]
```

This is fundamentally different from BNs: it tells you **which hypotheses are logically valid** explanations, whereas BNs tell you **which are most probable**.

## E. Download references

The articles so far also saved locally for reference.

1. https://opendl.ifip-tc6.org/db/conf/ifip11-9/df2008/KwanCLL08.pdf
2. https://pmc.ncbi.nlm.nih.gov/articles/PMC7512417/
3. https://pmc.ncbi.nlm.nih.gov/articles/PMC8112825/
4. https://commons.erau.edu/cgi/viewcontent.cgi?article=1180&context=jdfsl
5. https://pmc.ncbi.nlm.nih.gov/articles/PMC4930139/
6. https://tsapps.nist.gov/publication/get_pdf.cfm?pub_id=919693
7. https://csrc.nist.gov/CSRC/media/Projects/Measuring-Security-Risk-in-Enterprise-Networks/documents/pnfm_evidence-analysis.pdf
8. https://mason.gmu.edu/~cliu6/papers/AProbabilisticNetworkForensicM.pdf
9. https://www.sciencedirect.com/science/article/pii/S2666281722001615
10. https://researchprofiles.herts.ac.uk/files/34402091/1_s2.0_S2666281722001615_main.pdf
11. http://www.diva-portal.org/smash/get/diva2:1335798/FULLTEXT01.pdf
12. https://www.westminster.ac.uk/sites/default/public-files/general-documents/rohan-murray-a-memory-forensics-triage-thesis.pdf
13. https://www.digitalforensics.com/blog/articles/a-probabilistic-network-forensic-model-for-evidence-analysis/
14. https://github.com/mittalgovind/BayesForensics
15. https://www.semanticscholar.org/paper/Bayesian-Artificial-Intelligence-Korb-Nicholson/0150254af6d36b4e8eef503da2b6c25d16870ffb
16. https://dl.acm.org/doi/10.1145/3769126.3769231
17. https://www.sciencedirect.com/science/article/pii/S2666281725001635
