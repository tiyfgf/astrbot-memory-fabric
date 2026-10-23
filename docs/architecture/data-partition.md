# Private-chat data partition

## Evidence partition

Append-only records of user and bot turns. Evidence is immutable except for redaction metadata. It may contain raw text references, normalized text for search, timestamps, conversation/session ids, and content hashes.

## Episodic partition

Concrete experiences derived from evidence: what happened, who was involved, what the user said or did, and the event time. Episodic records retain evidence links and can become less detailed over time without deleting the original evidence.

## Semantic partition

Stable facts and preferences such as names, preferences, habits, commitments, and relationship observations. Every revision has `observed_at`, `valid_from`, optional `valid_to`, confidence, source evidence, and a supersession link.

## Fuzzy concept partition

Soft concepts that are useful without being asserted as facts. A concept contains a label or embedding region, affective valence/arousal, confidence, abstraction level, supporting episodes, and decay state. It may represent an association such as “sweet things often feel comforting” without claiming a universal rule.

## Association partition

Weighted edges between people, objects, topics, concepts, emotions, episodes, and actions. Edges have strength, last activation, reinforcement count, decay parameters, and provenance. Activation is a temporary runtime state and is never mistaken for a new fact.

## Behavior partition

Response guidance and proactive candidates are derived projections. They are not canonical memories. Each candidate records triggering activations, policy version, cooldown checks, and decision outcome.

## Audit partition

Immutable events describing extraction, merge, revision, recall, activation, decay, consolidation, deletion, restore, and proactive decisions. Audit data must support replay and explanation without exposing secrets.
