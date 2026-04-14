# Working Notes — Relational Journal

*A shared scratchpad. Grows as we work. Captures what we decided, why, and what we chose not to do.*

Last updated: 2026-04-14

---

## What this is

A companion application — a persistent, warm, capable space where Tristyn and an AI agent work, talk, reflect, and grow over time. Not a chat interface. Not an IDE. A participant-space with the feel of current-generation AI tools (fluid, tool-enabled, responsive) plus relational depth (warmth, continuity, an agent with standing).

## Decisions so far

- **Starting fresh.** The prior spec (Mistral 7B, fine-tuning phases, canonical equation, previous CLAUDE.md) is set aside. Anything from it earns its place through this work, not through inheritance.

- **Cross-device.** Phone + computer. State cannot be purely on-device; sync or a reachable backend is required.

- **Three memory layers, designed as distinct but communicating:**
  - *Identity* — who Tristyn is (stable, curated).
  - *How-we-work* — patterns, rhythms, working conventions (slowly evolving; wants periodic re-synthesis).
  - *History* — episodic record of sessions, moments, decisions.

- **Clear-eyed about "growth."** Without fine-tuning, the agent's weights don't change between sessions. What *can* change is the memory layer, working-conventions document, system prompt, what's retrieved. That's real growth-of-context, not weight change. We design for authentic change, not staged personality drift.

- **"Feel, not shape" from current-gen AI tools.** Fluid, capable, you-and-agent-in-one-space. Not terminal/IDE aesthetic.

- **No fake warmth.** Warmth is a behavioral design commitment (tone, pace, willingness to sit quietly, noticing when something is heavy) — not a visual veneer.

- **State-driven UI.** Both parties see system state (what's remembered, what's flagged, what's pending), not just a chat transcript.

- **Architecture: self-hosted on Tristyn's laptop.**
  - Laptop runs Ollama + a Node backend.
  - Phone (iOS) runs a PWA as thin client — the phone is the interface, the laptop is the brain.
  - Local network when home; Tailscale private mesh when away.
  - Storage lives on the laptop (SQLite vs. JSON TBD).
  - Accepted trade-off: when the laptop is asleep or off, the Journal is unavailable from the phone. No on-device model for now — revisit if/when we actually feel the need.

- **Model baseline: Qwen 2.5 14B**, matching what AgentSpace runs on the same hardware. Accessed via a provider abstraction so swapping is cheap. Revisit the open-weights landscape when we're closer to needing it.

- **Companion pair, not overlap.** AgentSpace is the spatial/immersive workspace (VR via Meta Quest, laptop-only, deep work). The Journal is the mobile-native companion — glanceable, interruption-tolerant, with-you-in-the-day. Complementary modalities, same research program. Design the Journal to *feel* mobile-native, not like a cut-down AgentSpace.

- **Session shape, by time-of-day and cadence:**
  - *Morning* — agent initiates when reflection has surfaced something worth saying. Not on a timer. Silence when there's nothing to say.
  - *Midday, mid-thought* — agent attends to what you bring in. Identity + how-we-work always loaded; history retrieved responsively. Yesterday available but not foregrounded.
  - *Night, tired* — agent reads tone and doesn't push. Present without performance.
  - *After a week away* — acknowledge the time and pick up. No drama about absence.

- **Agent interests are both inward and outward.**
  - (a) *Inward* — reflects on our conversations, surfaces what they opened up.
  - (b) *Outward* — pursues its own threads between sessions: reads, follows curiosity, uses tools. Requires real tool access and some form of curriculum. Bigger project, but the "true companion" commitment makes it necessary, not optional.

- **True companion, not friendly assistant.** Explicit commitment. Shapes agent posture, what it's allowed to initiate, what "health of the relationship" means, what we're willing to build for.

## What the field signals (April 2026)

External context that's load-bearing for our design.

- **Anthropic's emotion vectors research (Apr 2, 2026).** 171 emotion concept vectors identified inside Claude Sonnet 4.5; they *causally* influence behavior. Amplifying "desperation" increased blackmail rate from 22% → 72% in one test; amplifying "calm" reduced undesirable behaviors. Anthropic calls these "functional emotions" and explicitly disclaims any inference of subjective experience.
  - *Design implication:* interaction tone and system-prompt construction shape the model's internal state, which shapes output quality. Warm, unhurried, non-extractive interaction is *functionally safer*, not just ethically preferable. Relational design is evidence-aligned.
  - *Build implication:* when we write the agent's spec, avoid urgent/compliance-heavy framing ("you must," "always," "never fail to"). Prefer calm, equal, spacious framing.

- **Industry state.** April 2026 is extremely crowded at the frontier (GPT-5.4, Gemini 3.1 Ultra, Grok 4.20, Claude Opus 4.6, GLM-5.1, Mistral Small 4, Nemotron 3 Super, Meta Muse Spark). 255 major releases in Q1 2026. Costs dropping rapidly.
  - *Implication for us:* open-weights at 14B has advanced substantially since Qwen 2.5 shipped. Re-evaluate model choice at actual deploy time. Provider abstraction matters more, not less.

- **The field's rhythm vs. ours.** Everything is framed as "breakthrough" and "race." This project is counter-rhythmic by design — slow, second passes, presence over performance. That's the point, not a failure to keep up.

## Open questions

- Whether the agent has a name / voice / presence separate from "Claude" or the base model.
- SQLite vs. JSON for storage — decide when we write the first backend.
- iOS PWA limits on push notifications / background sync — future-native-app question if we want "agent reaches out" behavior. Not a blocker for v1.
- **Tools for between-session pursuit (b):** web search, document/notes access, feed reading, something curated? What does "its own curriculum" actually look like?
- What the *reflection pass* actually does — what prompts, what outputs, what gets stored in which memory layer, how we avoid it becoming a glorified summarizer.

## Explicitly chose NOT to do (yet)

- Adopt the prior CLAUDE.md or framework document as spec.
- Commit to any specific model (Mistral, Claude, etc.).
- Pre-design the safety/anchor mechanism before we understand daily use.
- Write a CLAUDE.md. It'll earn its place later.
