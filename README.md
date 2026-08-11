# UDLM — the data model, published in reviewable pieces

**What this is.** The Universal Data Lifecycle Model: a vendor-neutral, Apache-2.0 specification for
declaring data-center resources (intent), realizing them, discovering them, and rebuilding them.
Spec and schema only — no runtime lives here.

## How this repository is being published

The previous set was eighteen PRs totalling tens of thousands of lines, and it queued everything
behind the first one. That was too much to ask anyone to review.

**This publishes in small pieces, scoped to what is actually needed next.** The current target is the
**VM provisioning lifecycle** — the classes a VM touches end to end, and nothing else:

| | |
|---|---|
| **1. Foundation** | the meta-schemas everything else validates against |
| **2. VM lifecycle classes** | compute · network · address pool · storage class · namespace · volume |
| **3. The flow** | how the data moves, and where each piece comes from |

Further areas follow as they are needed. If something you are waiting on is not here, say so and it
moves up.

## Reading order

1. `registry/SPEC-DESIGN-REQUIREMENTS.md` — the rules every type must satisfy. Read this first.
2. `registry/class.schema.json` — the authoring surface. A type is defined as a **Class** at one of
   three scopes: Base (portable across a category), Type (portable across providers), Provider
   (provider-bound). Scope IS portability.
3. `registry/classes/` — the classes themselves, mirroring the hierarchy as directories.
4. `registry/generated/` — the compiled flat specs. **Never authored** — a generator emits them from
   the classes, and CI fails if they drift.
5. `registry/realized-entity.schema.json` — what an instance looks like once it exists.

## What review is most useful

The framework is settled; **the definitions are what need your eyes.** They were built against one
estate, and the question is whether they are fit for purpose against yours — the fields a VM
actually needs, the ones that are missing, and the ones that only make sense where they came from.
