# AstrBot Memory Fabric

A private-chat memory and behavior plugin for AstrBot.

This repository contains the design and implementation of the memory system. The deployed AstrBot/NapCat runtime remains in the sibling `qq-astrbot` workspace and is never treated as source code or test data.

## Current status

Design phase. No runtime implementation is enabled yet.

## Scope of the first release

- Private chat only, single primary user first.
- Full raw conversation ledger for audit and replay.
- Autonomous memory formation without per-message approval.
- Episodic memories, durable facts/preferences, fuzzy concepts, and weighted associations.
- Time decay, reinforcement, consolidation, versioning, reversible deletion, and audit trails.
- Retrieval that can influence wording, topic choice, and bounded proactive-care candidates.
- Proactive behavior starts at a conservative B-level policy; the architecture leaves room for stronger autonomy later.

## Non-goals for the first release

- Replacing AstrBot, OneBot, NapCat, or the DeepSeek provider.
- Group-chat intelligence.
- Model-weight fine-tuning.
- Copying an entire third-party plugin into this repository.
- Making every inferred concept a hard fact.

See [the architecture overview](docs/architecture/overview.md) and [the design draft](docs/superpowers/specs/2026-10-23-memory-fabric-design.md).

## License

Licensed under the GNU Affero General Public License v3.0 only ([AGPL-3.0-only](LICENSE)).
Third-party components retain their original licenses and attribution requirements.
