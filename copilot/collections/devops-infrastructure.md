# DevOps & Infrastructure Collection

A suite of specialized agents and prompts designed for SREs, Platform Engineers, and DevOps professionals. These tools enforce industry-standard best practices for security, observability, and infrastructure-as-code.

## 🤖 Agents Included

### [Infrastructure Architect](../../agents/specialized/infrastructure-architect/README.md)

#### **"The Builder"**

- Validates Docker Compose and Kubernetes manifests.
- Enforces immutable infrastructure patterns.
- Prevents configuration drift.

### [Security Guardian](../../agents/specialized/security-guardian/README.md)

#### **"The Auditor"**

- **Zero-Tolerance** for secrets in git.
- Enforces least-privilege container security.
- Validates external secret store patterns (Vault/Consul).

### [Observability Architect](../../agents/specialized/observability-architect/README.md)

#### **"The Watcher"**

- Mandates health checks for all services.
- Checks for Prometheus metric exposure.
- Validates structured logging configurations.

## 🔗 Prompt Chains

- **[Universal Code Review](../../prompts/chains/comprehensive-review-chain.md)**: A full-spectrum code audit chain.
- **[Root Cause Analysis](../../prompts/chains/root-cause-analysis-chain.md)**: A step-by-step debugging wizard for distributed systems.

### 💡 Usage Examples

#### **Scenario: Deployment Failure**

> @workspace Use the **Root Cause Analysis** chain to debug why my frontend container can't reach the postgres database. Here are the logs: [paste logs].

#### **Scenario: Security Audit**

> @workspace Act as the **Security Guardian**. Review this `docker-compose.yml` and tell me if it's safe to commit to a public repository.

#### **Scenario: New Service Setup**

> @workspace Act as the **Infrastructure Architect**. I need to add a Redis cache to this stack. Generate the config ensuring it meets **Observability** standards (health checks + metrics).
