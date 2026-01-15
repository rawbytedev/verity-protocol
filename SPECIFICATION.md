# Verity Protocol Specification v0.1.0

## Executive Summary

The Verity Protocol enables cryptographic verification of digital content authenticity, specifically designed to combat AI-generated misinformation in democratic processes. It provides a multi-tier verification system that ranges from cryptographic proof for official sources to evidence-based analysis for social media content.

### Core Innovation

1. **Self-Sovereign Identity for Institutions**: Organizations control their own digital identities using W3C Decentralized Identifiers (DIDs)

2. **Cryptographic Content Binding**: Content is irrevocably linked to its source via digital signatures

3. **Multi-Tier Verification**: Different verification strengths based on content source and transformation

4. **Platform-Resilient Authentication**: Special handling for social media platform transformations

## 1. Introduction & Motivation

### 1.1 The Problem Space

AI-generated misinformation represents an existential threat to democratic processes. Recent elections have seen:

- Deepfake audio of candidates making false statements
- AI-generated images of fake election notices
- Synthetic videos of poll workers engaging in fraud

### 1.2 Limitations of Current Solutions

- **Fact-checking**: Too slow, reactive rather than proactive
- **Platform moderation**: Inconsistent, opaque, and politically fraught
- **Media literacy**: Insufficient against sophisticated AI forgeries
- **Digital signatures**: Don't work for platform-transformed content

### 1.3 Verity's Approach

Verity provides a protocol for:

1. **Issuance**: Trusted entities cryptographically sign official content
2. **Anchoring**: Signatures are recorded on an immutable ledger
3. **Verification**: Anyone can verify content authenticity in seconds
4. **Attribution**: Clear provenance chains showing content origin

## 2. Core Principles

### 2.1 Foundational Principles

1. **Self-Sovereignty**: Entities control their own digital identities
2. **Cryptographic Integrity**: Security based on proven cryptography, not heuristics
3. **Progressive Trust**: Multiple verification tiers with clear confidence levels
4. **Open Standards**: Built on W3C, IETF, and other open standards

### 2.2 Design Goals

- **Speed**: Verification under 2 seconds for common cases
- **Accuracy**: Cryptographic certainty for official sources
- **Usability**: Simple enough for non-technical users
- **Scalability**: Support for millions of concurrent verifications

## 3. System Architecture

### 3.1 High-Level Architecture

```sh
┌─────────────────┐    ┌─────────────────┐    ┌─────────────────┐
│   Issuance      │    │   Anchoring     │    │   Verification  │
│                 │    │                 │    │                 │
│ • Entity signs  │───▶│ • Store claim   │───▶│ • Public API    │
│   content       │    │   on ledger     │    │ • Tiered logic  │
│ • Create Verity │    │ • Batch anchor  │    │ • Return result │
│   Claim         │    │   to Bitcoin    │    │   with evidence │
└─────────────────┘    └─────────────────┘    └─────────────────┘
         │                       │                       │
         └───────────────────────┴───────────────────────┘
                               │
                     ┌─────────────────┐
                     │   Identity      │
                     │   Management    │
                     │                 │
                     │ • DIDs & VCs    │
                     │ • Accreditation │
                     │ • Delegation    │
                     └─────────────────┘
```

### 3.2 Component Overview

1. **Identity Layer**: DID-based identities, accreditation credentials
2. **Issuance Layer**: Tools for entities to sign content
3. **Ledger Layer**: Immutable record of claims and credentials
4. **Verification Layer**: Multi-tier verification logic
5. **Presentation Layer**: User interfaces and APIs

## 4. Cryptographic Foundations

### 4.1 Algorithms & Standards

- **Digital Signatures**: Ed25519 (RFC 8032)
- **Hashing**: SHA-256 for content, SHA-512 for Merkle trees
- **Content Integrity**: SHA-256 for files, perceptual hashing for images
- **Key Derivation**: HKDF (RFC 5869)
- **DID Methods**: `did:verity` (custom), `did:web` (initial)

### 4.2 Signature Format

Verity uses Data Integrity Proofs (JSON-LD Signatures):

```json
{
  "type": "Ed25519Signature2020",
  "created": "2024-01-01T00:00:00Z",
  "verificationMethod": "did:verity:org:example#key-1",
  "proofPurpose": "assertionMethod",
  "proofValue": "z58DAdFfa9SkqZMVPxAQpic7ndSayn1PzZs6ZjWp1CktyGesjuTSwRdoWhAfGFCF5bppETSTojQCrfFPP2oumHKtz"
}
```

## 5. Data Structures

### 5.1 Verity Claim

The core data structure representing an authenticity assertion. See [full schema](schemas/verity-claim.schema.json).

### 5.2 DID Documents

W3C-compliant DID Documents for entity identity. See [DID method spec](did-methods/did-verity-method.md).

### 5.3 Credential Types

1. **Accreditation Credential**: Foundation → Entity
2. **Delegation Credential**: Entity → Role/Member
3. **Verity Claim**: Entity → Content

## 6. API Specifications

### 6.1 Ledger Gateway API

For anchoring and querying claims. See [OpenAPI spec](apis/ledger-gateway.yaml).

### 6.2 Verification API

For public content verification. See [OpenAPI spec](apis/verification-api.yaml).

## 7. Verification Tiers

### 7.1 Tier S: Secure (Cryptographic Proof)

- **Source**: Official domains (.gov, .edu, verified entities)
- **Method**: Direct hash comparison
- **Confidence**: 1.0 (cryptographic certainty)
- **Use Case**: Election office websites, official publications

### 7.2 Tier 1: Social (Platform-Normalized)

- **Source**: Social media platforms (Twitter, Facebook, etc.)
- **Method**: Platform-specific normalization + hash comparison
- **Confidence**: 0.95 (platform transformation accounted for)
- **Use Case**: Shared official content on social media

### 7.3 Tier 2: Wild (Evidence-Based)

- **Source**: Any other location
- **Method**: Forensic analysis, watermark detection, perceptual hashing
- **Confidence**: 0.0-0.9 (probabilistic)
- **Use Case**: Forwarded messages, blogs, unknown sources

## 8. Content Type Handling

### 8.1 Text & PDF Documents

- Direct SHA-256 hashing
- Metadata preservation guidelines
- Character encoding requirements

### 8.2 Images

- Primary: TrustMark watermarking
- Fallback: Perceptual hashing (dHash)
- Platform transformation profiles

### 8.3 Video & Audio

- Keyframe extraction specifications
- Audio fingerprinting (Chromaprint)
- Format handling guidelines

## 9. Compliance & Testing

### 9.1 Compliance Suite

See [compliance test suite](compliance/README.md).

### 9.2 Implementation Requirements

- MUST support Ed25519 signatures
- MUST implement `did:verity` resolution
- MUST support all verification tiers
- SHOULD provide audit logging

## 10. Security Considerations

### 10.1 Threat Model

1. **Key compromise**: Key rotation procedures
2. **Ledger attacks**: Byzantine fault tolerance requirements
3. **Replay attacks**: Nonce and timestamp requirements
4. **Sybil attacks**: Accreditation requirements

### 10.2 Privacy Considerations

- Content hashes only (no content stored)
- Optional metadata minimization
- GDPR compliance guidelines

## 11. Governance

### 11.1 Versioning

- Semantic versioning (MAJOR.MINOR.PATCH)
- Backward compatibility requirements
- Deprecation policies

### 11.2 Accreditation Process

1. Entity application with proofs
2. Foundation verification
3. DID issuance and accreditation
4. Ongoing compliance monitoring

## Appendices

### A. Glossary

- **Verity Claim**: A cryptographically signed assertion of content authenticity
- **DID**: Decentralized Identifier (W3C standard)
- **Tier S/Secure**: Cryptographic verification via official sources
- **Platform Normalization**: Accounting for platform-specific transformations

### B. Example Flows

See [example flows](assets/example-flows.md).

### C. References

- W3C Verifiable Credentials Data Model
- W3C Decentralized Identifiers
- RFC 8032: Ed25519 Digital Signature Algorithm
- JSON Schema specification
