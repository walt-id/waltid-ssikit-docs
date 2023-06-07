---
description: >-
  Learn about issuing SD-JWT credentials which includes hashing, creating
  disclosures and adding decoy hashes
---

# Issuing a SD-JWT Credential

### **SD-JWT Credential Issuance Process**

1. **Credential Creation**: The issuer first creates the credential, as usual.
2. **Conversion to SD-JWT Credential**: The issuer then transforms the credential into an SD-JWT. This is done by hashing all or only a subset of claims, adding decoy hashes, and preparing disclosures. At the end, the SD-JWT credential can contain plain-text claims next to disclosable ones.
3. **Claim Hashing**: The claim is transformed into a disclosure, which is a plain-text representations of the claim, by concatenating the attribute name and value, then prefixing it with a salt. The salt prevents attackers from guessing plain-text values via dictionary attacks. This is then converted to a base64 string, which will represent the disclosure. For example, the disclosure may look like this (salt + attribute name + value): `[ “dC12Y2xpYi9tYXN0ZXI”, “given_name”, “John” ]`. The disclosure is then put into a hash function, and the result gets included in the SD-JWT.&#x20;
4. **Adding Decoy Hashes:**  At this point, decoy hashes are also added to the SD-JWT. These decoy hashes are essentially dummy values that help conceal the actual number of claims a credential holds. By using decoy hashes, the issuer can prevent potential observers from determining how many claims are contained within the credential based on the number of hashes.
5. **SD-JWT Credential Transfer to Holder**: The issuer sends the SD-JWT and all disclosures to the holder. Because the holder now has the SD-JWT credential as well as all the disclosures, he can read the entire content of the credential. This allows the holder to decide which disclosures to send alongside the SD-JWT in a transaction with a verifier.
6. **Transfer Format**: On transfer, the SD-JWT is shared with the concatenated disclosures using the \~ sign. An example of this format would be:

<pre data-overflow="wrap"><code>eyJraWQiOiI5MmJlMTAzYjRkZmY0OGYxYmE5ODc4ZGQyNmZhZjcxZSIsImN0eSI6ImNyZWRlbnRpYWwtY2xhaW1zLXNldCtqc29uIiwidHlwIjoidmMrc2Qtand0IiwiYWxnIjoiRWREU0EifQ.eyJjcmVkZW50aWFsU2NoZW1hIjp7ImlkIjoiaHR0cHM6Ly9yYXcuZ2l0aHVidXNlcmNvbnRlbnQuY29tL3dhbHQtaWQvd2FsdGlkLXNzaWtpdC12Y2xpYi9tYXN0ZXIvc3JjL3Rlc3QvcmVzb3VyY2VzL3NjaGVtYXMvVmVyaWZpYWJsZUlkLmpzb24iLCJ0eXBlIjoiRnVsbEpzb25TY2hlbWFWYWxpZGF0b3IyMDIxIn0sImV2aWRlbmNlIjpbeyJkb2N1bWVudFByZXNlbmNlIjpbIlBoeXNpY2FsIl0sInZlcmlmaWVyIjoiZGlkOmVic2k6MkE5Qlo5U1VlNkJhdGFjU3B2czFWNUNkakh2THBRN2JFc2kySmI2TGRIS25ReGFOIiwiZXZpZGVuY2VEb2N1bWVudCI6WyJQYXNzcG9ydCJdLCJ0eXBlIjpbIkRvY3VtZW50VmVyaWZpY2F0aW9uIl0sInN1YmplY3RQcmVzZW5jZSI6IlBoeXNpY2FsIn1dLCJpc3N1YW5jZURhdGUiOiIyMDIxLTA4LTMxVDAwOjAwOjAwWiIsImNyZWRlbnRpYWxTdWJqZWN0Ijp7InBlcnNvbmFsSWRlbnRpZmllciI6IjA5MDQwMDgwODRIIiwiZmlyc3ROYW1lIjoiSmFuZSIsIl9zZCI6WyJuNWRYOEVpTUNoQ1hBR0o3elZCM1duQjc4Y3lBVFp3T1hwVkpCTUdOUzhzIiwiemFxMTNsa2lHLTd2am90SFppM0psSmhwS2JtUjFTVnV6Q3pLYVZYOUZRUSIsInhyYjdTOFZsNlctb0dMaVVQcTVlMmplVFpKVk5mYmRtNW9KNjd0VlVQem8iLCJwT0Jmb3hmQndqQUNPbXZ4aTNUSTc0RDN4Y2FwZS1RWVlGeUNPZEpPel9VIiwiRm1ZcmFmbWotUW9lbE1sSkQtVTN2OVgwS3hXTkZwelhwRl9McVc2dkZ0byJdLCJwbGFjZU9mQmlydGgiOiJMSUxMRSwgRlJBTkNFIiwiZ2VuZGVyIjoiRkVNQUxFIiwiZmFtaWx5TmFtZSI6IkRPRSIsImlkIjoiZGlkOmVic2k6MkFFTUFxWFdLWU11MUpIUEFnR2NnYTRkeHU3VGhnZmdOOTVWeUpCSkdaYlNKVXRwIiwibmFtZUFuZEZhbWlseU5hbWVBdEJpcnRoIjoiSmFuZSBET0UiLCJjdXJyZW50QWRkcmVzcyI6WyIxIEJvdWxldmFyZCBkZSBsYSBMaWJlcnTDqSwgNTk4MDAgTGlsbGUiXX0sIl9zZF9hbGciOiJzaGEtMjU2IiwiaWQiOiJ1cm46dXVpZDozYWRkOTRmNC0yOGVjLTQyYTEtODcwNC00ZTRhYTUxMDA2YjQiLCJ2YWxpZEZyb20iOiIyMDIxLTA4LTMxVDAwOjAwOjAwWiIsInR5cGUiOlsiVmVyaWZpYWJsZUNyZWRlbnRpYWwiLCJWZXJpZmlhYmxlQXR0ZXN0YXRpb24iLCJWZXJpZmlhYmxlSWQiXSwiaXNzdWVkIjoiMjAyMS0wOC0zMVQwMDowMDowMFoiLCJAY29udGV4dCI6WyJodHRwczovL3d3dy53My5vcmcvMjAxOC9jcmVkZW50aWFscy92MSJdLCJpc3N1ZXIiOiJkaWQ6ZWJzaToyQTlCWjlTVWU2QmF0YWNTcHZzMVY1Q2RqSHZMcFE3YkVzaTJKYjZMZEhLblF4YU4ifQ.5TZ1n6iDHtW3lnKA_7ofSQ-BWyvEr39LThGdIc1OMgUejG6JF6blGkTqcoaQABQJKq6pFgkhjrYcpDG8QcObDA~<a data-footnote-ref href="#user-content-fn-1">WyJXeS11VjJDa216SmJ4NGtjeTJQWjF3IiwiZGF0ZU9mQmlydGgiLCIxOTkzLTA0LTA4Il0</a>~<a data-footnote-ref href="#user-content-fn-2">WyJXeS11VjJDa216SmJ4NGtjeTJQWjF3IiwiZGF0ZU9mQmlydGgiLCIxOTkzLTA0LTA4Il0</a>

</code></pre>



### Issuance in Action

Using either the CLI, Kotlin or REST option, you can start issuing your SD-JWT credential.



...examples will be provided soon...



[^1]: 

[^2]: 
