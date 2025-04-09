---
noIndex: true
---

# Static Policies

Static verification policies are predefined for verifying credentials in standard use cases. The following lists out supported static policies by SSI-Kit along with their arguments

## General policies

| Name                      | Description                                                                                                                                               | Argument                                                                   |
| ------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------- |
| SignaturePolicy           | Verifies the signature of the W3C Verifiable credential.                                                                                                  | None                                                                       |
| JsonSchemaPolicy          | Verifies against the associated JSON schema. Note that the attribute credentialSchema must be set and the JSON schema must be accessible by the http URL. | None                                                                       |
| ValidFromBeforePolicy     | Verifies the credentials based on their valid-from date                                                                                                   | None                                                                       |
| ExpirationDateAfterPolicy | Verifies the credentials based on their expiration date                                                                                                   | None                                                                       |
| ChallengePolicy           | Verifies challenge                                                                                                                                        | `ChallengePolicyArg`, which contains specific challenges to check against. |
| VpTokenClaimPolicy        | Verify verifiable presentation by OIDC/SIOPv2 VP token claim.                                                                                             | `VpTokenClaim`                                                             |
| CredentialStatusPolicy    | Verifies credentials based on their status                                                                                                                | None                                                                       |

## EBIS/ESSIF Specific Policies

<table><thead><tr><th width="337">Name</th><th width="287.3333333333333">Description</th><th>Argument</th></tr></thead><tbody><tr><td>EbsiTrustedSchemaRegistryPolicy</td><td><p>Verify by EBSI Trusted Schema Registry.<br><br><em>Checks performed:</em> </p><ul><li>credential schema id has the correct format</li></ul></td><td>None</td></tr><tr><td>EbsiTrustedIssuerDidPolicy</td><td><p>Verify by trusted issuer did.<br><br>Checks performed: </p><ul><li>issuer did is resolvable against EBSI</li></ul></td><td>None</td></tr><tr><td>EbsiTrustedIssuerRegistryPolicy</td><td><p>Verify by EBSI Trusted Issuer Registry record.<br><br>Checks performed:</p><ul><li>issuer has any record on trusted registry having an authorization claim matching the VC schema</li></ul><ul><li>issuer's TIR record contains a VerifiableId credential</li></ul><ul><li>the authorized claim record (from p.1) has the type provided as argument to the policy</li></ul><ul><li>issuer's accreditation is valid - verifies against <code>EbsiTrustedIssuerAccreditationPolicy</code></li></ul></td><td><code>EbsiTrustedIssuerRegistryPolicyArg</code></td></tr><tr><td>EbsiTrustedSubjectDidPolicy</td><td><p>Verify by trusted subject did.<br><br>Checks performed:</p><ul><li>subject did is resolvable against EBSI</li></ul></td><td>None</td></tr><tr><td>EbsiTrustedIssuerAccreditationPolicy</td><td><p>Verify by issuer's authorized claims.<br><br>Checks performed: </p><ul><li>fetches the attribute specified by the <code>termsOfUse</code> property</li></ul><ul><li>checks whether the credential stored as the attribute body has the required accreditation claims to match the current VC schema</li></ul></td><td>None</td></tr><tr><td>IssuedDateBeforePolicy</td><td>Verify by issuance date.</td><td>None</td></tr></tbody></table>



## GAIA-X specific policies

| Name               | Description                  | Argument |
| ------------------ | ---------------------------- | -------- |
| GaiaxTrustedPolicy | Verify Gaiax trusted fields. | None     |
| GaiaxSDPolicy      | Verify Gaiax SD fields.      | None     |
