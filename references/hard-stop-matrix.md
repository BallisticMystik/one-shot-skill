# Hard-Stop Matrix

Stop and ask for explicit approval when any item below is encountered. Approval should describe the decision, affected files/contracts, and expected risk.

## Governance Stops

| Trigger | Required Approval |
|---|---|
| Create, activate, archive, or re-scope a sidechain | Sidechain approval |
| Modify locked `task_plan.md`, `analysis.md`, `spec.md`, or `findings.md` | Locked-plan amendment approval |
| Governance files disagree | User decision on precedence |
| Checkpoint claims completion or phase close | Checkpoint review approval |
| Scope expands into another sidechain | Scope expansion approval |

## Safety Stops

| Trigger | Required Approval |
|---|---|
| New autonomous signing payload, dispatch source, or signing semantics | Threat-model approval |
| Cap, risk, leverage, loss-limit, or guard policy change | Safety policy approval |
| Real-fund, mainnet, armed-mode, or testnet execution with value at risk | Execution approval |
| Health scan acts across user/session boundaries | Architecture/safety approval |
| Crash recovery behavior is ambiguous | Recovery design approval |

## Engineering Stops

| Trigger | Required Approval |
|---|---|
| New dependency or framework | Dependency approval |
| Destructive git operation | Git operation approval |
| Schema change with unclear consumers | Contract approval |
| Invariant must be weakened to proceed | Invariant exception approval |
| Tests cannot run and risk is non-trivial | Verification exception approval |

## Product/Design Stops

| Trigger | Required Approval |
|---|---|
| New product direction or UX workflow | Product approval |
| Material visual direction change after styleguide is accepted | Design approval |
| Accessibility or mobile behavior tradeoff | UX risk approval |
| Animation/interaction that could obscure operational data | Operator UX approval |

## Stop Message Format

Use this format:

```text
Hard stop: <trigger>
Current source of truth: <file/path:line if available>
Conflict or decision needed: <specific choice>
Recommended option: <one recommendation with reason>
Impact if approved: <files/contracts/tests affected>
```
