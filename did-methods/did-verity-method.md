# `did:verity` DID Method Specification

## Abstract

This document defines the `did:verity` DID method for the Verity Protocol, providing self-sovereign identity for organizations and individuals within the Verity ecosystem.

## Status

This specification is in **DRAFT** status for the v0.1.0

## DID Method Name

The namestring that identifies this DID method is: `verity`

A DID that uses this method MUST begin with: `did:verity:`

## Method-Specific Identifier

The method-specific identifier is a hierarchical structure:

```sh
did:verity:<namespace>:<identifier>
```

Where:

- `<namespace>`: One of `org`, `edu` or custom
- `<identifier>`: A unique string within the namespace

### Examples

```sh
did:verity:foundation
did:verity:org:cook-county-elections
did:verity:person:jane-smith-role-1
```

## CRUD Operations

### Create

A `did:verity` DID is created by:

1. Generating an Ed25519 key pair
2. Constructing a DID Document
3. Registering the DID with the Verity Ledger

### Read (Resolve)

Resolution follows this process:

1. Parse the DID into namespace and identifier
2. Query the Verity Ledger's DID Registry
3. Retrieve the DID Document from IPFS (via CID in ledger)
4. Return the DID Document

### Update

Updates require:

1. New DID Document with updated keys/services
2. Signature from current controller key
3. Transaction to update the CID in the ledger

### Deactivate

Deactivation marks the DID as revoked in the ledger.

## DID Document Format

Example DID Document:

```json
{
  "@context": [
    "https://www.w3.org/ns/did/v1",
    "https://w3id.org/security/suites/ed25519-2020/v1"
  ],
  "id": "did:verity:org:cook-county-elections",
  "verificationMethod": [{
    "id": "did:verity:org:cook-county-elections#key-1",
    "type": "Ed25519VerificationKey2020",
    "controller": "did:verity:org:cook-county-elections",
    "publicKeyMultibase": "z6MkrJV1... (Base58btc encoded or address)"
  }],
  "authentication": ["did:verity:org:cook-county-elections#key-1"],
  "service": [{
    "id": "#verity-agent",
    "type": "VerityAgentService",
    "serviceEndpoint": "https://agent.cookcounty.gov/verity"
  }]
}
```

## Security Considerations

- Key rotation must be supported
- Revocation must be immediate and verifiable
- DID Documents are immutable once anchored

## Privacy Considerations

- DIDs are pseudonymous by design
- No personal data in the ledger (only IPFS CIDs)
- Optional service endpoints can be added
