### Vote result calculation

Each account has specific voting power. 

- **balance voting power** means 1 coin equals to 1 vote. If account owns balance of 1000 tokens, it has 1000 more voting power than account that holds 1 token. Token may be for example DAO token, algorand ASA, Algorand token itself, Ethereum token or any other tokens which are compatible with this standard.
- **single account voting power** means that 1 account has 1 vote. This can be also reduced to trusted accounts using trusted list extension where questioner selects accounts which he consider trusted.

Single question  results will always lead to multiple results:

- **Simple balance results**
- **Quadratic balance results**
- **Simple single account results**
- **Quadratic single account results**
- **Simple trusted list results**
- **Quadratic trusted list results**

This specifications does not interpret what level of acceptance of which type of results is acceptance criteria for questioner. Questioner SHOULD define his acceptance criteria in memorandum, constitution or company statute.

Note, that in the delegation extension, a voting power of an account if it does not vote, is transfered to a delegated account.

#### Simple balance results

Single account voting power for specific option is ```Token balance * On / (O1 + O2 .. Om)```

Result for all options MUST be sum of all balance voting power of all accounts which has voted. 

#### Quadratic balance results

Single account voting power for specific option is ```Token balance * On^2 / (O1^2 + O2^2 .. Om^2)```

Result for all options MUST be sum of all balance voting power of all accounts which has voted. 

#### Simple single account results

Single account voting power for specific option is ```1 * On / (O1 + O2 .. Om)```

Result for all options MUST be sum of all balance voting power of all accounts which has voted. 

#### Quadratic single account results

Single account voting power for specific option is ```1 * On^2 / (O1^2 + O2^2 .. Om^2)```

Result for all options MUST be sum of all balance voting power of all accounts which has voted. 

#### Simple trusted list results

Single account voting power from trusted list for specific option is ```1 * On / (O1 + O2 .. Om)``` , else 0.

Result for all options MUST be sum of all balance voting power of all accounts which has voted. 

#### Quadratic trusted list results

Single account voting power from trusted list for specific option is ```1 * On^2 / (O1^2 + O2^2 .. Om^2)``` , else 0.

Result for all options MUST be sum of all balance voting power of all accounts which has voted. 
