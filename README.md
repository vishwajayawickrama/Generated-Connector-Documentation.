# WSO2 Integrator Connector Documentation

AI-generated step-by-step integration guides for WSO2 Integrator: BI connectors, produced using an AI agentic workflow. Each guide documents the complete low-code canvas workflow — from project creation to verifying the final integration — with accompanying screenshots.

---

## How These Docs Were Generated

All guides in this repository were created by an AI agent that:

1. Operated a live **WSO2 Integrator: BI** environment running inside VS Code (code-server)
2. Performed every action through the low-code canvas UI — no `.bal` files were edited manually
3. Captured screenshots at each step to illustrate the workflow
4. Produced structured Markdown documentation describing each configuration step

---

## Connectors Covered

| Connector | Version | Guide |
|---|---|---|
| **Kafka Consumer** (`ballerinax/kafka`) | Swan Lake | [kafka-consumer-integration-creation-guide.md](kafka-consumer-connector-documentation/workflow-docs/kafka-consumer-integration-creation-guide.md) |
| **Redis** (`ballerinax/redis`) | `3.1.0` | [redis-connection-set-operation-guide.md](redis-connector-documentation/workflow-docs/redis-connection-set-operation-guide.md) |
| **Snowflake** (`ballerinax/snowflake`) | `2.2.0` | [snowflake-connector-guide.md](snowflake-connector-documentation/workflow-docs/snowflake-connector-guide.md) |

---

## Repository Structure

```
.
├── kafka-consumer-connector-documentation/
│   ├── screenshots/          # Step-by-step UI screenshots
│   └── workflow-docs/        # Markdown integration guide
├── redis-connector-documentation/
│   ├── screenshots/
│   └── workflow-docs/
└── snowflake-connector-documentation/
    ├── screenshots/
    └── workflow-docs/
```

---

## Prerequisites (Common)

- **WSO2 Integrator: BI** extension installed in VS Code or code-server
- **Ballerina Swan Lake** (version varies per guide — see individual guides)
- Network access to [Ballerina Central](https://central.ballerina.io) for pulling connector modules

---

> **Note:** Any credentials shown in these guides (usernames, passwords, account identifiers) are placeholder values for illustration purposes only. Replace them with your own credentials before use.
