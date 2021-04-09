---
description: Secure architecture evaluation criteria
---

# Architectural criteria

The actual check-list from community for architecture requirements is placed [here](https://github.com/OWASP/ASVS/blob/master/4.0/en/0x10-V1-Architecture.md) and [here on our gitbook](https://docs.whitespots.io/practices-implementation/design/security-requirements/asvs-v4-checklists#v-1-architecture-design-and-threat-modeling-requirements) + [russian version](https://docs.whitespots.io/practices-implementation/design/security-requirements/asvs-v4-sdlc-split/asvs-v4-sdlc-split-rus#dizain) \(a bit more requirements were moved to design due to our point of view\). 

We would like to tell you 2 points from our team.

* [ ] Each component of your architecture should **never trust to any other component.** It means that:  - If you need to sign any data from your service - sign it there. Don't delegate this task to any 3rd party service  - If you need to allow a user to do something on your system - read all the necessary information from the user session, not from the IDs provided by the client.  ...
* [ ] Each architecture change **is illustrated by a sequence diagram and the difference between the two states**: before and after. It means that: - You should always understand the key point of each improvement - All new components should satisfy other security requirements and pass all SSDLC stages.

