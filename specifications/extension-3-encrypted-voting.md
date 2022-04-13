### Extension 3 - Encrypted voting

Purpose of the encrypted voting is to hide voter cast while the voting session is in progress.

Questioner for each question generates new Ed25519 mnemonic and stores it securly. Public key of this encryption account is called Question public key. If encryption of the messages is allowed, he publish encryption account address in the question message.

Curve25519XSalsa20Poly1305 is used to encrypt data. Voter encrypts the data in form of https://scholtz.github.io/AMS/AMS-0001/avote-vote.json and produces the json with the https://scholtz.github.io/AMS/AMS-0001/avote-vote-enc.json schema.

Encrypted vote cast is the message stored on the blockchain.

The blockchain message MUST be self signed message, with amount 703 of basic tokens with specific note structure described below.

Encrypted vote cast starts with ```avote-vote-enc/v1/{ShortQuestionId}:j``` according to ARC-0002, following the json data.

Questioner MAY publish his encryption keys to specific auditing account using ARC-0015 starndard. The content of the message is the mnemonic of the encryption account.

Questioner MAY publish the mnemonic of the encrypting account to the restult message. The questioner SHOULD publish the policy on weather he plans to publish the private encryption key on his website or in the question.


Json data MUST comply with following json schema:

```
{
    "$schema": "http://json-schema.org/draft-07/schema",
    "$id": "https://scholtz.github.io/AMS/AMS-0001/avote-vote-enc.json",
    "type": "object",
    "title": "Vote cast schema",
    "description": "Knowledge based pure democracy answer JSON document in encrypted form.",
    "default": {},
    "examples": [
        {"nonce":"ftGVJfrKJg+PPNCMbKPdLMN3OKNNnHDk","otPK":"w955HlFMM4e9dD1OQv31k4npHhs/w4QWc5Q1tcjxFkM=","cT":"O+M+3Y78RdxnMD6mJfNrfi8eT7dKmAFxJCq4z8Zb/lob+7tWptW1hPQWe60lmT64YLNdMSrPd9N0Wszr6AQFar5jbekHmM/YME/FEf4FjpYBLOwXK54MNy+8LOORNp1f"}
    ],
    "required": [
        "nonce",
        "otPK",
        "cT"
    ],
    "properties": {
        "nonce": {
            "$id": "#/properties/nonce",
            "type": "string",
            "title": "Nonce",
            "description": "Base64 data of random number. Byte length: nacl.box.nonceLength. const nonce = nacl.randomBytes(nacl.box.nonceLength);",
            "examples": [
                "ftGVJfrKJg+PPNCMbKPdLMN3OKNNnHDk"
            ],
            "additionalProperties": false
        },
        "otPK": {
            "$id": "#/properties/otPK",
            "type": "string",
            "title": "Encryption public key",
            "description": "Public key of randomly generated key pair when encoding the message. const otKeyPair = nacl.box.keyPair();",
            "examples": [
                "w955HlFMM4e9dD1OQv31k4npHhs/w4QWc5Q1tcjxFkM="
            ],
            "additionalProperties": false
        },
        "cT": {
            "$id": "#/properties/cT",
            "type": "string",
            "title": "Cipher text",
            "description": "Public key of randomly generated key pair when encoding the message. const cipherText = nacl.box(Buffer.from(encMsg),nonce,rcptPubKey,otKeyPair.secretKey)",
            "examples": [
                "O+M+3Y78RdxnMD6mJfNrfi8eT7dKmAFxJCq4z8Zb/lob+7tWptW1hPQWe60lmT64YLNdMSrPd9N0Wszr6AQFar5jbekHmM/YME/FEf4FjpYBLOwXK54MNy+8LOORNp1f"
            ],
            "additionalProperties": false
        }
    },
    "additionalProperties": false
}
```

Example: 
```
avote-vote-enc/v1/XIP4Y7NMP2:j{"nonce":"ftGVJfrKJg+PPNCMbKPdLMN3OKNNnHDk","otPK":"w955HlFMM4e9dD1OQv31k4npHhs/w4QWc5Q1tcjxFkM=","cT":"O+M+3Y78RdxnMD6mJfNrfi8eT7dKmAFxJCq4z8Zb/lob+7tWptW1hPQWe60lmT64YLNdMSrPd9N0Wszr6AQFar5jbekHmM/YME/FEf4FjpYBLOwXK54MNy+8LOORNp1f"}
```
