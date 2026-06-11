# Rotation and least privilege

Storing secrets safely reduces the chance of a leak, but secrets can still be exposed, so two further practices limit the damage when one is: scoping each secret to the least access it needs, so a leak reaches little, and rotating secrets regularly, so an exposure has a limited lifetime. Together they shrink the blast radius and the duration of any compromise, which matters because no storage is perfect and some leaks will happen.

## Least privilege for each secret

Least privilege means each secret grants only the access it actually needs, no more, so that if it leaks, the access it hands an attacker is as narrow as possible. A key that only needs to read should not also be able to write or delete. A credential that only needs one service's data should not reach others. A token scoped to a single purpose limits what its exposure compromises to that purpose. The reasoning is that the damage of a leaked secret equals the access it grants, so minimizing each secret's access minimizes the worst case of its exposure. A broadly privileged secret is a large liability if leaked; a narrowly scoped one is a small one.

## Separate secrets for separate purposes and environments

Following from least privilege, different purposes and different environments should use different secrets, so that the access each represents is isolated. A development secret separate from production means a development leak does not touch production. A secret for one service separate from another means leaking one does not expose the other. This separation contains a compromise to the narrow slice the leaked secret covered, rather than letting one exposure cascade across everything. The opposite, one powerful secret shared across purposes and environments, means a single leak compromises all of it at once, which is exactly the concentration of risk that separation avoids. Each secret should be specific, so its exposure is specific.

## Rotation limits the lifetime of exposure

Rotation means changing secrets regularly, replacing the old value with a new one, so that any given secret is only valid for a limited time. The benefit is that a secret which leaked without your knowledge stops working once it is rotated, so the window during which an undetected exposure can be exploited is bounded by the rotation interval rather than being open-ended. A secret that never changes, if leaked and not noticed, remains usable indefinitely; a secret rotated on a schedule becomes useless to an attacker after the next rotation. Regular rotation is therefore a defense against the leaks you do not know about, capping how long any exposure can be exploited.

## Each secret needs an owner and a schedule

Making rotation real requires knowing what secrets exist, who is responsible for each, and when each should be rotated, rather than rotation being a vague intention. Each secret having a documented owner and a rotation schedule means rotation actually happens on a cadence rather than never, and means that when a secret needs changing, someone is responsible for doing it. An inventory of secrets, with owners and schedules, also surfaces the secrets that have been around too long, the ones most likely to have leaked at some point without notice. Without this tracking, rotation is something everyone agrees is good and no one does, leaving long-lived secrets accumulating risk.

## Together they shrink the worst case

Least privilege and rotation work on the two dimensions of a secret's risk: how much a leak grants, and how long a leak lasts. Least privilege shrinks how much, by ensuring each secret grants little. Rotation shrinks how long, by ensuring each secret is valid only for a bounded period. A secret that is both narrowly scoped and regularly rotated is a small, time-limited liability even if leaked, where a broadly privileged, never-rotated secret is a large, permanent one. Applying both, especially to the most powerful secrets and the ones touching the most sensitive systems, is what keeps the inevitable occasional exposure from becoming a serious breach. The next page covers the response when you know a secret has leaked, which rotation is also the core of.
