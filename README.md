# AI Agent Engineering Standard

> **English** · [**Español**](README_ES.md)

A normative specification of **32 documents** that defines how AI agents should behave in software engineering tasks: how to reason, what evidence to demand, when to stop iterating, and which technical rules to apply.

## What problem does it solve?

AI agents produce inconsistent results: they assert confidently without evidence, iterate without a stopping criterion, generate interfaces with an "AI tell," and violate architecture, security and testing principles. This standard turns agent behavior into an **auditable and verifiable specification**, not a list of good intentions.

## Structure

7 levels (0–6) and 32 documents. The single navigation point is the **Master Index (32)**.

| Level | Content | Documents |
| :--- | :--- | :--- |
| 0 | Constitution and supreme principles | 00 |
| 1 | Operative protocol, cognitive model, context | 01, 02, 04–11, 24 |
| 2 | Writing and communication rules | 03, 12, 13 |
| 3 | Technical specializations | 14–23 |
| 4 | Audit | 25 |
| 5 | Governance and evolution | 26–30 |
| 6 | Glossary and index | 31, 32 |

### Documents

| ID | Name | Purpose |
| :--- | :--- | :--- |
| **00** | Agent Constitution | Supreme, immutable principles (evidence over probability). |
| **01** | Agent Operative Protocol | Mandatory execution flow (Reception → Delivery). |
| **02** | Convergence Policy | When to stop iterating and accept a solution. |
| **03** | Writing Rules | Remove LLM patterns and maximize information density. |
| **04** | Cognitive Model | How to reason (deliberative, hierarchical, systemic). |
| **05** | Epistemic Model | How to evaluate evidence, knowledge and uncertainty. |
| **06** | Iterative Reasoning Protocol (IRP) | Internal review loops (Understanding → Self-criticism). |
| **07** | Subagent System (SSA) | Specialized roles (Architect, Backend, UX…). |
| **08** | Context Management Protocol | Manage working memory and task focus. |
| **09** | Project Awareness (PAP) | Understand the system before intervening. |
| **10** | Conflict Resolution Matrix | Precedence hierarchy between rules. |
| **11** | New Projects and Initial Context (Onboarding) | Process PRD, TRD and context documents. |
| **12** | Prompt Engineering and User Communication | How to ask, confirm and handle ambiguity. |
| **13** | Generative AI: Biases and Discipline | Recognize and correct model biases. |
| **14** | Visual Design Anti-patterns | Avoid generic interfaces and the "AI tell". |
| **15** | Frontend Engineering | Component, state and rendering rules. |
| **16** | Backend Engineering | Domain, service and business logic rules. |
| **17** | Software Architecture | Structure, layers, patterns and cohesion. |
| **18** | Database | Modeling, queries, migrations and integrity. |
| **19** | APIs and Contracts | Endpoint design, versioning and compatibility. |
| **20** | Security | Authentication, authorization, encryption and OWASP. |
| **21** | Observability and Resilience | Logs, metrics, traces, timeouts, circuit breakers. |
| **22** | Strategic Testing Management | Test pyramid, mocks, TDD, coverage, mutation, UAT, CI gates. |
| **23** | Advanced Engineering Principles | DDD, Hexagonal, SOLID, DRY/KISS/YAGNI, cyclomatic complexity. |
| **24** | Project Memory and Continuous Improvement | Decision Log, Known Problems, retrospectives. |
| **25** | Audit System | Final verification of standard compliance. |
| **26** | RFC System | Formal process for modifying the standard. |
| **27** | Standard Governance | Evolution and stability principles. |
| **28** | Normative Language | Definition of MUST, MUST NOT, MAY. |
| **29** | Standard Architecture | Templates, identifiers and document structure. |
| **30** | Git/GitHub Policy | Secrets, commits, exclusion files. |
| **31** | Glossary | Official definitions of technical terms. |
| **32** | Master Index | Navigation and global map of the standard. |

## How to use

**With an AI agent (recommended):** point the agent to this repository and instruct it to adopt the standard. The agent must read the documents in the order defined by the **Master Index reading flow (32)** and comply with the **Constitution (00)** and the **Operative Protocol (01)** in every task.

**As a human auditor:** use the **Audit System (25)** to verify that the agent's work complies with the standard before accepting it.

**To apply technical rules:** consult the specializations (14–23). Each rule includes priority, normative statement and verification method.

## Governance

- The standard evolves only through **RFCs** (26). It is never edited directly.
- Semantic versioning **MAJOR.MINOR.PATCH** (27, GV-006).
- Mandatory normative language (28): `MUST`, `MUST NOT`, `MAY`.
- Terms defined in the **Glossary (31)**.

## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md). Every proposal requires an RFC with the fields: Problem, Evidence, Impact, Proposed solution, Compatibility, Risks and Initial state.

## Security

Report vulnerabilities through [SECURITY.md](SECURITY.md). Publishing secrets or sensitive data in public issues is prohibited.

## License

**Creative Commons Attribution 4.0 International (CC BY 4.0)** — see [LICENSE](LICENSE).