# did:key

Specification [https://w3c-ccg.github.io/did-method-key/](https://w3c-ccg.github.io/did-method-key/)

```
./ssikit.sh did create -m key

Creating did:key (key: fc3ed411f141446aa7ff30b2b8f31e71)

Results:

DID created: did:key:z6MkhH5XtZAXwqs4kbGWyL7pTev1EWtjGgQTiXFtsPCMVHW3

DID document (below, JSON):

{
    "assertionMethod" : [
        "did:key:z6MkhH5XtZAXwqs4kbGWyL7pTev1EWtjGgQTiXFtsPCMVHW3#z6MkhH5XtZAXwqs4kbGWyL7pTev1EWtjGgQTiXFtsPCMVHW3"
    ],
    "authentication" : [
        "did:key:z6MkhH5XtZAXwqs4kbGWyL7pTev1EWtjGgQTiXFtsPCMVHW3#z6MkhH5XtZAXwqs4kbGWyL7pTev1EWtjGgQTiXFtsPCMVHW3"
    ],
    "capabilityDelegation" : [
        "did:key:z6MkhH5XtZAXwqs4kbGWyL7pTev1EWtjGgQTiXFtsPCMVHW3#z6MkhH5XtZAXwqs4kbGWyL7pTev1EWtjGgQTiXFtsPCMVHW3"
    ],
    "capabilityInvocation" : [
        "did:key:z6MkhH5XtZAXwqs4kbGWyL7pTev1EWtjGgQTiXFtsPCMVHW3#z6MkhH5XtZAXwqs4kbGWyL7pTev1EWtjGgQTiXFtsPCMVHW3"
    ],
    "@context" : "https://www.w3.org/ns/did/v1",
    "id" : "did:key:z6MkhH5XtZAXwqs4kbGWyL7pTev1EWtjGgQTiXFtsPCMVHW3",
    "keyAgreement" : [
        "did:key:z6MkhH5XtZAXwqs4kbGWyL7pTev1EWtjGgQTiXFtsPCMVHW3#z6LSfpgN3sMHc1drweSsDCLb9uxDrsbyBb7CtjDhpCxraf4w"
    ],
    "verificationMethod" : [
        {
            "controller" : "did:key:z6MkhH5XtZAXwqs4kbGWyL7pTev1EWtjGgQTiXFtsPCMVHW3",
            "id" : "did:key:z6MkhH5XtZAXwqs4kbGWyL7pTev1EWtjGgQTiXFtsPCMVHW3#z6MkhH5XtZAXwqs4kbGWyL7pTev1EWtjGgQTiXFtsPCMVHW3",
            "publicKeyBase58" : "3ppVJJv6cJNbe6RpHm9ycZN1QwcsroA72WLy37ELa4if",
            "type" : "Ed25519VerificationKey2019"
        },
        {
            "controller" : "did:key:z6MkhH5XtZAXwqs4kbGWyL7pTev1EWtjGgQTiXFtsPCMVHW3",
            "id" : "did:key:z6MkhH5XtZAXwqs4kbGWyL7pTev1EWtjGgQTiXFtsPCMVHW3#z6LSfpgN3sMHc1drweSsDCLb9uxDrsbyBb7CtjDhpCxraf4w",
            "publicKeyBase58" : "59WCXZYRWYv7rG56gYpdqKjk1j4rUyw41kW2KkKKsHJB",
            "type" : "X25519KeyAgreementKey2019"
        }
    ]
}

```
