# did:web

Specification [https://w3c-ccg.github.io/did-method-web/](https://w3c-ccg.github.io/did-method-web/)

```
./ssikit.sh did create -m web --domain example.com --path /user/1234

Creating did:web (key: 10637d2f6e4144f4a5f61063b07016b6)

Results:

DID created: did:web:example.com::user:1234

DID document (below, JSON):

{
    "assertionMethod" : [
        "did:web:example.com::user:1234#10637d2f6e4144f4a5f61063b07016b6"
    ],
    "authentication" : [
        "did:web:example.com::user:1234#10637d2f6e4144f4a5f61063b07016b6"
    ],
    "@context" : "https://www.w3.org/ns/did/v1",
    "id" : "did:web:example.com::user:1234",
    "verificationMethod" : [
        {
            "controller" : "did:web:example.com::user:1234",
            "id" : "did:web:example.com::user:1234#10637d2f6e4144f4a5f61063b07016b6",
            "publicKeyJwk" : {
                "alg" : "EdDSA",
                "crv" : "Ed25519",
                "kid" : "10637d2f6e4144f4a5f61063b07016b6",
                "kty" : "OKP",
                "use" : "sig",
                "x" : "ys4NAC0bXx7WNFGL9BAKLYwweyV9CJXXrImhm5c0AFA"
            },
            "type" : "Ed25519VerificationKey2019"
        }
    ]
}

Install this did:web at: https://example.com/.well-known/user/1234/did.json

```

