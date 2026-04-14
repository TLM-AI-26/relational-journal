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

## Open questions

- What "warmth" looks like concretely in interaction (tone, pace, stillness, reflection back).
- What a good day vs. bad day of using the Journal actually looks like.
- Whether the agent has a name / voice / presence separate from "Claude" or the base model.
- SQLite vs. JSON for storage (decide when we're about to write the first backend).
- iOS PWA limits on push notifications / background sync — future-native-app question if we want "agent reaches out" behavior. Not a blocker for v1.

## Explicitly chose NOT to do (yet)

- Adopt the prior CLAUDE.md or framework document as spec.
- Commit to any specific model (Mistral, Claude, etc.).
- Pre-design the safety/anchor mechanism before we understand daily use.
- Write a CLAUDE.md. It'll earn its place later.
