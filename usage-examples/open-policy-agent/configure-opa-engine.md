# Configure OPA engine

Setting up the **Open Policy Agent** engine can be done following the steps:
1. install the **Open Policy Agent** engine:
   1. refer to [https://www.openpolicyagent.org/docs/#running-opa](https://www.openpolicyagent.org/docs/#running-opa)
   for more details on how to install **Open Policy Agent** engine
2. configure the engine:
   1. add the `opa` executable to your `PATH` variable
3. verify the setup is complete:
   1. running `opa eval "1*2+3"` from any location should output a result similar to:
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
   
Once the **OPA engine** setup is complete, it can be used with [dynamic policies](/concepts/verification-policies/dynamic-policies.md)
for credential verification.