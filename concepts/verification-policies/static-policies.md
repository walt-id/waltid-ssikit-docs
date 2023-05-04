# Static Policies

## General policies

### SignaturePolicy

Verifies the signature of the W3C Verifiable credential.

Argument: _None_.

### JsonSchemaPolicy

Verifies against the associated JSON schema. Note that the attribute _credentialSchema_ must be set and the JSON schema must be accessible by the http URL.

Argument: _None_.

### ValidFromBeforePolicy

Verify by valid from.

Argument: _None_.

### ExpirationDateAfterPolicy

Verify by expiration date.

Argument: _None_.

### ChallengePolicy

Verify challenge.

Argument: `ChallengePolicyArg`

### VpTokenClaimPolicy

Verify verifiable presentation by OIDC/SIOPv2 VP token claim.

Argument: `VpTokenClaim`

### CredentialStatusPolicy

Verify by credential status.

Argument: _None_.

## EBIS/ESSIF specific policies

### EbsiTrustedSchemaRegistryPolicy

Verify by EBSI Trusted Schema Registry.

Argument: _None_.

The following checks are performed:

* credential schema id has the correct format

### EbsiTrustedIssuerDidPolicy

Verify by trusted issuer did.

Argument: _None_.

The following checks are performed:

* issuer did is resolvable against EBSI

### EbsiTrustedIssuerRegistryPolicy

Verify by EBSI Trusted Issuer Registry record.

Argument: `EbsiTrustedIssuerRegistryPolicyArg`.

The following checks are performed:

1. issuer has any record on trusted registry having an authorization claim matching the VC schema
2. issuer's TIR record contains a VerifiableId credential
3. the authorized claim record (from p.1) has the type provided as argument to the policy
4. issuer's accreditation is valid - verifies against `EbsiTrustedIssuerAccreditationPolicy`

### EbsiTrustedSubjectDidPolicy

Verify by trusted subject did.

Argument: _None_.

The following checks are performed:

* subject did is resolvable against EBSI

### EbsiTrustedIssuerAccreditationPolicy

Verify by issuer's authorized claims.

Argument: _None_.

Performs the following actions:

1. fetches the attribute specified by the `termsOfUse` property
2. checks whether the credential stored as the attribute body has the required accreditation claims to match the current VC schema

### IssuedDateBeforePolicy

Verify by issuance date.

Argument: _None_.

## GAIA-X specific policies

### GaiaxTrustedPolicy

Verify Gaiax trusted fields.

Argument: _None_.

### GaiaxSDPolicy

Verify Gaiax SD fields.

Argument: _None_.

