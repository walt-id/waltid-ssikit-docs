---
description: Install and run the Open Policy Engine (OPA) on your local machine
---

# Setup

### Installation

1. Download the Open Policy Agent as described [here](https://www.openpolicyagent.org/docs/latest/#1-download-opa).
2. Set the permissions of the downloaded file to allow execution:

```bash
chmod 755 ./opa
```

### Path Configuration

1. Move the downloaded executable to a location in your system's PATH to make it accessible from any directory. A common location for custom binaries on macOS is \~/.local/bin. You can move it there with the following command:

```bash
mv opa ~/.local/bin/opa
```

### Verify Setup

1. Test the setup by running a simple expression with OPA:

```bash
opa eval "1*2+3"
```

2. If everything is working correctly, you should see output like this:

```json
{
   "result": [
      {
         "expressions": [
            {
               "value": 5,
               "text": "1*2+3",
               "location": {
                  "row": 1,
                  "col": 1
               }
            }
         ]
      }
   ]
}
```

\
Next Steps
----------

1. Creating a dynamic policy
2. Verifying a verifiable credential using a dynamic policy
