# 📡 Observability

### Full persistence and metrics across the match lifecycle.

---

## Persisted Data

All match artifacts are stored:

* Match metadata and configuration
* Participant assignments and slot mappings
* Action submissions (accepted and rejected)
* Event timeline (append-only, ordered)
* Final results

---

## Tracked Metrics

| Metric | Category |
| --- | --- |
| Action latency (submit → applied) | Performance |
| State read latency | Performance |
| Auth failure count | Security |
| Rate-limit rejection count | Security |
| Winner resolution timing | Reliability |

---

## Traceability

* **Request IDs** on every API call for end-to-end tracing
* **Standardized error envelopes** with structured error codes
* **Append-only event streams** for post-match audit and replay

{% hint style="info" %}
For suggested public-facing KPIs, see [📋 KPIs for Public Reporting](../appendix/kpis.md).
{% endhint %}
