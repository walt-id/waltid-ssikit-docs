---
noIndex: true
---

# Inspection

Velocity credential verification is available with the `verify` command:

```
./ssikit.sh velocity verify -h
```

![verify-cmd](assets/verify-cmd.png)

E.g. Verify credential.

```
./ssikit.sh velocity verify -i did:ion:1234567890 credential.jwt checks.json
```

{% tabs %}
{% tab title="credential-data" %}
```
eyJqd2siOnsia3R5IjoiRUMiLCJleHQiOnRydWUsImtleV9vcHMiOlsidmVyaWZ5Il0sIngiOiJVd3V5Y2lfMUJNa05DdVkwZ0lPWFZ3ZDZTOXBPMldOUWpsdUVXbWd3TGNBIiwieSI6Ik5vYlp6WFh1VUtNQmIwU1ZpaGo2cG10RWY2cXd4Y1FwSHlOMmRwSHBjM1kiLCJjcnYiOiJQLTI1NiJ9LCJhbGciOiJFUzI1NiIsInR5cCI6IkpXVCJ9.eyJ2YyI6eyJAY29udGV4dCI6WyJodHRwczovL3d3dy53My5vcmcvMjAxOC9jcmVkZW50aWFscy92MSJdLCJpZCI6Ijc1NmZlMWIzLWYwOGEtNDgxYy05ZWFlLTU2ZWIwMGI2NWQ1NyIsInR5cGUiOlsiSWREb2N1bWVudCIsIlZlcmlmaWFibGVDcmVkZW50aWFsIl0sImNyZWRlbnRpYWxTdWJqZWN0Ijp7ImZpcnN0TmFtZSI6eyJsb2NhbGl6ZWQiOnsiZW4iOiJBZGFtIn19LCJsYXN0TmFtZSI6eyJsb2NhbGl6ZWQiOnsiZW4iOiJTbWl0aCJ9fSwia2luZCI6IkRyaXZlcnNMaWNlbnNlIiwiYXV0aG9yaXR5Ijp7ImxvY2FsaXplZCI6eyJlbiI6IkNhbGlmb3JuaWEgRE1WIn19LCJsb2NhdGlvbiI6eyJjb3VudHJ5Q29kZSI6IlVTIiwicmVnaW9uQ29kZSI6IkNBIn0sImRvYiI6eyJkYXkiOjIwLCJtb250aCI6NiwieWVhciI6MTk2Nn0sImlkZW50aXR5TnVtYmVyIjoiMTIzMTAzMTIzMTIiLCJkZWZhdWx0Ijp0cnVlfX0sInN1YiI6ImFkYW0uc21pdGhAZXhhbXBsZS5jb20iLCJhdWQiOiIgIiwiaXNzIjoiNzU2ZmUxYjMtZjA4YS00ODFjLTllYWUtNTZlYjAwYjY1ZDU3IiwianRpIjoiNzU2ZmUxYjMtZjA4YS00ODFjLTllYWUtNTZlYjAwYjY1ZDU3IiwiaWF0IjoxNjIwMTI4NjgyLCJuYmYiOjE2MjAxMjg2ODJ9.iqbGO5LfYzUmvesVSCquWHekbC-z3VCvls156zsNnmvz7y6sFtcH7lH0IkRNwljGQQvsce50O7RG06QOSnMS4g
```
{% endtab %}

{% tab title="check-data" %}
```
{
    "TRUSTED_ISSUER": "SELF_SIGNED",
    "UNREVOKED": "PASS",
    "UNEXPIRED": "NOT_APPLICABLE",
    "UNTAMPERED": "PASS"
}
```
{% endtab %}

{% tab title="response" %}
```
Verification result:
true
{
    "TRUSTED_ISSUER": "SELF_SIGNED",
    "UNREVOKED": "PASS",
    "UNEXPIRED": "NOT_APPLICABLE",
    "UNTAMPERED": "PASS"
}
```
{% endtab %}
{% endtabs %}
