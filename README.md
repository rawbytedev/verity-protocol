# Verity Protocol Specification

[![CC BY 4.0][cc-by-shield]][cc-by]

## Overview

The Verity Protocol is an open standard for cryptographically verifying the authenticity of digital content, with initial focus on election integrity and combating AI-generated misinformation.

## Version

**Current**: v0.1.3 (Pre-release)

## Quick Links

- [Full Specification](SPECIFICATION.md)
- [Verity Claim Schema](schemas/verity-claim.schema.json)
- [API Definitions](apis/)
- [DID Method Specification](did-methods/did-verity-method.md)

## Repository Structure

```sh
verity-protocol/
├── SPECIFICATION.md          # Complete protocol specification
├── schemas/                  # JSON Schema definitions
├── apis/                     # OpenAPI API specifications
├── did-methods/              # DID method specifications
├── compliance/               # Compliance test suites
├── assets/                   # Diagrams and visuals
└── changelog/               # Version history
```

## Getting Started

For implementers:

1. Read the [SPECIFICATION.md](SPECIFICATION.md)

2. Review the JSON schemas for data structures

3. Check API specifications for integration points

For investors:

1. Review the [Executive Summary](SPECIFICATION.md#executive-summary)

2. See [Architecture Overview](SPECIFICATION.md#architecture-overview)

3. Examine [Demo Flows](assets/demo-flows.md)

## License

This specification is licensed under [CC BY 4.0](LICENSE).
This work is licensed under a
[Creative Commons Attribution 4.0 International License][cc-by].

[![CC BY 4.0][cc-by-image]][cc-by]

[cc-by]: http://creativecommons.org/licenses/by/4.0/
[cc-by-image]: https://i.creativecommons.org/l/by/4.0/88x31.png
[cc-by-shield]: https://img.shields.io/badge/License-CC%20BY%204.0-lightgrey.svg
