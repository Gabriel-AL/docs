# 2021-11-05 - Adjust ADR approval rules for the new org structure

{% hint style="info" %}
This document represents an architecture decision record (ADR) and has been mirrored from the ADR section in our Shopware 6 repository.
You can find the original version [here](https://github.com/shopware/platform/blob/trunk/resources/references/adr/workflow/2021-11-05-adjust-ADR-approval-rules.md)
{% endhint %}

## Context

When we decided to introduce ADRs we also decided that there need to be special approval rules for those ADRs.
The approval rules are now outdated after the reorg, so to continuously ensure that the decisions documented in ADRs work in the long run for us, we want to adapt the approval rules.

## Decision

The old approval rules for reference:
```
*  Two additional developers have to review the ADR
   *  One developer must be a member of the core development team
   *  One developer must be a member of a team, other than the team of the creator
*  One product owner or higher role has to approve an ADR
```

The new approval rule is the following:
* At least one member of each of the Component Teams for the Core, Admin and Storefront area have to review the ADR.

## Consequences

ADRs now need to be approved by the new approval rules.
