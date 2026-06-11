# What to do when one leaks

Despite every precaution, secrets sometimes get exposed: committed to a repository, pasted somewhere public, included in a screenshot, found in logs. When a secret leaks, the response is not to hope it went unnoticed but to treat it as compromised and replace it immediately. A leaked secret is an open door until it is changed, and the assumption must be that if you could find the exposure, so could someone else, including the automated scanners that hunt for leaked secrets constantly.

## Assume it is compromised

The first move is to treat any leaked secret as compromised, regardless of how briefly it was exposed or whether you think anyone saw it. You cannot know who accessed it, and assuming the best is how exposures turn into breaches. Secrets committed to public repositories in particular are scraped by automated tools within a very short time, so a secret that touched a public repository should be assumed to have been captured, even if you removed it moments later. The safe assumption, that an exposed secret is in the wrong hands, drives the right response; the unsafe assumption, that a quick removal undid the exposure, leaves the door open.

## Rotate it immediately

The core of the response is to rotate the leaked secret, generating a new one and revoking or replacing the exposed one, so that the leaked value no longer works. This is the action that actually closes the door: the exposed secret becomes useless once it is replaced, regardless of who has it. Rotation should happen as soon as the leak is discovered, because every moment the exposed secret remains valid is a moment it can be used. Removing the secret from where it leaked, deleting the commit, the message, the screenshot, is not sufficient on its own, because the exposure already happened and may have been captured; only replacing the secret renders the leaked copy worthless.

## Removal is not enough

A common mistake is to remove the secret from where it appeared and consider the problem solved, without rotating it. Removing a secret from a repository, for instance, does not erase it from the repository's history, and it certainly does not retrieve any copies already captured by scanners or observers during the exposure. The secret is still valid, and the leaked copies still work. This is why removal alone is inadequate: the leaked value remains usable until it is rotated. The correct sequence is to rotate first, making the leaked value useless, and then clean up the exposure as a secondary step, rather than cleaning up and hoping the exposure did no harm.

## Investigate the scope and the cause

After rotating, it is worth understanding how far the secret could have been used and how it leaked. Checking whether the exposed secret was used in unexpected ways during its exposure window can reveal whether the leak was actually exploited. Understanding how it leaked, a committed file, a logged value, a shared screenshot, points to the process gap that let it happen, so you can close that gap and prevent the next leak of the same kind. A leak is information about a weakness in how secrets are handled, and responding fully means not just rotating the one secret but fixing the path that exposed it, so the same mistake does not recur.

## Build the response into the routine

Because leaks happen, the response should be a known procedure rather than an improvisation, and the practices from the rest of this reference make the response faster and less damaging. Knowing what secrets exist and who owns each means you can identify and rotate a leaked one quickly. Least privilege means a leaked secret granted little, so the exposure is contained. Separate secrets per environment and purpose mean the leak touches only its slice. Regular rotation means you already have a rotation process to invoke. The systems that handle a leak well are the ones that prepared for it: a secret inventory, scoped and separated secrets, a rotation capability, and the firm rule that any exposed secret is rotated immediately and treated as compromised. The leak is then a contained, quickly closed incident rather than an open-ended breach.
