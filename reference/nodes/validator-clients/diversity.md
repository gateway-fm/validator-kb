# Validator Client Diversity

To reduce the risk of being exposed to a bug or technological decision 
in one validator client, it is a good practice run different validator clients.

Even though the validator clients use the same API, there is no standard of
storing keys in them.

There are two options on how it is possible to run them:

**Diversify online validator clients**: run different validator clients at the
same time, for different validators. For example, run Vouch for validators 0 to
99, run Lighthouse for validators 100 to 199, etc. Upside: the whole system is
resilient toward issues in a single validator clients, not all of them will go
down at the same time. Downside: adds complications to the setup, monitoring
and managing validator clients.

**Diversify cold backup**: run the same validator clients across all
validators, and keep keystores and launch scripts ready for another validator
client to replace it in case of disaster. Upside of this approach: easy to
manage online validator clients, simple setup. Downside: in case of an issue in
a validator client, all validators will be offline at the same time.
