### Result

Result is the message stored on the blockchain.

The blockchain message MUST be with amount 0 of basic tokens with specific note structure described below. 

Sender of the message is auditor. Anybody can calculate results and be in the role of auditor. 

If sender is the questioner, the results counted are considered final. Questioner in rare cases can fix results by submitting the result message again. The latest message of questioner is the decision making message.

Result starts with ```avote-result/v1/{ShortQuestionId}:j``` according to ARC-0002, following the json data.

ShortQuestionId is the tx id of the message with the question for which this vote is answer. ShortQuestionId must be upper case substring from zero with length of 10 characters.


Json data MUST comply with following json schema:

```
{
    "$schema": "http://json-schema.org/draft-07/schema",
    "$id": "https://scholtz.github.io/AMS/AMS-0001/avote-result.json",
    "type": "object",
    "title": "Vote result schema",
    "description": "Knowledge based pure democracy result JSON document.",
    "default": {},
    "examples": [
        {"q":"CRID3AHJGGVE75UTDO5GI7PXM6PUD6WXB7BTAD3IPWFTMUXUKHDA","r":{"sbr":{"A":3500.1,"B":7300.1,"C":2000.1},"qbr":{"A":3000.1,"B":7000.1,"C":2000.1},"ssar":{"A":50.1,"B":30.1,"C":40.1},"qsar":{"A":50.1,"B":30.1,"C":40.1},"stlr":{"A":5.1,"B":2.1,"C":1.1},"qtlr":{"A":5.1,"B":2.1,"C":1.1}}}
    ],
    "required": [
        "q",
        "r"
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
        "r": {
            "$id": "#/properties/r",
            "type": "object",
            "title": "Results",
            "examples": [
                {"sbr":{"A":3500.1,"B":7300.1,"C":2000.1},"qbr":{"A":3000.1,"B":7000.1,"C":2000.1},"ssar":{"A":50.1,"B":30.1,"C":40.1},"qsar":{"A":50.1,"B":30.1,"C":40.1},"stlr":{"A":5.1,"B":2.1,"C":1.1},"qtlr":{"A":5.1,"B":2.1,"C":1.1}}
            ],
            "additionalProperties": true,
            "properties": {
                "sbr": {
                    "$id": "#/properties/simple-balance-results",
                    "type": "object",
                    "title": "Simple balance results",
                    "examples": [
                        {"A":3500.1,"B":7300.1,"C":2000.1}
                    ],
                    "additionalProperties": true,
                },
                "qbr": {
                    "$id": "#/properties/quadratic-balance-results",
                    "type": "object",
                    "title": "Quadratic balance results",
                    "examples": [
                        {"A":3500.1,"B":7300.1,"C":2000.1}
                    ],
                    "additionalProperties": true,
                },
                "ssar": {
                    "$id": "#/properties/simple-single-account-results",
                    "type": "object",
                    "title": "Simple single account results",
                    "examples": [
                        {"A":3500.1,"B":7300.1,"C":2000.1}
                    ],
                    "additionalProperties": true,
                },
                "qsar": {
                    "$id": "#/properties/quadratic-single-account-results",
                    "type": "object",
                    "title": "Quadratic single account results",
                    "examples": [
                        {"A":3500.1,"B":7300.1,"C":2000.1}
                    ],
                    "additionalProperties": true,
                },
                "stlr": {
                    "$id": "#/properties/simple-trusted-list-results",
                    "type": "object",
                    "title": "Simple trusted list results",
                    "examples": [
                        {"A":3500.1,"B":7300.1,"C":2000.1}
                    ],
                    "additionalProperties": true,
                },
                "qtlr": {
                    "$id": "#/properties/quadratic-trusted-list-results",
                    "type": "object",
                    "title": "Quadratic trusted list results",
                    "examples": [
                        {"A":3500.1,"B":7300.1,"C":2000.1}
                    ],
                    "additionalProperties": true,
                },
            }
        }
    },
    "additionalProperties": false
}
```


Example:
```
avote-result/v1/CRID3AHJGG:j{"q":"CRID3AHJGGVE75UTDO5GI7PXM6PUD6WXB7BTAD3IPWFTMUXUKHDA","r":{"sbr":{"A":3500.1,"B":7300.1,"C":2000.1},"qbr":{"A":3000.1,"B":7000.1,"C":2000.1},"ssar":{"A":50.1,"B":30.1,"C":40.1},"qsar":{"A":50.1,"B":30.1,"C":40.1},"stlr":{"A":5.1,"B":2.1,"C":1.1},"qtlr":{"A":5.1,"B":2.1,"C":1.1}}}
```
