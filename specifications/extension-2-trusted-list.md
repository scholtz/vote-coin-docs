# Extension 2 - Trusted list



The trusted list is implementation extension which allows to calculate the results according to the trusted list specified by the questionaree.

If the voting system implementation does not implement trusted list extension, it should clearly state that the results are calculated only in the form 1 token = 1 vote.

The blockchain message MUST be self signed message, with amount 705 of basic tokens with specific note structure described below.

TL configuration message MUST start with `avote-tl/v1:j` according to ARC-0002, following the json data.

Trusted list contains all accounts which were added to the trusted list and which were not removed from the trusted list until the decision time of the voting.

The trusted list voting results calculates the same way as the 1 coin = 1 vote, with difference that if the account is on the trusted list, his voting power equals 1, and if the account is not on the trusted list, its voting power equals zero. The results for 1 coin = 1 vote are calculated in balance of the account at the final question block (the question entry block plus the duration stated in the question duration).

Decision snapshot of the trusted list for the vote calculation is the list of accounts in the trusted list in the final block when it is allowed to vote for the question. The additions or removal from the trusted list in the last question block MUST be processed. If the account is in the list of the accounts to be added as well as in the list to be removed in the single transaction, the removal MUST be applied.

```
{
    "$schema": "http://json-schema.org/draft-07/schema",
    "$id": "https://scholtz.github.io/AMS/AMS-0001/avote-tl.json",
    "type": "object",
    "title": "Trusted list management schema",
    "description": "Knowledge based pure democracy trusted list JSON document.",
    "default": {},
    "examples": [
        {
            "a": [
                "TESTAUZJU4JRAPUZBH4FCPYDLEWIFIFRPVILUZBSYP6IBZLYF6M6YVMMX4",
                "TESTB74MOARQDWSX4433VWVNO4VJK3PDQWQ4JEOVQQTK3ZIX2MK3JF55TE",
                "TESTC2TMLDK273INHLXCSV235NFJ5LITNFDXZPU7JTZCVCBAZDUSJS4OPU"
            ],
            "r": [
                "TESTQKYINIZLITDRT3BECSIPI77IQVCXG5I5SNOQLRO4PWSAQPSPCRHUXU"
            ]
        }
    ],
    "properties": {
        "a": {
            "$id": "#/properties/a",
            "type": "array",
            "title": "Trusted list additions",
            "description": "List of accounts to be added to the trusted list",
            "default": [],
            "examples": [
                [
                    "TESTAUZJU4JRAPUZBH4FCPYDLEWIFIFRPVILUZBSYP6IBZLYF6M6YVMMX4",
                    "TESTB74MOARQDWSX4433VWVNO4VJK3PDQWQ4JEOVQQTK3ZIX2MK3JF55TE"
                ]
            ],
            "additionalItems": false,
            "items": {
                "$id": "#/properties/a/items",
                "anyOf": [
                    {
                        "$id": "#/properties/a/items/anyOf/0",
                        "type": "string",
                        "title": "Account",
                        "minLength": 1,
                        "maxLength": 60,
                        "description": "The valid account",
                        "default": "",
                        "examples": [
                            "TESTAUZJU4JRAPUZBH4FCPYDLEWIFIFRPVILUZBSYP6IBZLYF6M6YVMMX4",
                            "TESTB74MOARQDWSX4433VWVNO4VJK3PDQWQ4JEOVQQTK3ZIX2MK3JF55TE"
                        ]
                    }
                ]
            }
        },
        "r": {
            "$id": "#/properties/r",
            "type": "array",
            "title": "Trusted list removals",
            "description": "List of accounts to be removed from the trusted list.",
            "default": [],
            "examples": [
                [
                    "TESTQKYINIZLITDRT3BECSIPI77IQVCXG5I5SNOQLRO4PWSAQPSPCRHUXU"
                ]
            ],
            "additionalItems": false,
            "items": {
                "$id": "#/properties/r/items",
                "anyOf": [
                    {
                        "$id": "#/properties/r/items/anyOf/0",
                        "type": "string",
                        "title": "Account",
                        "minLength": 1,
                        "maxLength": 60,
                        "description": "The valid account.",
                        "default": "",
                        "examples": [
                            "TESTQKYINIZLITDRT3BECSIPI77IQVCXG5I5SNOQLRO4PWSAQPSPCRHUXU"
                        ]
                    }
                ]
            }
        }
    },
    "additionalProperties": false
}
```

```
avote-tl/v1:j{"a":["TESTAUZJU4JRAPUZBH4FCPYDLEWIFIFRPVILUZBSYP6IBZLYF6M6YVMMX4","TESTB74MOARQDWSX4433VWVNO4VJK3PDQWQ4JEOVQQTK3ZIX2MK3JF55TE","TESTC2TMLDK273INHLXCSV235NFJ5LITNFDXZPU7JTZCVCBAZDUSJS4OPU"],"r":["TESTQKYINIZLITDRT3BECSIPI77IQVCXG5I5SNOQLRO4PWSAQPSPCRHUXU"]}
```
