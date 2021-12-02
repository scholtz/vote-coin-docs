# Question

Question is the message stored on the blockchain.

The blockchain message MUST be self signed message, with amount 702 of basic tokens with specific note structure described below.

Question starts with `avote-question/v2:j` according to ARC-0002, following the json data.

If json data is not valid according to JSON standard, the question MUST NOT be shown to the users.

Json data MUST comply with following json schema:

```
{
  "$schema": "http://json-schema.org/draft-07/schema",
  "$id": "https://scholtz.github.io/AMS/AMS-0001/avote-question.json",
  "type": "object",
  "title": "Question schema",
  "description": "Knowledge based pure democracy question JSON document.",
  "default": {},
  "examples": [
      {
          "t": "Best project",
          "q": "Decide which project is the best\nA - AAA\nB - BBB\nC - CCC",
          "duration": 100,
          "category": "community",
          "o": {
              "A": "AAA",
              "B": "BBB",
              "C": "CCC"
          }
      }
  ],
  "required": [
      "t",
      "q",
      "duration",
      "category",
      "o"
  ],
  "properties": {
      "t": {
          "$id": "#/properties/t",
          "type": "string",
          "minLength": 1,
          "maxLength": 50,
          "title": "Title of the question",
          "description": "Title shown in the table of the questions",
          "default": "",
          "examples": [
              "Best project"
          ]
      },
      "q": {
          "$id": "#/properties/q",
          "type": "string",
          "minLength": 1,
          "maxLength": 500,
          "title": "Question text",
          "description": "The text of the question. MAY contain new lines specified as \n. ",
          "default": "",
          "examples": [
              "Decide which project is the best\nA - AAA\nB - BBB\nC - CCC"
          ]
      },
      "duration": {
          "$id": "#/properties/duration",
          "type": "integer",
          "minimum": 1,
          "maximum": 1000000,
          "title": "The duration how long the question is valid.",
          "description": "Duration is calculated in number of blocks. If there is 1, the question will have valid votes only in the block of inception, and the next block.",
          "default": 0,
          "examples": [
              100
          ]
      },
      "category": {
          "$id": "#/properties/category",
          "type": "string",
          "minLength": 1,
          "maxLength": 50,
          "title": "The category",
          "description": "The category of the question. Categories are managed by the questioner.",
          "default": "",
          "examples": [
              "community"
          ]
      },
      "o": {
          "$id": "#/properties/o",
          "type": "object",
          "title": "Valid vote options",
          "description": "Valid vote options. Object of mapping from code to text of the question. The code will be used in vote cast to specify the answer.",
          "default": {},
          "examples": [
              {
                  "A": "AAA",
                  "B": "BBB",
                  "C": "CCC"
              }
          ],
          "additionalProperties": true
      }
  },
  "additionalProperties": false
}
```

Example:

```
avote-question/v1:j{"t":"Best project","q":"Decide which project is the best\nA - AAA\nB - BBB\nC - CCC","max":4410,"category":"community","o":{"A":"AAA","B":"BBB","C":"CCC"}}
```

\
