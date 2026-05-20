# Theoretical Basis of the Teaching Methodology

> learn-via-repo's methodology (Minimal Comparison Method, Checkpoints A/B, three-layer progression, Diátaxis structure) isn't ad-hoc — each piece maps to an established theory in education or information architecture. This doc lists the theoretical backing, each with: core claim / source / matching rule in the skill.

---

## §1. Feynman Technique

**Core claim**: if you can't explain something in the simplest language (no jargon), you don't really understand it.

**Source**: Richard Feynman (Nobel laureate in physics)'s learning philosophy, adopted by Cornell Notes / Mortimer Adler and other learning-method systems.

**Matching rules**:
- Checkpoint A: "Explain in one sentence with no jargon"
- A student saying "got it" doesn't pass — they must Repack and pass the Feynman check
- If the teacher can't explain a concept clearly, go back and understand it; don't use "simply put" as a cover

**Counter-example**: memorizing "ReAct = Reasoning + Acting" ≠ understanding. Saying "look things up while writing the report, not look everything up first and not blindly make things up" is understanding.

---

## §2. Semantic Waves

**Core claim**: a good explanation must traverse the full wave — from abstract technical (high complexity) to concrete example (low complexity) and back to the technical concept (with new understanding). "Down only" is a "descending elevator" — the student knows the concrete example but can't transfer.

**Source**: Karl Maton, "Knowledge-Building" (2013), Legitimation Code Theory. Widely cited in computing-education research (e.g., SIGCSE).

**Matching rules**:
- After every concrete example, immediately Repack to the term
- After every abstract concept, immediately Unpack to a concrete example
- Forbidden "down only" — finishing an example without returning to the term
- Forbidden "up only" — only abstract definitions, no examples

**Counter-examples**:
- Down only: 5 minutes of "look things up while writing the report," never says "this is called ReAct" → student remembers "look-while-writing" but doesn't recognize "ReAct" next time
- Up only: 10 minutes of "Reasoning + Acting + Observation loop interleaving improves task quality," no examples → student is cognitively overloaded, nothing lands

---

## §3. Cognitive Load Theory

**Core claim**: working memory has limited capacity (about 4±1 chunks). Teaching too much at once causes overload and learning efficiency collapses.

**Source**: John Sweller (1988-2010 series of papers); adopted as a foundational pedagogy by Cambridge, Harvard education schools.

**Matching rules**:
- At most 3 core concepts per lesson
- Show the minimal version first (low load), then the industrial version (high load)
- A checkpoint every 15-20 minutes, avoid cognitive backlog

**Counter-example**: one lesson covering ReAct + Memory + Tools + Routing + Heartbeat → the student only remembers the last one

---

## §4. Scaffolding / Zone of Proximal Development

**Core claim**: students need "scaffolding" while learning — supports slightly above current ability, gradually removed until the student can do it independently.

**Source**: Lev Vygotsky's ZPD theory (1978); Wood, Bruner, Ross "Scaffolding" (1976) applied to teaching.

**Matching rules**:
- The minimal implementation is scaffolding (30-100 lines the student can read)
- Industrial enhancements are the gradual removal process (minimal → +error handling → +concurrency → +monitoring)
- Checkpoints A/B verify whether the scaffolding can be removed

**Counter-example**: throw 1600 lines of `attempt.ts` at the student right away → no scaffolding, beyond ZPD, student gives up

---

## §5. Comparative Learning / Contrasting Cases

**Core claim**: comparing two similar-but-different cases activates deeper understanding. Significantly more effective than learning one case alone.

**Source**: Schwartz & Bransford "A time for telling" (1998); Rittle-Johnson research series.

**Matching rules**:
- The core of the **Minimal Comparison Method** — minimal version vs repo version
- Three-column comparison table (minimal / repo location / explanation)
- §1.2 three-industry-solutions comparison

**Counter-example**: explaining only how the repo implements ReAct without comparing the minimal version or industry alternatives → student doesn't know where the trade-offs are

---

## §6. C4 Model (C4 Architecture Documentation)

**Core claim**: architecture documentation should have 4 layers: System Context → Container → Component → Code. Each layer stands on its own; zoom in progressively.

**Source**: Simon Brown, "Software Architecture for Developers" (2013-2025).

**Matching rules**:
- stage-1-foundations: System Context (domain layer)
- stage-2-architecture: Container + Component (architecture layer)
- stage-3-walkthroughs: Code (code layer)
- Strict layering; stage-2 doesn't paste lots of code, stage-3 doesn't drown in architecture talk

**Counter-example**: the existing OpenClaw `docs/learning/01-concepts.md` mixes concepts and code — layering unclear, student zigzags

---

## §7. Diátaxis Framework

**Core claim**: software documentation should split into four fundamentally different types, because they answer **fundamentally different kinds of questions**:
- **Tutorial** (learning-oriented, action): teach a beginner to do something
- **How-to** (work-oriented, action): teach a practiced user to solve a problem
- **Reference** (work-oriented, cognitive): precise factual lookup
- **Explanation** (learning-oriented, cognitive): understand the why

Each type has a different writing style, organization, reader expectation. Mixing them frustrates everyone.

**Source**: Daniele Procida (2014-2024), adopted by Django, CNCF, Gatsby, Numpy, and other major open-source projects. https://diataxis.fr/

**Matching rules**:
- stage-1-foundations / stage-2-architecture = Explanation (understand the why)
- stage-3-walkthroughs = Tutorial (follow along)
- stage-4-applied = How-to + Explanation (apply to your project)
- reference / resources = Reference (look up facts)

**Counter-example**: the existing OpenClaw `lessons/` + `designs/` two-artifacts pattern — both mix Explanation and Tutorial, 60% content overlaps, the student doesn't know which to read

---

## §8. Cognitive Apprenticeship

**Core claim**: learning a complex skill goes through 6 stages: Modeling (teacher demos) → Coaching (teacher guides) → Scaffolding → Articulation (student says it) → Reflection (compare with expert) → Exploration (self-directed).

**Source**: Collins, Brown, Newman "Cognitive apprenticeship: Teaching the crafts of reading, writing, and mathematics" (1989).

**Matching rules**:
- Modeling = stage-3-walkthroughs (teacher walks through code)
- Coaching = real-time checkpoints A/B + Scenario D unblocking strategies
- Scaffolding = Minimal Comparison Method (scaffolding via minimal version)
- Articulation = exercises/concept-checks.md (student says it in their own words)
- Reflection = exercises/transfer.md's "why it doesn't fit your project" questions (compare expert vs own approach)
- Exploration = stage-4-applied/mvp-sketch.md (student designs autonomously)

**Counter-example**: missing the Articulation stage — student only listens, doesn't speak; teacher thinks they get it → at the end discovers they don't

---

## §9. Bloom's Taxonomy

**Core claim**: cognitive ability has 6 levels from low to high: Remember → Understand → Apply → Analyze → Evaluate → Create. Teaching should progress level-by-level, with different checks per level.

**Source**: Bloom et al. (1956); revised version Anderson & Krathwohl (2001).

**Matching rules**:
- stage-1-foundations: Remember + Understand (remember domain concepts, understand terms)
- stage-2-architecture: Understand + Apply (understand the repo's design, apply similar designs to new scenarios)
- stage-3-walkthroughs: Apply + Analyze (can run the code, can analyze every design decision)
- exercises/code-finding: Evaluate (verify the accuracy of understanding)
- stage-4-applied: Create (create your own solution)

**Counter-example**: ask the student to Create ("design Mnemos's core schema") while skipping Remember → student hasn't internalized domain concepts, can't produce a reasonable design

---

## §10. High-quality tech blog structure

**Core claim**: good tech blogs all follow progressive complexity — work from a small example to a complete case. Start with a problem, not an answer.

**Source**: observation of Anthropic Engineering / Google AI Blog / Stripe Engineering / Vercel Engineering / Apple ML Research — patterns common to high-quality content.

**Matching rules**:
- walkthrough §0 general view: start with the problem, cite authoritative material
- walkthrough §1: reverse argument to spark curiosity
- walkthrough §4.1: minimal implementation (small example)
- walkthrough §4.4: industrial enhancement (full case)
- The whole piece uses file:line — verifiable

**Counter-example**: starting with "our system supports X / Y / Z" → the reader has no reason to care; they close the tab

---

## §11. Wayfinding (Information Architecture)

**Core claim**: the IA "wayfinding" principle — every page should tell the reader: where am I (You are here), where can I go, how do I get back.

**Source**: Peter Morville & Louis Rosenfeld, "Information Architecture for the World Wide Web" (1998-2015).

**Matching rules**:
- Every directory has a README.md explicitly marking "You are here"
- stage-1/2/3/4 numbering hints at the path
- walkthrough §6 links to exercises, §7 links to stage-4-applied
- Cross-cutting directories (reference / exercises / resources) accessible from any stage

**Counter-example**: the existing OpenClaw `lessons/` has no README — student doesn't know whether to start with 00 or 01

---

## §12. Constructionism (added in V2)

**Core claim**: learn by **building**, not passively receiving information. The learner producing something that runs is far more effective than 10 lectures. This is why stage-0 exists.

**Source**: Seymour Papert, "Mindstorms: Children, Computers, and Powerful Ideas" (1980) + "Constructionism" (1991). MIT Media Lab founder. Papert created the Logo programming language and believed learning is "building shareable artifacts outside the head," not just "building knowledge inside the head."

**Matching rules**:
- **stage-0-fundamentals/ mandatory** (when student is A/B/C/D level) — clone and run a beginner repo first, then read stage-1 theory
- **stage-0 takes priority over stage-1**: Papert opposed the traditional "theory first, experiment second" order — he argued "build first, reflect second"
- **graduation-check.md includes "can modify + can extend" questions**: just running it ≠ enough; must be able to change the system prompt, add a new tool, to count as understanding
- **stage-3 §4.1 references stage-0 code**: because the student has **run this code with their own hands**, the cognitive anchor is strongest ("remember that act() you ran?")
- **Scenario F** (companion stage-0) forbids the teacher giving the answer in 5 min — the struggle-self-rescue loop is what Papert called "productive failure"

**Counter-examples** (cross-domain):
- AI agent: throw OpenClaw's `attempt.ts` (1600+ lines of industrial code) at the student, skipping stage-0 hands-on → student has no "I've written act() myself" muscle memory; 1600 lines = instant overload
- Web framework: throw thousands of lines of Express's application.js + router at the student → student hasn't written their own middleware; can't locate "the prototype scenario" when looking at next() edge cases
- Database: throw SQLite's btree.c (tens of thousands of lines) at the student → student hasn't implemented a minimal cursor; gets lost the moment page-switching branches appear
- OS: throw Linux's scheduler at the student → student hasn't written their own minimal round-robin; can't understand "why we need" CFS's red-black tree optimizations

**Difference from Cognitive Apprenticeship**:
- Cognitive Apprenticeship: "teacher demos → student imitates"
- Constructionism: "student builds first → teacher just supports"
- learn-via-repo uses both: stage-0 = Constructionism; stage-3 = Cognitive Apprenticeship

**Key quote** (Papert):
> "Better learning will not come from finding better ways for the teacher to instruct, but from giving the learner better opportunities to construct."

This is the design philosophy of stage-0.

---

## §13. The most important belief, learned from experience

> "More lines of code = doing the same thing more robustly, safely, flexibly.
> Not more new concepts.
> Once you understand the 80-line skeleton, you understand the intent of the 1600-line version."

This isn't from a paper; it's from two months of teaching OpenClaw. Every time someone said "I can't read this 1600-line code," saying this sentence first gave them confidence.

The theories above can be reverse-engineered to derive this experience:

- **Cognitive Load**: 1600 lines of industrial code is way beyond ZPD; must drop to an 80-line minimal version first
- **Comparative Learning**: 80 vs 1600 comparison activates deep understanding
- **Scaffolding**: minimal version is scaffolding; industrial version is the reality after scaffolding is removed

---

## §14. How to apply these theories selectively

Not every lesson uses all theories. Pick by scenario:

| Scenario | Most relevant theory |
|------|-------------|
| **stage-0 hands-on prerequisite** | **Constructionism (Papert)** + Cognitive Apprenticeship Modeling |
| Concept introduction (stage-1) | Feynman + Semantic Waves + external material |
| Concept check | Feynman + Articulation |
| Code explanation | Scaffolding + Comparative Learning + Cognitive Load |
| Code verification | Bloom's Evaluate level + file:line location questions |
| Student transfer | Cognitive Apprenticeship Exploration |
| Doc organization | Diátaxis + C4 + Wayfinding |
| Overall pacing | Cognitive Load (≤3 concepts) + checkpoints (≤20 min) |

Each theory is "most useful at a specific moment," not "stacked all at once."

---

## §15. Further reading

- Feynman Technique: [The Feynman Technique](https://fs.blog/feynman-technique/)
- Semantic Waves: Karl Maton "Knowledge-Building" (2013)
- Cognitive Load: John Sweller "Cognitive Load Theory" (2011)
- ZPD / Scaffolding: Wood, Bruner, Ross (1976)
- Comparative Learning: Schwartz & Bransford "A time for telling" (1998)
- C4 model: [c4model.com](https://c4model.com/)
- Diátaxis: [diataxis.fr](https://diataxis.fr/)
- Cognitive Apprenticeship: Collins, Brown, Newman (1989)
- Bloom Taxonomy: Anderson & Krathwohl (2001) revised
- Information Architecture: Morville & Rosenfeld (2015)
- **Constructionism**: Seymour Papert "Mindstorms" (1980) + "Constructionism" (1991)
