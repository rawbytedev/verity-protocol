1. Content Verification Request:
    Input: Content URL + Platform Context
2. Content Normalization:
    • Download content from URL
    • Apply platform-specific normalization (compression, resizing)
    • Generate perceptual hash for images/video
    • Extract text for documents
3. Signature Discovery:
    • Check for embedded signatures in metadata
    • Query blockchain for content hashes
    • Check centralized registries
4. DID Resolution:
    • Parse issuer DID from signature
    • Resolve DID → DIDDoc (from IPFS via smart contract)
    • Check key authorization and revocation status
5. Signature Verification:
    • Verify cryptographic signature
    • Check delegation chain validity
    • Verify timestamp and expiration
6. Trust Assessment:
    • Determine verification tier (S, 1, 2)
    • Check Foundation verification status
    • Evaluate delegation depth and permissions
7. Result Presentation:
    • Generate verification badge
    • Show detailed verification report