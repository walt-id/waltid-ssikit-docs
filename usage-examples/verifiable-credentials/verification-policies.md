# Verification Policies

For verification of verifiable credentials, the SSIKit provides several predefined, static verification policies. Additionally, it provides a way to create custom policies dynamically, using a policy execution engine, such as **Open Policy Agent**.

To list the available verification policies and their descriptions, run:

```
ssikit vc policies list
```

The output will show the available policies, where static, predefined policies are indicated by the leading `-`, whereas dynamically created policies are indicated by `*`:

```
ssikit vc policies list
walt.id SSI Kit 1.11.0-SNAPSHOT (running on Java 16.0.2+7-suse-lp153.30.15-x8664)

- SignaturePolicy       Verify by signature,    Argument: None
- JsonSchemaPolicy       Verify by JSON schema,  Argument: None
- TrustedSchemaRegistryPolicy    Verify by EBSI Trusted Schema Registry,         Argument: None
- TrustedIssuerDidPolicy         Verify by trusted issuer did,   Argument: None
- TrustedIssuerRegistryPolicy    Verify by trusted EBSI Trusted Issuer Registry record,  Argument: None
- TrustedSubjectDidPolicy        Verify by trusted subject did,  Argument: None
- IssuedDateBeforePolicy         Verify by issuance date,        Argument: None
- ValidFromBeforePolicy  Verify by valid from,   Argument: None
- ExpirationDateAfterPolicy      Verify by expiration date,      Argument: None
- GaiaxTrustedPolicy     Verify Gaiax trusted fields,    Argument: None
- GaiaxSDPolicy  Verify Gaiax SD fields,         Argument: None
- ChallengePolicy        Verify challenge,       Argument: ChallengePolicyArg
- VpTokenClaimPolicy     Verify verifiable presentation by OIDC/SIOPv2 VP token claim,   Argument: VpTokenClaim
- CredentialStatusPolicy         Verify by credential status,    Argument: None
- DynamicPolicy  Verify credential by rego policy,       Argument: DynamicPolicyArg
- VerifiableMandatePolicy        Predefined policy for verifiable mandates,      Argument: JsonObject
* GaiaXPolicy    - no description -,     Argument: JsonObject
* ItsMePolicy    Check that credential is mine,  Argument: JsonObject

(*) ... mutable dynamic policy
```

