# Apply multiple sites
```
// comand to apply multiple sites:
Add to firebase json and make hosting to array or simply add target to object: 

    {
        "hosting": [
            {
                target: "resource-name",
                "public": "public",
                "ignore": [
                    "firebase.json",
                    "**/.*",
                    "**/node_modules/**"
                ]
            }
        ]
    }

firebase target:apply hosting alias resource-name
```