# Environment variables and vaults

If secrets do not belong in code, repositories, frontends, logs, or screenshots, they need somewhere to live where the application can use them but they are not exposed. The common answers are environment variables for simpler cases and dedicated secret managers for more demanding ones. Both keep secrets out of the code while making them available to the application, and the choice between them depends on how many secrets you have and how much control you need over them.

## Environment variables

An environment variable holds a value in the environment the application runs in, rather than in the code, so the application reads the secret from its environment at run time instead of having it written into a file that gets committed. This keeps the secret out of the codebase and out of version control: the code references the environment variable, and the actual value is supplied by the environment where the application runs, which is configured separately and not committed. Environment variables are the common baseline for keeping secrets out of code, suitable for many applications, and they are supported everywhere applications run. The value lives in the run-time environment, the code only names it.

## The local configuration file caveat

Locally, environment variables are often set from a configuration file that holds the values, and this file is exactly the kind that must never be committed to version control. The file containing the actual secret values is excluded from version control, so that the secrets it holds are not committed, while a non-secret example file showing which variables are needed, without their values, can be committed to document what the application requires. This pattern, real values in an excluded file, an example with no values committed, is standard, and the critical part is ensuring the file with real values is genuinely excluded, because committing it is one of the most common secret leaks.

## Secret managers and vaults

For more secrets, more environments, or more demanding control, a dedicated secret manager or vault stores secrets centrally with access control, rather than spreading them across environment configurations. A secret manager keeps secrets in one protected place, controls who and what can read each one, and often supports rotation and auditing of access. This is more capable than environment variables: it centralizes the secrets, makes access controllable and observable, and eases rotation. Many platforms provide a secret manager as a feature, so before adopting a separate tool, it is worth checking whether the platform you already use offers one, in keeping with the stack-check discipline. For a small application a few environment variables suffice; as the number of secrets and environments grows, a manager becomes worthwhile.

## Separate secrets per environment

Whichever storage you use, the secrets for different environments, development, testing, production, should be separate, so that a secret used in development is not the same one that protects production data. Separate secrets per environment mean that a leaked development secret cannot touch production, limiting the damage of any exposure to the environment it belongs to. This is part of scoping, covered next, but it bears on storage because it means each environment has its own set of secret values, configured separately, rather than one shared set across all of them. Sharing a secret across environments means a leak anywhere is a leak everywhere, which separate per-environment secrets prevent.

## The principle: usable but not exposed

The goal uniting environment variables and secret managers is to make secrets available to the application that needs them while keeping them out of the places they could leak. The code names the secret; the value comes from the environment or the manager at run time; the value is never committed, never in the frontend, never in logs. Whether you use environment variables for a simple case or a secret manager for a demanding one, the principle holds: the application can reach the secret, but the secret is not sitting in the codebase or any public artifact. This is what lets a system use its secrets without exposing them, which is the entire purpose of secrets storage. The next pieces, scoping and rotation, then limit what any single secret can do and how long an exposure lasts.
