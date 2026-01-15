# Example Verification Flows

## Flow 1: Tier S - Official Document Verification

1. **User**: Accesses `https://elections.cookcounty.gov/voter-guide.pdf`
2. **System**: Computes SHA-256 hash of PDF
3. **System**: Queries ledger for hash
4. **Ledger**: Returns Verity Claim with issuer DID
5. **System**: Resolves DID to DID Document
6. **System**: Verifies signature on claim
7. **Result**: `Cryptographic Proof - Issued by Cook County Elections`

## Flow 2: Tier 1 - Social Media Image Verification

1. **User**: Copies Twitter image URL
2. **System**: Fetches image from `pbs.twimg.com`
3. **System**: Applies Twitter normalization profile
4. **System**: Computes hash of normalized image
5. **System**: Compares with `platformHashes.twitter` in claim
6. **Result**: `Platform Verified (Twitter) - 96% confidence`

## Flow 3: Tier 2 - Unknown Source Verification

1. **User**: Uploads image from email
2. **System**: Attempts TrustMark watermark detection
3. **System**: Computes perceptual hash
4. **System**: Compares with known claims (fuzzy match)
5. **System**: Runs forensic analysis if needed
6. **Result**: `Likely Authentic - 72% confidence based on perceptual match`
