# Technical Decisions Doc

This doc aims to provide one, consolidated place, for answers to broader questions that affect our development, design, and current planning of the Unified JS & Mobile SDKs. The need for this comes out of decisions getting lost in slack threads & GH discussions. This is our new source of truth!

The decisions documented here come after collaboration and consensus amongst Unified SDK leaders. 

**Please add decisions/consensus as they arise!**

Format:
```markdown
## <Topic Name (with date MM/YYYY)>

**Summary**: 

**Rationale**:

**Relevant Links**:
```

---

## OrderID Creation (08/2021)

**Summary**: At this point, we only need to design the specs & SDKs for orderID generation & authorizing/capturing occurring on the server-side. We can revisit this at a later date/backlog it, but for now we can proceed without this in our MVP/design specs.

**Rationale**: 
- A low portion (~5%) of existing PayPal merchants use the client-side only integration.
- We want to narrow the scope of MVP for now so we can make progress on designing specs, get things working, and iterate later based on feedback as requirements change.

**Relevant Links**:
- [GH Discussion](https://github.com/paypal/paypal-sdk-spec/discussions/22)

