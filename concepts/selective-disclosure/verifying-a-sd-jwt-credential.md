---
description: >-
  Verifier requests, holder shares selective disclosures, verifier verifies
  hashes and signature.
---

# Verifying a SD-JWT Credential

### SD-JWT Credential Verification Process

1. **Selective Disclosure Sharing**: During the verification process, the verifier asked for a certain set of claims. The selective disclosure sharing mechanism allows the holder then to only share does require claims through sending the whole SD-JWT plus the disclosures which are needed for verification. This process therefore helps with privacy by not revealing more identity information than what's specifically requested.
2. **Disclosure Verification**: The verifier, upon receiving the shared disclosures and the SD-JWT, can confirm that the shared disclosures are a part of the SD-JWT. This is done by hashing the received disclosures in the same manner as the issuer did during [the issuance process](issuing-a-sd-jwt-credential.md).
3. **Hash Comparison and Tamper Check**: The verifier then compares the hashed values of the shared disclosures with the values present in the SD-JWT. If the hashed values match, the verifier can be confident that the shared values haven't been tampered with and are actually part of the SD-JWT.
4. **Transfer Format**: Transferring the credential from holder to verifier happens through the sharing of the SD-JWT with the concatenated disclosures which were chosen to be revealed using the \~ sign. An example of this format would be:

{% code overflow="wrap" %}
```
eyJraWQiOiI5MmJlMTAzYjRkZmY0OGYxYmE5ODc4ZGQyNmZhZjcxZSIsImN0eSI6ImNyZWRlbnRpYWwtY2xhaW1zLXNldCtqc29uIiwidHlwIjoidmMrc2Qtand0IiwiYWxnIjoiRWREU0EifQ.eyJjcmVkZW50aWFsU2NoZW1hIjp7ImlkIjoiaHR0cHM6Ly9yYXcuZ2l0aHVidXNlcmNvbnRlbnQuY29tL3dhbHQtaWQvd2FsdGlkLXNzaWtpdC12Y2xpYi9tYXN0ZXIvc3JjL3Rlc3QvcmVzb3VyY2VzL3NjaGVtYXMvVmVyaWZpYWJsZUlkLmpzb24iLCJ0eXBlIjoiRnVsbEpzb25TY2hlbWFWYWxpZGF0b3IyMDIxIn0sImV2aWRlbmNlIjpbeyJkb2N1bWVudFByZXNlbmNlIjpbIlBoeXNpY2FsIl0sInZlcmlmaWVyIjoiZGlkOmVic2k6MkE5Qlo5U1VlNkJhdGFjU3B2czFWNUNkakh2THBRN2JFc2kySmI2TGRIS25ReGFOIiwiZXZpZGVuY2VEb2N1bWVudCI6WyJQYXNzcG9ydCJdLCJ0eXBlIjpbIkRvY3VtZW50VmVyaWZpY2F0aW9uIl0sInN1YmplY3RQcmVzZW5jZSI6IlBoeXNpY2FsIn1dLCJpc3N1YW5jZURhdGUiOiIyMDIxLTA4LTMxVDAwOjAwOjAwWiIsImNyZWRlbnRpYWxTdWJqZWN0Ijp7InBlcnNvbmFsSWRlbnRpZmllciI6IjA5MDQwMDgwODRIIiwiZmlyc3ROYW1lIjoiSmFuZSIsIl9zZCI6WyJuNWRYOEVpTUNoQ1hBR0o3elZCM1duQjc4Y3lBVFp3T1hwVkpCTUdOUzhzIiwiemFxMTNsa2lHLTd2am90SFppM0psSmhwS2JtUjFTVnV6Q3pLYVZYOUZRUSIsInhyYjdTOFZsNlctb0dMaVVQcTVlMmplVFpKVk5mYmRtNW9KNjd0VlVQem8iLCJwT0Jmb3hmQndqQUNPbXZ4aTNUSTc0RDN4Y2FwZS1RWVlGeUNPZEpPel9VIiwiRm1ZcmFmbWotUW9lbE1sSkQtVTN2OVgwS3hXTkZwelhwRl9McVc2dkZ0byJdLCJwbGFjZU9mQmlydGgiOiJMSUxMRSwgRlJBTkNFIiwiZ2VuZGVyIjoiRkVNQUxFIiwiZmFtaWx5TmFtZSI6IkRPRSIsImlkIjoiZGlkOmVic2k6MkFFTUFxWFdLWU11MUpIUEFnR2NnYTRkeHU3VGhnZmdOOTVWeUpCSkdaYlNKVXRwIiwibmFtZUFuZEZhbWlseU5hbWVBdEJpcnRoIjoiSmFuZSBET0UiLCJjdXJyZW50QWRkcmVzcyI6WyIxIEJvdWxldmFyZCBkZSBsYSBMaWJlcnTDqSwgNTk4MDAgTGlsbGUiXX0sIl9zZF9hbGciOiJzaGEtMjU2IiwiaWQiOiJ1cm46dXVpZDozYWRkOTRmNC0yOGVjLTQyYTEtODcwNC00ZTRhYTUxMDA2YjQiLCJ2YWxpZEZyb20iOiIyMDIxLTA4LTMxVDAwOjAwOjAwWiIsInR5cGUiOlsiVmVyaWZpYWJsZUNyZWRlbnRpYWwiLCJWZXJpZmlhYmxlQXR0ZXN0YXRpb24iLCJWZXJpZmlhYmxlSWQiXSwiaXNzdWVkIjoiMjAyMS0wOC0zMVQwMDowMDowMFoiLCJAY29udGV4dCI6WyJodHRwczovL3d3dy53My5vcmcvMjAxOC9jcmVkZW50aWFscy92MSJdLCJpc3N1ZXIiOiJkaWQ6ZWJzaToyQTlCWjlTVWU2QmF0YWNTcHZzMVY1Q2RqSHZMcFE3YkVzaTJKYjZMZEhLblF4YU4ifQ.5TZ1n6iDHtW3lnKA_7ofSQ-BWyvEr39LThGdIc1OMgUejG6JF6blGkTqcoaQABQJKq6pFgkhjrYcpDG8QcObDA~
WyJXeS11VjJDa216SmJ4NGtjeTJQWjF3IiwiZGF0ZU9mQmlydGgiLCIxOTkzLTA0LTA4Il0~WyJXeS11VjJDa216SmJ4NGtjeTJQWjF3IiwiZGF0ZU9mQmlydGgiLCIxOTkzLTA0LTA4Il0

```
{% endcode %}

### Verification in Action

Using either the CLI, Kotlin or REST option, you can start verifying your SD-JWT credential.



{% tabs %}
{% tab title="CLI" %}
### &#x20;**Creating a SD-JWT Credential Presentation**

\
We create a presentation to provide the verifier with the holder's credentials for verification. The presentation can include data from multiple credentials, making verification easier as only one interaction is required. We provide the holder DID and the disclosures to create a presentation, which we can then present to a verifier, via the present command.\
\
**Example Command**

```bash
ssikit vc present \
-i did:key:z6MktopRgCooC5LbjRUs6b6Yh7R5mNFTEmyLmSYZQd5Lm14a \
-c 234235 \
--sd credentialSubject \
--sd credentialSubject.dateOfBirth \
vc.txt

```

**Options:**

* `-i, --holder-did`**:** DID of the holder (owner of the VC)
* `-c, --challange`: Challenge to be used in the LD proof
* `--sd, --selective-disclosure`: Path to selectively disclosed fields, in a simplified JsonPath format. Can be specified multiple times. By default NONE of the sd fields are disclosed, for multiple credentials, the path can be prefixed with the index of the presented credential, e.g. "credentialSubject.familyName", "0.credentialSubject.familyName", "1.credentialSubject.dateOfBirth".\
  \
  other options
* `--sd-all-for`: Selects all selective disclosures for the credential at the specified index to be disclosed. Overrides --sd flags!
* `--sd-all`: Selects all selective disclosures for all presented credentials to be disclosed.

**Example Response**

{% code overflow="wrap" %}
```
eyJraWQiOiJkaWQ6a2V5Ono2TWt0b3BSZ0Nvb0M1TGJqUlVzNmI2WWg3UjVtTkZURW15TG1TWVpRZDVMbTE0YSN6Nk1rdG9wUmdDb29DNUxialJVczZiNlloN1I1bU5GVEVteUxtU1laUWQ1TG0xNGEiLCJ0eXAiOiJKV1QiLCJhbGciOiJFZERTQSJ9.eyJzdWIiOiJkaWQ6a2V5Ono2TWt0b3BSZ0Nvb0M1TGJqUlVzNmI2WWg3UjVtTkZURW15TG1TWVpRZDVMbTE0YSIsIm5iZiI6MTY4NjY1NjQxMSwiaXNzIjoiZGlkOmtleTp6Nk1rdG9wUmdDb29DNUxialJVczZiNlloN1I1bU5GVEVteUxtU1laUWQ1TG0xNGEiLCJ2cCI6eyJ0eXBlIjpbIlZlcmlmaWFibGVQcmVzZW50YXRpb24iXSwiQGNvbnRleHQiOlsiaHR0cHM6Ly93d3cudzMub3JnLzIwMTgvY3JlZGVudGlhbHMvdjEiXSwiaWQiOiJ1cm46dXVpZDo1MzQ0YWZmMi0wN2ZiLTRiZTktYmM3Yi0xZjFlZWM1NTNhMDUiLCJob2xkZXIiOiJkaWQ6a2V5Ono2TWt0b3BSZ0Nvb0M1TGJqUlVzNmI2WWg3UjVtTkZURW15TG1TWVpRZDVMbTE0YSIsInZlcmlmaWFibGVDcmVkZW50aWFsIjpbImV5SnJhV1FpT2lKa2FXUTZhMlY1T25vMlRXdDBiM0JTWjBOdmIwTTFUR0pxVWxWek5tSTJXV2czVWpWdFRrWlVSVzE1VEcxVFdWcFJaRFZNYlRFMFlTTjZOazFyZEc5d1VtZERiMjlETlV4aWFsSlZjelppTmxsb04xSTFiVTVHVkVWdGVVeHRVMWxhVVdRMVRHMHhOR0VpTENKMGVYQWlPaUpLVjFRaUxDSmhiR2NpT2lKRlpFUlRRU0o5LmV5SnpkV0lpT2lKa2FXUTZhMlY1T25vMlRXdDBiM0JTWjBOdmIwTTFUR0pxVWxWek5tSTJXV2czVWpWdFRrWlVSVzE1VEcxVFdWcFJaRFZNYlRFMFlTSXNJbTVpWmlJNk1UWTROalkxTmpNMU1Td2lhWE56SWpvaVpHbGtPbXRsZVRwNk5rMXJkRzl3VW1kRGIyOUROVXhpYWxKVmN6WmlObGxvTjFJMWJVNUdWRVZ0ZVV4dFUxbGFVV1ExVEcweE5HRWlMQ0pwWVhRaU9qRTJPRFkyTlRZek5URXNJblpqSWpwN0luUjVjR1VpT2xzaVZtVnlhV1pwWVdKc1pVTnlaV1JsYm5ScFlXd2lMQ0pXWlhKcFptbGhZbXhsUVhSMFpYTjBZWFJwYjI0aUxDSldaWEpwWm1saFlteGxTV1FpWFN3aVFHTnZiblJsZUhRaU9sc2lhSFIwY0hNNkx5OTNkM2N1ZHpNdWIzSm5Mekl3TVRndlkzSmxaR1Z1ZEdsaGJITXZkakVpWFN3aWFXUWlPaUoxY200NmRYVnBaRG94TW1GaE5qUmpZeTAyTnpnekxUUTJZV0l0T0dWaU1TMWlPV1UyTkRkaVpHVTFOek1pTENKcGMzTjFaWElpT2lKa2FXUTZhMlY1T25vMlRXdDBiM0JTWjBOdmIwTTFUR0pxVWxWek5tSTJXV2czVWpWdFRrWlVSVzE1VEcxVFdWcFJaRFZNYlRFMFlTSXNJbWx6YzNWaGJtTmxSR0YwWlNJNklqSXdNak10TURZdE1UTlVNVEU2TXprNk1URmFJaXdpYVhOemRXVmtJam9pTWpBeU15MHdOaTB4TTFReE1Ub3pPVG94TVZvaUxDSjJZV3hwWkVaeWIyMGlPaUl5TURJekxUQTJMVEV6VkRFeE9qTTVPakV4V2lJc0ltTnlaV1JsYm5ScFlXeFRZMmhsYldFaU9uc2lhV1FpT2lKb2RIUndjem92TDNKaGR5NW5hWFJvZFdKMWMyVnlZMjl1ZEdWdWRDNWpiMjB2ZDJGc2RDMXBaQzkzWVd4MGFXUXRjM05wYTJsMExYWmpiR2xpTDIxaGMzUmxjaTl6Y21NdmRHVnpkQzl5WlhOdmRYSmpaWE12YzJOb1pXMWhjeTlXWlhKcFptbGhZbXhsU1dRdWFuTnZiaUlzSW5SNWNHVWlPaUpHZFd4c1NuTnZibE5qYUdWdFlWWmhiR2xrWVhSdmNqSXdNakVpZlN3aVpYWnBaR1Z1WTJVaU9sdDdJbVJ2WTNWdFpXNTBVSEpsYzJWdVkyVWlPbHNpVUdoNWMybGpZV3dpWFN3aVpYWnBaR1Z1WTJWRWIyTjFiV1Z1ZENJNld5SlFZWE56Y0c5eWRDSmRMQ0p6ZFdKcVpXTjBVSEpsYzJWdVkyVWlPaUpRYUhsemFXTmhiQ0lzSW5SNWNHVWlPbHNpUkc5amRXMWxiblJXWlhKcFptbGpZWFJwYjI0aVhTd2lkbVZ5YVdacFpYSWlPaUprYVdRNlpXSnphVG95UVRsQ1dqbFRWV1UyUW1GMFlXTlRjSFp6TVZZMVEyUnFTSFpNY0ZFM1lrVnphVEpLWWpaTVpFaExibEY0WVU0aWZWMHNJbDl6WkNJNld5SlFjWFI1UmpaWU4yVTJWVGR5UkU0d2JsTkJYMXBpVEZOTk5VNDVlVXcxYkZOUVlYWXdNa05NZUVaVklsMTlMQ0pxZEdraU9pSjFjbTQ2ZFhWcFpEb3hNbUZoTmpSall5MDJOemd6TFRRMllXSXRPR1ZpTVMxaU9XVTJORGRpWkdVMU56TWlmUS4wb2QxNFI5ckxsejBuaFJSY19HU3RxZ1g4eE5YSjk4Y3JsdWRiYmN5UUFMdUJyRC1CNnZwS2kzbzlBWmIwNGpOZ0FWanp1SVhKWUYweUpNOWdLLVlCUX5XeUpqUTBKbFZDMTVlV05HVUVjeWEyeDFia0V3T0Zobklpd2laR0YwWlU5bVFtbHlkR2dpTENJd0lsMH5XeUl6TTBOcWJYaDNibkZQTkY5WFVtWnZOMGxUV1ZWUklpd2lZM0psWkdWdWRHbGhiRk4xWW1wbFkzUWlMSHNpYVdRaU9pSmthV1E2YTJWNU9ubzJUV3QwYjNCU1owTnZiME0xVEdKcVVsVnpObUkyV1dnM1VqVnRUa1pVUlcxNVRHMVRXVnBSWkRWTWJURTBZU0lzSW1OMWNuSmxiblJCWkdSeVpYTnpJanBiSWxacFpXNXVZU0pkTENKbVlXMXBiSGxPWVcxbElqb2lRbUYxYldGdWJpSXNJbVpwY25OMFRtRnRaU0k2SWxSaGJXbHVieUlzSW1kbGJtUmxjaUk2SWsxaGJHVWlMQ0p1WVcxbFFXNWtSbUZ0YVd4NVRtRnRaVUYwUW1seWRHZ2lPaUpLWVc1bElFUlBSU0lzSW5CbGNuTnZibUZzU1dSbGJuUnBabWxsY2lJNklqQTVNRFF3TURnd09EUklJaXdpY0d4aFkyVlBaa0pwY25Sb0lqb2lUWFZ1YVdOb0lpd2lYM05rSWpwYklrSlNaWGczVFRSaWMxcHdTVEJCY0V4cVpFUjNRM05KTFd0MVJWZDJNbFpPYVdGVk5VMDVaR0ZzTkRnaVhYMWR-Il19LCJpYXQiOjE2ODY2NTY0MTEsIm5vbmNlIjoiMjM0MjM1IiwianRpIjoidXJuOnV1aWQ6NTM0NGFmZjItMDdmYi00YmU5LWJjN2ItMWYxZWVjNTUzYTA1In0.bLCEF-1BoXn2IKx53MJ27JxBk3bI_waDEk4Gb6qZycmHxx0UqzQt3zfUdGcRadrmOUtnoDKc9pgJOAz4NJFzBQ
```
{% endcode %}



**Parseing the presentation to JSON**

Using the parse command, you can print the presenation as a JSON object.

```
ssikit vc parse -r -c ata/vc/presented/vp-1686656411530.json
```

**Options:**

* `-r`: Recursively parse credentials in presentation
* `-c`: Credential content or file path

### &#x20;**Verifying SD-JWT Presentation**

We can check the validity of the presentation by providing the verify command with it. Use the storage location printed at the end of the last command.

**Example Command**

```bash
ssikit vc verify data/vc/presented/vp-1686656411530.json
```

\
**Example Output**

```bash
Results:

SignaturePolicy:	 passed
Verified:		 true
```
{% endtab %}

{% tab title="REST" %}
coming soon
{% endtab %}
{% endtabs %}

### Demo

{% embed url="https://youtu.be/fo5JxPszCqY?t=358" %}
