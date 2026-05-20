# Testing Guide (for invited test buddies)

> Hi — thanks for taking the time to test this skill. This doc tells you **how to test** and **how to give feedback** so your input lands where it matters.

Total testing time: **60-90 minutes** (not counting actually learning a domain — that takes 8-12 weeks).

---

## What we're testing

I'm **not** asking you to go through a full domain learning cycle (that's months). I want to test the **trigger-to-artifact-generation-to-first-lesson** experience:

1. Does the Phase 0 entry interaction feel natural? Are the questions reasonable?
2. When Phase 2C presents you candidate repos, is the evaluation table clear? Does it help you decide?
3. When the artifacts (10 top-level directories) are generated, what's your first impression on opening them? Do you know where to start?
4. Are the repos recommended in `stage-0-fundamentals/recommended-repos.md` actually qualified? (Click into a couple and skim.)
5. How does the first piece of stage-1 (mental model) read? You don't need to read all of it — just scan.
6. The AI's tone when talking to you — does it feel like a real teacher, or like generated cards?

---

## Testing tasks

Please run through **at least 1 scenario**. If you want to do more, try crossing domains (e.g., Scenario 1 + Scenario 3).

### Scenario 1: Pretend you're a total beginner

Pretend you're a complete beginner in some domain (even if you're actually an expert).

```
You input: "Use this repo to teach me X"
(Pick X as a domain you really have **no experience** in. E.g., if you're a frontend dev, pick redis; if you're a backend dev, pick v8.)
```

Expected: the skill will
1. Go down Path A (you brought a repo)
2. Ask your level → you pick A (total beginner)
3. Determine "beginner + industrial-scale repo" → recommend stage-0
4. Run Phase 2C to find 3-5 beginner repo candidates
5. Let you evaluate the candidates
6. Generate the full artifacts after you pick

### Scenario 2: You have a direction but no specific repo

```
You input: "I want to learn web frameworks but don't know which repo to start with"
(Or swap "web frameworks" for any direction you actually care about)
```

Expected: the skill will
1. Go down Path B (you brought a direction)
2. Ask your level + what you want to do after
3. Run a search and give you 3-5 target repo candidates (Express / Koa / Fastify / Hono etc)
4. Once you pick, then find a stage-0 beginner repo
5. Generate artifacts

### Scenario 3: Exploring mode

```
You input: "I want to learn something technical, but I don't know what"
```

Expected: the skill will
1. Go down Path C (exploring)
2. Use a conversational approach with 1-3 questions to help you narrow down
3. If you say "I don't know" — show you a domain menu to pick from
4. Once you converge on a direction, switch to Path B

---

## What to watch for during the test

While you're going through the flow, **keep an eye on these observation points** — when you come back to give feedback, say specifically which step triggered the reaction.

### Experience

- **The opening line**: how does the skill open Phase 0? Comfortable or awkward?
- **Tone**: does the AI use jargon you don't know? Drop acronyms without explaining? Spit out short fragmented sentences like "X for A, Y for B, Z for C"?
- **Pacing**: from your trigger to artifact generation, how long total? Feels too long-winded, just right, or too rushed?
- **Interactivity**: when you're asked to make choices, do you have enough info? Or are you picking blind?

### Content

- **Are recommended repos reasonable?** — click into a couple of the 3-5 candidates Phase 2C gave you. Are they really built on langchain / spring (which would be disqualifying)? Are the star counts right?
- **Is the generated artifact structure understandable?** Open the directory; can the root README.md tell you "where to start" within 5 minutes?
- **Does stage-0 graduation-check make sense?** Open `stage-0-fundamentals/graduation-check.md`. Could you actually pass / fail those 5 questions?

### Bugs

- **Crashes / errors / flow stuck**: screenshot + tell me how to reproduce
- **AI takes the wrong path**: you clearly brought a repo (A), it routed you to Path C (exploring)
- **Repeated questions**: Phase 0 asked something, then Phase 1 asked it again

---

## Feedback template

After testing, file a GitHub issue using the template below. **Length doesn't matter, specificity does** — no need to write a "professional bug report," just tell me like you'd tell a friend.

```markdown
## Test scenario

I ran scenario ___ (1/2/3 or custom).

The role I pretended to be: ___ (e.g., "frontend engineer who's never touched databases")

Domain / repo I picked: ___

## Overall impression (30-second version)

___ (e.g., "Flow works end-to-end, but the Phase 0 opening felt a bit mechanical;
the recommended beginner repo was solid;
but the first stage-1 piece read too academic")

## Specific observations

### Experience

- Opening line: ___
- Tone: ___
- Pacing: ___ (too long / just right / too rushed)
- Interactivity: ___

### Content

- Recommended repo reasonableness: ___
- Artifact structure clarity: ___
- stage-0 graduation-check: ___

### Bugs / anomalies

___ (if any)

## What I'd want improved (in priority order)

1. ___
2. ___
3. ___

## I'd recommend this skill to

___ (e.g., "a coworker switching from frontend to database internals" — this helps me understand who the real audience is)

## I wouldn't recommend this skill to

___ (e.g., "already-senior engineers — they might find it too verbose" — this helps me understand the limits)
```

---

## Some smaller questions

### Q: Do I actually need to learn the domain while testing?

No — you only need to go through Phase 0 → Phase 4, look at the generated artifact structure and the opening of stage-0 / stage-1, and give me feedback on that **pre-experience**. If you actually want to dig in further, that's a bonus, not a requirement.

### Q: How long does testing one scenario take?

Fastest: 20-30 minutes (just run the flow and skim the artifacts). Longest: 60-90 minutes (if you're willing to click through a few candidate repos and look carefully).

### Q: I'm not familiar with education theory — Constructionism / Feynman etc. What now?

**You don't need to know any of it.** Those theories are the design backing of the skill; as a user, what you should feel is "oh this skill doesn't let me skip the basics" or "oh this skill makes me rephrase things in my own words." Just check whether that experience suits you — no need to read [theory.md](./references/theory.md).

### Q: What if I give up partway through?

Just tell the AI "I'm stopping" — the skill won't push you to finish. Later you can give feedback like "I dropped off at step ___, because ___" — **the dropout point is itself the best feedback**. It tells me the threshold is too high at that point.

### Q: Can I invite others to test with me?

Yes, as long as they have a software-engineering background (otherwise the feedback perspective doesn't match). Have them follow this doc.

---

## Feedback channels

- **GitHub issue** (preferred): [new issue](https://github.com/CZYCW/learn-via-repo/issues/new)
- **Direct contact**: open a GitHub issue first, or I'll have shared a way to reach me before you started testing

I'll respond to every piece of feedback. **If your feedback triggers a V4-style improvement, I'll credit you in the commit message / changelog** (tell me if you'd rather not be named).

---

Thanks again for spending the time on this — every bit of feedback makes the skill more useful for the people who come after you to actually learn something with it.
