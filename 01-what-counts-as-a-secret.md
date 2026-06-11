# What counts as a secret

A secret is anything that grants access, proves identity, or unlocks a capability, and whose exposure would let someone act as you or reach something they should not. The category is broader than just passwords, and the first step in protecting secrets is recognizing all of them, because a secret you do not think of as a secret is one you will not protect. Treating the full set as sensitive is what prevents the leaks that come from overlooking something.

## The common kinds

The secrets most systems handle include API keys that authenticate you to a service, often with the ability to spend money or access data; passwords, whether a user's or a system's; tokens that grant access for a session or a purpose; private keys used for encryption, signing, or authentication; and connection strings that contain the credentials to reach a database or another system. Each of these, if exposed, hands someone else the access it represents. The unifying feature is that the secret is the thing standing between an outsider and a capability, so whoever holds the secret holds the capability.

## Why they need protection

A secret needs protection because exposure is not a partial problem; it is a full grant of whatever the secret unlocks. An exposed API key lets anyone make calls as you, potentially running up costs or reaching your data. An exposed database credential lets anyone reach the database. An exposed private key lets anyone do whatever that key authorizes. There is rarely a halfway state: once a secret is out, the access it represents is available to whoever has it, until the secret is changed. This all-or-nothing nature is why secrets are guarded so carefully, and why a single leaked secret can be a serious breach rather than a minor slip.

## Secrets hide in unexpected places

Beyond the obvious credentials, secrets accumulate in places people forget. A connection string in a configuration file contains a secret. A token pasted into a chat message is a secret now sitting in that chat history. A key visible in a screenshot shared for debugging is exposed. A credential in a log line is in the logs. Recognizing that secrets end up in configuration, messages, screenshots, logs, and other incidental places is part of protecting them, because the leak often happens not through the front door but through one of these side channels where a secret was casually placed without thinking of it as sensitive.

## Treat the whole category as sensitive

The practical stance is to treat anything that grants access or proves identity as a secret requiring protection, rather than protecting only the things explicitly labeled as passwords. When you handle a key, a token, a credential, or a private key, the default is that it is sensitive and must be kept out of the places it could leak and stored where access is controlled. This default catches the secrets that would otherwise be overlooked, the connection string that does not feel like a password, the API key that seems harmless, the token that was only meant to be temporary. The rest of this reference assumes this broad recognition, because the protections only work if applied to everything that actually is a secret, not just the things that obviously look like one.
