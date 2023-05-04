# Rest API interface for _credentialStatus_

All the revocation related endpoints are located under the _revocations_ path:
`https://signatory.ssikit.walt.id/v1/revocations/`:
- [check](check-status.md) - check the verifiable credential revocation status
- [revoke](revoke.md) - revoke a verifiable credential

{% hint style="info" %}
_Check_ is a low level function. For a high level _check_, refer to
[CredentialStatusPolicy](/concepts/verification-policies/static-policies.md#CredentialStatusPolicy).
{% endhint %}

\
Refer to the [Issue with status](/concepts/credential-statuses/issue-with-status.md) section to learn about
how to issue a verifiable credential with a _credentialStatus_ property.