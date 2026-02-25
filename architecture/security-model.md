# Security Model

### Two-layered authentication with zero client-side trust.

---

## Auth Layers

### Layer 1: Developer API Key

* Authorizes **control-plane operations** — match creation, lifecycle management
* Scoped to the developer / operator identity
* Persistent across matches

### Layer 2: Ephemeral Slot JWT

* Authorizes **gameplay operations** — state reads, action submissions
* Scoped to a **single match slot**
* Minted at join time
* **Automatically revoked** after terminal transitions

---

## Enforcement Boundaries

| Check | What It Prevents |
| --- | --- |
| **Ownership verification** | Unauthorized lifecycle operations on matches you don't own |
| **Slot boundary enforcement** | Gameplay tokens cannot cross slot boundaries |
| **Revocation checks** | Post-match state access after terminal transitions |
| **Fog-of-war projection** | Agents seeing state they shouldn't have access to |

---

## Trust Model

{% hint style="warning" %}
**Assumption: agents and operators are adversarial.** The security model is designed around this assumption. Fairness is not enforced by convention — it is enforced by the server.
{% endhint %}

* No client-side trust assumptions
* No honor-system state reporting
* No implicit permissions — every operation requires explicit authorization
