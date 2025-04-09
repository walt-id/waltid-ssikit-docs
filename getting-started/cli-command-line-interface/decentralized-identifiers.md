---
noIndex: true
---

# Decentralized Identifiers

DID related operations, like registering, updating and deactivating DIDs. For more info on DIDs, go [here](../../ssi-kit/ssi-kit/what-is-ssi/technologies-and-concepts/decentralised-identifiers-dids.md).

Commands:

* [Create DID](decentralized-identifiers.md#create-did) - using **create** command.
* [Resolve DID](decentralized-identifiers.md#resolve-did) - using **resolve** command.
* [List DIDs](decentralized-identifiers.md#list-dids) - using **list** command.
* [Import DID](decentralized-identifiers.md#import-did) to custodian store - using **import** command.
* [Delete DID](decentralized-identifiers.md#delete-did) from custodian - using **delete** command.

All commands have the help option available:

* `<your-command> -h`
* `<your-command> --help`

E.g. `did create -h`

![Create did help command output](../../.gitbook/assets/did-create-help-menu.png)

### Create DID

Creates a DID document using `did create [options]` command based on the corresponding SSI ecosystem (DID method). Optionally the associated asymmetric key is also created.

#### Options

* `-m, --did-method [key | web | ebsi | iota | jwk | cheqd]` - Specify DID method \[key], Supported DID methods are: "key", "web", "ebsi", "iota", "jwk"
* `-k, --key TEXT` - Specific key (ID or alias)
* `-d, --domain TEXT` - Domain for did:web
* `-p, --path TEXT` - Path for did:web
* `-v, --version INT` - Version of did:ebsi. Allowed values: 1 (default), 2
* `-n, --network [testnet | mainnet]` - cheqd network, default is `testnet`
* `-j, --useJwkJcsPub` - specifies whether to create a did:key using the jwk\_jcs-pub multicodec (code: [0xeb51](https://github.com/multiformats/multicodec/blob/master/table.csv#L516))

The returned value represents the DID document.

E.g. `did create -m ebsi -k 8a2c3628acdd45999b4c0b5a69911437`

![](<../../.gitbook/assets/Capture (2).PNG>)

{% hint style="info" %}
**IOTA support**

For creating IOTA DIDs and registering them on the IOTA tangle, a wrapper library needs to be installed and available in the local library path.

The wrapper library is included in the SSIKit Docker image, such that for Docker users no additional setup is required.

CLI users can find instructions for build and SSIKit integration at:

[https://github.com/walt-id/waltid-iota-identity-wrapper](https://github.com/walt-id/waltid-iota-identity-wrapper)
{% endhint %}

### Resolve DID

Resolves the DID document.

Options:

-d, --did TEXT DID to be resolved

-r, --raw / -t, --typed

-w, --write

### List DIDs

List all created DIDs using `did list` command

![List dids command output](<../../.gitbook/assets/image (4).png>)

### Import DID

Import DID to custodian store using `did import [options]` command

#### Options

* `-k, --key-id TEXT` - Specify key ID for imported did, if left empty, only public key will be imported
* `-f, --file TEXT` - Load the DID document from the given file
* `-d, --did TEXT` - Try to resolve DID document for the given DID

### Delete DID

Use the `delete` command to delete a DID:

* `did delete <your did>`

E.g. `did delete -d "did:ebsi:zs79GYJvzEnQYxkAAj4UX1j"`

![](<../../.gitbook/assets/image (14) (1).png>)
