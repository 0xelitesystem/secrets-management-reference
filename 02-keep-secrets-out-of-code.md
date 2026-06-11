# Keep secrets out of code

The most common way secrets leak is being put somewhere they do not belong: in source code, in a public repository, in a frontend bundle, in logs, in screenshots. Each of these is a place a secret can be read by someone who should not have it. The first rule of secrets management is keeping them out of all of these, because once a secret reaches one of them, it should be considered exposed regardless of what happens next.

## Never in source code committed to a repository

A secret written directly into source code travels wherever that code goes, and code goes into version control, which keeps history. A secret committed to a repository is in the repository's history even if you later remove it, because version control preserves what was there. If the repository is or ever becomes public, the secret is exposed to anyone who looks, including automated scanners that hunt for exactly this. Keeping secrets out of committed code means they are never written into files that get committed, and the configuration files that would hold them are excluded from version control so they cannot be committed by accident. The history-preserving nature of version control is what makes a committed secret a lasting exposure, not a momentary one.

## Never in frontend code

A secret placed in code that runs in the browser, the frontend, is visible to anyone using the site, because frontend code is delivered to and readable by the user. There is no hiding a secret in frontend code; it can be read by inspecting what the browser received. This is a frequent and serious mistake: putting an API key in frontend JavaScript so the browser can call a service directly exposes that key to every visitor. The rule is that secrets live on the server side, never in the frontend, and where the browser needs to reach a service, the request goes through your server, which holds the secret, rather than the browser holding it. Anything in the frontend is public by nature.

## Never in logs

Secrets written into log output sit in the logs, which are often stored, retained, and accessible to more people and systems than the secret should be. A credential, token, or key that appears in a log line, perhaps because an error or a debug statement printed it, is now in the logs wherever they go. This is an easy leak to create accidentally, by logging a request that contains a token, or an error that includes a connection string. Keeping secrets out of logs means ensuring that what gets logged does not include them, scrubbing or omitting the sensitive parts, so that the logs, which are not treated as secret storage, never contain the secrets.

## Never in screenshots or shared with third parties

Secrets leak through casual sharing too: a screenshot taken for debugging that happens to show a key, a configuration pasted into a message or a third-party tool, a secret included in something sent outside your control. Once a secret is in a screenshot shared somewhere, in a chat history, or pasted into an external service, it is exposed to wherever that went. The discipline is to be careful that secrets do not end up in screenshots, messages, or anything shared with third parties, because these incidental channels are common leak paths precisely because they feel casual. A secret shared this way is exposed just as surely as one committed to a public repository.

## Assume exposure means compromise

The reason these rules are absolute is that once a secret reaches any of these places, you cannot reliably un-expose it. A secret committed to a repository is in the history. A secret in a frontend bundle was delivered to users. A secret in logs is wherever the logs went. A secret in a shared screenshot is wherever that was shared. In each case the secret should be treated as compromised, because you cannot know who saw it, which means the response is to rotate it, as the page on leaks covers. This is why keeping secrets out of these places in the first place matters so much: the alternative is not cleanup but replacement, because exposure cannot be undone, only responded to.
