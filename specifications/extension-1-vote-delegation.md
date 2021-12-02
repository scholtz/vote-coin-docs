# Extension 1 - Vote delegation

Vote delegation is the extension for the voting system. It MAY not have to be used by the voting system implementation. If the voting system does not implement delegation, it should clearly state that voting system does not support delegation of the voting power. For knowledge based pure democracy voting system it is highly RECOMMENDED to use the delegation of the voting power.

Vote delegation is the delegation of the voting power from the delegee account to delegated account. If delegee does not vote, and delegated account votes for question, the delegated account votes with voting power of it self plus sum of voting power of all delegee accounts.

The delegation SHOULD be used in these usecases.

* Person 1 trusts his friend Person 2 in all matters. Person 1 delegates all his/her voting power to Person 2. Person 1 may vote for questions he believes knows the best answer to. With all other voting where Person 2 votes, the Person 1 votes with the Person 2.
* Person 1 trusts Politician 1 in the matter of Finance, and Politician 2 in the matter of IT. Politicians will vote in their specified field of interest, and gain the Person 1 voting power.

The delegation is transferable. If person A delegate his voting power to person B, and person B delegates his voting power to person C, and only person C casts the vote, the voting power of Person C is sum of Person A, Person B and Person C.

To prevent circular delegation, the maximum depth for vote delegation is 100 delegations.

If person A delegates 20 % of his voting power to person B, and 80 % to person C, and person A and B does not vote, and person C votes, the sum of voting power of person C is 80% of person A plus 100% of voting power of person C.

The blockchain message MUST be self signed message, with amount 701 of basic tokens with specific note structure described below.

Vote delegation note field in the blockchain MUST start with `avote-delegation/v1:j` according to ARC-0002, following the json data.

If json data is not valid according to JSON standard, or according to the schema below, the voting power MUST NOT be transfered.

The weights of the delegation between accounts MUST be integer numbers in range between 0 and 1000 including.

Json data MUST comply with following json schema:

```
{
    "$schema": "http://json-schema.org/draft-07/schema",
    "$id": "https://scholtz.github.io/AMS/AMS-0001/avote-delegation.json",
    "type": "object",
    "title": "Vote power delegation schema",
    "description": "Knowledge based pure democracy vote delegation JSON document.",
    "default": {},
    "examples": [
        {"d":{"any":{"TESTB74MOARQDWSX4433VWVNO4VJK3PDQWQ4JEOVQQTK3ZIX2MK3JF55TE":20,"TESTC2TMLDK273INHLXCSV235NFJ5LITNFDXZPU7JTZCVCBAZDUSJS4OPU":80},"finance":{"TESTDUUODZVXNO4YKEK4I5I6UU67ANYBJ77JZUI444VAD7V3TL26DVOMFA":1}}}
    ],
    "required": [
        "d"
    ],
    "properties": {
        "d": {
            "$id": "#/properties/d",
            "type": "object",
            "title": "Delegation of power",
            "description": "The object of categories with the object of accounts and the weights. Weight must be integer number in range from 0 to 1000 including.",
            "default": {},
            "examples": [
                {"any":{"TESTB74MOARQDWSX4433VWVNO4VJK3PDQWQ4JEOVQQTK3ZIX2MK3JF55TE":20,"TESTC2TMLDK273INHLXCSV235NFJ5LITNFDXZPU7JTZCVCBAZDUSJS4OPU":80},"finance":{"TESTDUUODZVXNO4YKEK4I5I6UU67ANYBJ77JZUI444VAD7V3TL26DVOMFA":1}}
            ],
            "additionalProperties": true
        }
    },
    "additionalProperties": false
}
```

Example:

```
avote-delegation/v1:j{"d":{"any":{"TESTB74MOARQDWSX4433VWVNO4VJK3PDQWQ4JEOVQQTK3ZIX2MK3JF55TE":20,"TESTC2TMLDK273INHLXCSV235NFJ5LITNFDXZPU7JTZCVCBAZDUSJS4OPU":80},"finance":{"TESTDUUODZVXNO4YKEK4I5I6UU67ANYBJ77JZUI444VAD7V3TL26DVOMFA":1}}}
```

\
