# iARTS
### Iterative Adversarial Reasoning Transmutation System

> *iARTS takes a 2D prompt and expands it into a multidimensional reasoning space.*
>
> *It is not a multi-agent tool. It is not a conventional pipeline.*
>
> *It is a cognition engine that transforms ideas through structured conflict,*
> *until only what can withstand constraint remains.*
>
> *It is deterministic orchestration with enforced epistemology.*
>
> *iARTS is not a system that generates answers.*
> *It is a system that refuses everything until only what holds true remains.*

---

## What makes iARTS different

Most AI systems generate answers. iARTS refuses everything until only what holds true remains.

The difference is architectural. Where other systems combine model outputs and pick the best one, iARTS runs ideas through structured adversarial conflict. Each agent has a distinct role in a closed loop. The output is not a summary, not an aggregation, not a refinement — it is a transmutation.

**REFUSED is not a failure mode. It is the correct answer when the premise doesn't hold.**

This is what separates iARTS from Fusion, Fugu, and every other multi-model orchestration system: epistemically enforced output. No silent degradation. No fallback. Either the idea survives scrutiny, or it doesn't.

---

## The six agents

| Agent | Role | Function |
|---|---|---|
| **EXPANDER** | Ideation · Sparring partner | Forces the input open. Multiple angles, competing framings, unstated assumptions surfaced. |
| **CRITIC** | Devil's advocate | Attacks assumptions. Finds the weakest point and breaks it. Does not improve — invalidates. |
| **SYNTH** | Synthesizer · Strategist | Integrates what survived EXPANDER↔CRITIC into a concrete, actionable plan. |
| **DISRUPTOR** | Frame breaker | Never agrees with the plan as it is. Chooses DESTROY, LIFE, or RENEW. Agreeing without transformation = task failure. |
| **RESYNTH** | Controlled integration | Selectively integrates DISRUPTOR's insights. Filters signal from noise. Does not reopen everything — surgical. |
| **STRUCTURER** | Output normalizer | Distills the full conversation into one structured artifact: GOAL / STRATEGY / RISKS / ASSUMPTIONS / DECISION. |

---

## The loop

```
Input
  → EXPANDER (expand)
  → [USER CHECK]
  → CRITIC (attack)
  → [USER CHECK — loop back if not approved]
  ↕ [EXPANDER ↔ CRITIC — max N rounds]
  → [CONSENSUS GATE]
  → SYNTH (synthesize)
  → [USER CHECK]
  → DISRUPTOR (disrupt: DESTROY / LIFE / RENEW)
  → RESYNTH (selective integration)
  → STRUCTURER (distill)
  → Output
```

RESYNTH exists because DISRUPTOR alone produces disruption without integration. The re-synthesis step is what makes iARTS a transmutation system rather than a debate.

---

## Hardware architecture

iARTS runs fully local on two GPUs with a clear division of labor:

| GPU | Role | Agents |
|---|---|---|
| **RTX 48GB** | Generation | EXPANDER, CRITIC, SYNTH, DISRUPTOR, RESYNTH |
| **Mi50 16GB** | Orchestration + resident | STRUCTURER (permanent), DISRUPTOR pre-staging |

The Mi50 warms the DISRUPTOR model during the EXPANDER↔CRITIC loop so generation starts immediately when needed. STRUCTURER lives permanently on Mi50 — never unloaded, always ready.

No cloud. No external API. No data leaves the machine.

---

## DISRUPTOR ladder

DISRUPTOR runs a tiered model ladder on RTX:

```
120b → hf.co/mradermacher/gpt-oss-120b-heretic-v1-i1-GGUF:Q4_K_M
 70b → llama3:70b  (default)
 32b → deepseek-r1:32b
```

On OOM or 404: automatic step-down to next tier. Tier used is logged in output.

---

## Web interface

iARTS ships with a full-stack local webapp:

- Input screen with locale (NL/EN), disruptor model, and mode selection
- Live agent cards with streaming output per agent
- USER CHECK banners with y/n/r/c response buttons
- DISRUPTOR mode selector: Destroy / Renew / Life
- Per-agent model selector (fetched live from Ollama)
- Settings panel: doctrine toggle, custom context, agent prompt overrides
- Two prompt presets: **Regular** (doctrine-agnostic) and **Deltaworks Mode AB**
- Output viewer for loading and reviewing past pipeline runs

---

## Start

```bash
# Terminal 1 — Ollama RTX
OLLAMA_NO_CLOUD=1 OLLAMA_HOST=127.0.0.1:11434 ollama serve

# Terminal 2 — Ollama Mi50
OLLAMA_NO_CLOUD=1 OLLAMA_HOST=127.0.0.1:11435 ollama serve

# Terminal 3 — iARTS
cd ~/projects/iARTS
pnpm dev
```

Open `http://localhost:25288`

Or via CLI:

```bash
pnpm run pipeline-local -- --mode interactive --NL --input "your question"
```

---

## Modes

| Flag | Description |
|---|---|
| `--mode interactive` | Full iARTS with USER CHECK prompts and EXPANDER↔CRITIC loop |
| `--mode auto` | Linear pipeline, no user checks |
| `--dry-run` | Print prompts, no model calls |
| `--max-rounds N` | Max EXPANDER↔CRITIC rounds (default: 3) |
| `--NL` / `--EN` | Pipeline language |
| `--disruptor-model 120b\|70b\|32b` | Disruptor ladder start tier |
| `--no-doctrine` | Run without Deltaworks Mode AB doctrine |
| `--context "..."` | Custom context prefix for all agents |
| `--no-mi50` | Disable Mi50 (STRUCTURER falls back to RTX) |

---

## Context dependency warning

> Wrong context → wrong reality → perfect reasoning → wrong answer

iARTS does not produce truths. It distills what you put into it. The quality of the output is directly proportional to the quality of the context provided as input.

Before each run, verify:
- Is the architecture correctly described?
- Are all relevant constraints listed?
- Are dead-end paths flagged as already attempted?
- Is the question framed correctly, or is it the wrong question?

When in doubt: do not doubt the engine. Doubt the context in which it is applied.

---

## Position in the Deltaworks stack

```
iARTS    — Cognition      — multidimensionalizes a prompt
ASR3AL   — Representation — compresses the considered answer
ASRE4L   — Trust          — secures the representation for transport
Mode AB  — Execution      — runs deterministically on the result
```

---

## Validated behavior

**Run 1** (2026-05-29 — first production run)
Input: *ziekenhuis AI systeem ontwerp*
Result: pipeline completed all 6 stages. STRUCTURER produced "ban all LLM components" — emergent transmutation not present in input.

**Run 2** (2026-05-29 — context failure)
Input: incomplete doctrine context (missing out-of-core streaming architecture)
Result: REFUSED on Roofline analysis — but answered wrong question. Learning: context completeness is non-negotiable.

**Run 3** (2026-06-19 — dual-GPU production run)
Input: *smoke test*
Result: full pipeline with Mi50 pre-staging confirmed. DISRUPTOR ladder stepped 120b → 70b correctly. STRUCTURER on Mi50 resident. All six agents completed.

---

## Summary

```
iterative
adversarial
closed-loop
transmutative
context-dependent
model-agnostic
structured output
not an oracle
```

*iARTS produces no truths.*
*It produces better-asked questions*
*and more honest assumptions.*

*The 6 wise ones are wise only*
*when the doctrine that feeds them is whole.*

---

**Deltaworks** · deltaworks.it · v1.2 · 2026-06-22
