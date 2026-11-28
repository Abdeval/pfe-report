# Consistency check: what Chapters 3–4 rely on in Chapters 1–2

Date: 6 November 2026. Checked against `chapters/chapter1/chapter1.tex` and
`chapters/chapter2/chapter2.tex` of the Overleaf project.

**Main finding: Chapter 1 covers everything Chapters 3–4 need about the LMS.
Chapter 2 is still a skeleton (headings only), so every item that belongs to
it is missing.** Chapter 3 already cites the related work and refers to
`\cref{sec-synthesis}` and `\cref{sec-related-work}`; these references resolve,
but they point at empty sections until Chapter 2 is written. Nothing in
Chapters 1–2 was rewritten; only `\label{}`s were added to four headings of the
Chapter 2 skeleton (`sec-kt`, `sec-llm`, `sec-mas`, `sec-synthesis`).

| Item | Status | Where |
|---|---|---|
| Moodle architecture | present | Ch. 1 §1.5.2 (PHP, database, `moodledata`, plugins) |
| Moodle web services (REST, token) | present | Ch. 1 §1.5.4 |
| Course structure: sections, activities, completion, restrict access | present | Ch. 1 §1.5.5 (completion, restrict access); sections and activities in §1.2.2 and §1.5.2 |
| LTI 1.3 | present | Ch. 1 §1.3.3 and §1.5.4 |
| Adaptive and personalised learning | missing | Ch. 2 §2.1 (heading only) |
| Knowledge tracing: BKT (four parameters), IRT, DKT | missing | Ch. 2 §2.1.2 (heading only) |
| Context-aware learning: Dey (2001), context dimensions | missing | Ch. 2 §2.2 (heading only) |
| LLMs: prompting, structured output, hallucination, RAG (embeddings, vector search) | missing | Ch. 2 §2.3 (heading only) |
| Multi-agent systems: definitions, orchestration patterns, LangGraph / CrewAI / AutoGen comparison table | missing | Ch. 2 §2.4 (heading only) |
| Related work: ELA Tutor, IJACSA-Arch, GenMentor, CA-MA-DRL, LASI-DC, the three surveys | missing | Ch. 2 §2.5 (heading only) |
| Synthesis: gaps G1–G8 and the positioning statement | missing | Ch. 2 §2.6 (heading only) |

Terminology: Chapter 1 uses *learner*, *LMS*, *learning context* and *Moodle
context* consistently with the glossary. It never uses *topic* or *mastery*,
so there is no conflict.

---

## Proposed paragraphs for the missing items

These are short paragraphs to start each section; they only use the sources
already in the bibliography (keys in `\cite{}`). Paste, then expand when you
write Chapter 2.

### §2.1.2 Learner model and knowledge tracing

```latex
Knowledge tracing estimates, from a learner's answers, the probability that
each skill is mastered. Bayesian Knowledge Tracing (BKT)~\cite{corbett1994kt}
models each skill as a hidden binary state (learned or not) with four
parameters: the prior probability $P(L_0)$ that the skill is known, the
probability $T$ of learning it at each opportunity, the probability $S$ of a
slip (a wrong answer although the skill is known) and the probability $G$ of a
guess (a right answer although it is not). After each answer, Bayes' rule
updates the estimate, then the learning step is applied. Item Response Theory
(IRT) instead estimates a learner ability and an item difficulty on a common
scale, and Deep Knowledge Tracing (DKT) replaces the hidden-state model by a
recurrent neural network trained on response sequences. BKT is
interpretable and works with few answers, which is why
\cref{chap-contribution} uses it.
```
(DKT and IRT need their own references: add `piech2015dkt` and an IRT textbook
before citing them.)

### §2.2.1 The notion of context

```latex
Dey defines context as ``any information that can be used to characterize
the situation of an entity'', where an entity is a person, place or object
relevant to the interaction between a user and an
application~\cite{dey2001context}. A system is context-aware when it uses
context to provide relevant information or services. In learning, the
relevant entities are the learner, the activity, the course and its
constraints. We therefore distinguish knowledge, activity, temporal and
pedagogical dimensions of the learning context, together with the device and
the affective state, which are harder to observe.
```

### §2.3 LLMs (prompting, structured output, hallucination, RAG)

```latex
Large language models generate text from a prompt that combines
instructions, examples and data. Applications that need machine-readable
results ask for a structured output, a JSON object that follows a given
schema, which can be validated in code. LLMs also \emph{hallucinate}: they
produce fluent statements that are not supported by their input, a risk the
surveys identify as central for education~\cite{wang2024llm4edu,chu2025agents}.
Retrieval-augmented generation (RAG) reduces this risk by retrieving passages
of a trusted corpus, here the course material, and placing them in the
prompt. Passages and questions are encoded as vectors by an embedding model,
and the closest passages are found by vector similarity, often combined with
a keyword search.
```

### §2.4 Multi-agent systems

```latex
An LLM-based agent combines a language model with a profile (its role), a
memory, tools it can call and a way to plan its actions. In an LLM-based
multi-agent system, several such agents communicate to solve a task; the
survey by Guo et al.\ describes them along four dimensions: the
agent--environment interface, agent profiling, communication, and capability
acquisition~\cite{guo2024mas}. The same survey warns that the hallucination of
one agent can cascade through the others. Common orchestration patterns are a
supervisor that routes requests, a sequential pipeline, a hierarchy of agents,
and an explicit graph or state machine.
```
The framework comparison table (LangGraph, CrewAI, AutoGen…) is still empty in
Notion. Fill its rows from each framework's current documentation before
writing it; I did not invent its content.

### §2.5 Related work

Use section 3 of `SOTA_Articles_Report.pdf` ("What the primary articles show,
and their weak points"): one paragraph per work (what it shows, then its weak
points), with the keys `lopezgoyez2026ela`, `khaddar2026ijacsa`,
`wang2025genmentor`, `sharif2026camadrl`, `matilla2025lasi`, and the surveys
`chu2025agents`, `wang2024llm4edu`, `guo2024mas`. The side-by-side table of
section 4 of that report becomes the comparison table of §2.5.3.

### §2.6 Synthesis and positioning

```latex
The analysis of the related work reveals eight gaps:
(G1) no LLM multi-agent system has an explicit, multi-dimensional context model;
(G2) LLM agents are disconnected from knowledge tracing;
(G3) adaptation covers one dimension at a time, rarely inside a real LMS;
(G4) tutoring is reactive;
(G5) there is no evidence of learning effect;
(G6) teacher control is weak;
(G7) grounding and reliability across agents are vague or unmeasured;
(G8) French and Arabic, the privacy of student data and the local context
(including Algerian Law 18-07~\cite{algeria_law1807}) are not addressed.

Recent work combines LLM agents and LMSs~\cite{lopezgoyez2026ela}, describes
interoperable but unimplemented architectures~\cite{khaddar2026ijacsa}, or
models a rich context without LLMs~\cite{sharif2026camadrl}. None grounds
specialised LLM agents on an explicit, shared model of the learner and their
context (knowledge, activity, temporal and pedagogical constraints), able to
adapt path, content and feedback jointly inside a real LMS, nor measures its
effect on learning. This work aims to fill that gap.
```
