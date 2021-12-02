# Cast vote

Question is the message stored on the blockchain.

The blockchain message MUST be self signed message, with amount 703 of basic tokens with specific note structure described below.

Question starts with `avote-vote/v1/{ShortQuestionId}:j` according to ARC-0002, following the json data.

ShortQuestionId is the tx id of the message with the question for which this vote is answer. ShortQuestionId must be upper case substring from zero with length of 10 characters.

If json data is not valid according to JSON standard, or according to the schema below, the answer MUST NOT be calculated to the final results. If the vote cast code list does not mach with question option codes list, the answer MUST NOT be calculated to the final result.

The weights of the answers MUST be integer numbers in range between 0 and 1000 including. If the weights of results does not match with this criteria, the answer MUST NOT be calculated to the final result.

The voting power of the user is distributed to answers according to specified weights. For example in the example of distribution of `{"A":35,"B":73,"C":20}` the sum of the weights is 128, so the voting power of the casted vote for `A` is `35/128~=27,3%`

Json data MUST comply with following json schema:

```
{
    "$schema": "http://json-schema.org/draft-07/schema",
    "$id": "https://scholtz.github.io/AMS/AMS-0001/avote-vote.json",
    "type": "object",
    "title": "Vote cast schema",
    "description": "Knowledge based pure democracy answer JSON document.",
    "default": {},
    "examples": [
        {"q":"CRID3AHJGGVE75UTDO5GI7PXM6PUD6WXB7BTAD3IPWFTMUXUKHDA","a":{"A":35,"B":73,"C":20}}
    ],
    "required": [
        "q",
        "a"
    ],
    "properties": {
        "q": {
            "$id": "#/properties/q",
            "type": "string",
            "minLength": 1,
            "maxLength": 60,
            "title": "The question id",
            "description": "Tx id of the question message from the blockchain",
            "default": "",
            "examples": [
                "CRID3AHJGGVE75UTDO5GI7PXM6PUD6WXB7BTAD3IPWFTMUXUKHDA"
            ]
        },
        "a": {
            "$id": "#/properties/a",
            "type": "object",
            "title": "Valid vote options",
            "description": "Valid vote options. Object of mapping from code to weight of the answer.",
            "default": {},
            "examples": [
                {"A":35,"B":73,"C":20}
            ],
            "additionalProperties": true
        }
    },
    "additionalProperties": false
}
```

Example:

```
avote-vote/v1/CRID3AHJGG:j{"q":"CRID3AHJGGVE75UTDO5GI7PXM6PUD6WXB7BTAD3IPWFTMUXUKHDA","a":{"A":35,"B":73,"C":20}}
```

\
