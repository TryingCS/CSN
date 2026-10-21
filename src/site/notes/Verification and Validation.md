---
{"dg-publish":true,"permalink":"/verification-and-validation/","created":"2026-10-16T18:42:51.896+01:00","updated":"2026-10-16T18:42:58.097+01:00","dg-note-properties":{}}
---

#ms 
## Verification vs. Validation (V&V)


| | **Verification** | **Validation** |
|---|---|---|
| **Question** | "Did I build the model **right**?" | "Did I build the **right** model?" |
| **Meaning** | Is the code/implementation correct? Does it match the mathematical equations? Are there bugs? | Does the model accurately represent the real system? Are the assumptions reasonable? Do results match reality? |
| **Focus** | **Internal correctness** (code vs. math) | **External correctness** (model vs. reality) |
| **Example** | You wrote code for \(E = mc^2\) but typed \(E = mc^3\). Verification catches this. | You modeled a bank queue assuming arrivals are uniform, but in reality they follow Poisson. Validation catches this. |

**In short:**
- **Verification** = checking the translation from math to code (no bugs, correct algorithm).
- **Validation** = checking whether the model is a good enough representation of the real system for your objectives.

You can have a perfectly verified model (no bugs) that is completely invalid (wrong assumptions). And you can have a valid conceptual model that is poorly verified (buggy code).