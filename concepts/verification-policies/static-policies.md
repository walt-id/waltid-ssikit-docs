# Static Policies

## General policies

### SignaturePolicy

Verifies the signature of the W3C Verifiable credential.

### JsonSchemaPolicy

Verifies against the associated JSON schema. Note that the attribute _credentialSchema_ must be set an the JSON schema must be accessible by the http URL.

### ValidFromBeforePolicy&#x20;

Verify by valid from.

### ExpirationDateAfterPolicy

Verify by expiration date.

### ChallengePolicy&#x20;

Verify challenge, Argument: ChallengePolicyArg

### VpTokenClaimPolicy&#x20;

Verify verifiable presentation by OIDC/SIOPv2 VP token claim, Argument: VpTokenClaim

### CredentialStatusPolicy&#x20;

Verify by credential status, Argument: None

## EBIS/ESSIF specific policies

### TrustedSchemaRegistryPolicy

Verify by EBSI Trusted Schema Registry.

### TrustedIssuerDidPolicy&#x20;

Verify by trusted issuer did.

### TrustedIssuerRegistryPolicy&#x20;

Verify by trusted EBSI Trusted Issuer Registry record.

### TrustedSubjectDidPolicy&#x20;

Verify by trusted subject did.

### IssuedDateBeforePolicy&#x20;

Verify by issuance date.



## GAIA-X specific policies

### GaiaxTrustedPolicy&#x20;

Verify Gaiax trusted fields, Argument: None

### GaiaxSDPolicy

Verify Gaiax SD fields, Argument: None

