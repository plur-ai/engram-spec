# The Open Engram Standard

> An **engram** is the smallest unit of AI agent memory: one atomic learned fact —
> a correction, a preference, a procedure — stored as a human-readable record
> *outside* the model, with provenance, a type classification, and a scope.
> An agent can recall it, an operator can read and edit it, and anyone can delete
> it, provably. **Memory should be something you can open.**

This repository is the home of the **Open Engram Standard**: the language-agnostic
specification of the engram object, the pack format that bundles engrams for
sharing, the `.plur` capsule that seals a pack into a single integrity-checked
file, and the trust model that lets a third party verify what they received.

It is written so that an independent implementer can read and write conformant
engrams, packs, and capsules **in any language**, without reading the reference
TypeScript. Implementations welcome.

## Contents

| File | What it is |
|---|---|
| [`ENGRAM-STANDARD-v1.md`](ENGRAM-STANDARD-v1.md) | The standard — conformance terminology (RFC 2119), engram object, packs, capsules, trust model |
| [`engram.schema.json`](engram.schema.json) | JSON Schema for a single engram |
| [`pack-manifest.schema.json`](pack-manifest.schema.json) | JSON Schema for a pack manifest |
| [`scope-metadata.schema.json`](scope-metadata.schema.json) | JSON Schema for scope metadata |

Schemas are also served at
[`plur.ai/spec/v1/engram.schema.json`](https://plur.ai/spec/v1/engram.schema.json)
(and siblings) for validation without cloning.

## Why an open format

There are two ways to give an AI long-term memory: bake it into model weights,
or store it externally in a format someone owns. The open engram format makes
four properties non-negotiable:

1. **Open / inspectable** — every engram is a plain-text record you can read, diff, and version.
2. **Instantly correctable** — fix one fact by editing one entry. No retraining.
3. **Provably forgettable** — delete the entry; under version control, the diff is the proof. You cannot prove erasure from model weights.
4. **Owned** — your data, your infrastructure. Memory follows the agent, not the vendor.

The Model Context Protocol (MCP) standardizes the *transport* between agents and
memory servers; it deliberately does not define a memory *format*. This standard
is the data layer: what a portable memory looks like inside.

## Reference implementation

[PLUR](https://github.com/plur-ai/plur) (Apache-2.0) is the reference
implementation — a local-first engram engine with an MCP server, used across
Claude Code, Cursor, Windsurf, OpenClaw, and Hermes.

- What an engram is (definition): https://plur.ai/engram
- Implementation-oriented spec of `@plur-ai/core` (schema, activation model, injection algorithm): https://plur.ai/spec.html
- Benchmarks: https://plur.ai/benchmark.html

## Source of truth

The standard is developed in the PLUR monorepo at
[`plur-ai/plur/spec/`](https://github.com/plur-ai/plur/tree/main/spec) and
mirrored here so the standard is citable and watchable independently of the
reference implementation. If the two ever disagree, the monorepo copy wins.

## License

- The specification text (`ENGRAM-STANDARD-v1.md`) is licensed under
  [CC-BY-4.0](https://creativecommons.org/licenses/by/4.0/).
- The JSON Schemas and any reference code are licensed under
  [Apache-2.0](LICENSE-Apache-2.0).
