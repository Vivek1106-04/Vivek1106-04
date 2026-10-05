<h1 align="center">Hi, I'm Vivek Gangavarapu</h1>

<p align="center">
  <a href="https://github.com/Vivek1106-04">
    <img src="https://readme-typing-svg.demolab.com?font=Fira+Code&weight=600&size=22&pause=1200&color=2EA44F&center=true&vCenter=true&width=720&lines=I+fix+query+optimizers+in+Apache+Spark;I+build+MCP+servers+for+real+databases;GSoC+2026+%40+Apache+Software+Foundation;59+upstream+PRs+across+12+organisations" alt="Typing intro">
  </a>
</p>

<p align="center">
  <b>I work on the insides of query engines and the tools that let LLM agents talk to them.</b><br>
  B.Tech CSE @ IIIT Kottayam (2027) &middot; Bangalore, India
</p>

<p align="center">
  <a href="https://github.com/pulls?q=author%3AVivek1106-04+is%3Apr+-user%3AVivek1106-04"><img src="https://img.shields.io/badge/upstream_PRs-59-2ea44f?style=for-the-badge&logo=github" alt="Upstream PRs"></a>
  <a href="https://github.com/pulls?q=author%3AVivek1106-04+is%3Apr+is%3Amerged+-user%3AVivek1106-04"><img src="https://img.shields.io/badge/merged-14-8250df?style=for-the-badge&logo=git-merge&logoColor=white" alt="Merged PRs"></a>
  <a href="https://summerofcode.withgoogle.com/programs/2026/projects/9OKlqIS9"><img src="https://img.shields.io/badge/GSoC_2026-Apache-F9AB00?style=for-the-badge&logo=google&logoColor=white" alt="GSoC 2026"></a>
  <a href="https://www.linkedin.com/in/vivek-gangavarapu"><img src="https://img.shields.io/badge/LinkedIn-connect-0A66C2?style=for-the-badge&logo=linkedin" alt="LinkedIn"></a>
</p>

<h3 align="center">Code I've shipped into</h3>

<p align="center">
  <a href="https://github.com/apache/spark/pulls?q=author%3AVivek1106-04"><img src="https://github.com/apache.png" width="56" alt="Apache" title="Apache Spark, AsterixDB, SeaTunnel"></a>&nbsp;&nbsp;
  <a href="https://github.com/google/adk-go/pulls?q=author%3AVivek1106-04"><img src="https://github.com/google.png" width="56" alt="Google" title="Google ADK"></a>&nbsp;&nbsp;
  <a href="https://github.com/quantumlib/Cirq/pulls?q=author%3AVivek1106-04"><img src="https://github.com/quantumlib.png" width="56" alt="Google Quantum AI" title="Google Cirq"></a>&nbsp;&nbsp;
  <a href="https://github.com/google-gemini/gemini-cli/pulls?q=author%3AVivek1106-04"><img src="https://github.com/google-gemini.png" width="56" alt="Gemini" title="Gemini CLI"></a>&nbsp;&nbsp;
  <a href="https://github.com/ClickHouse/clickhouse-connect/pulls?q=author%3AVivek1106-04"><img src="https://github.com/ClickHouse.png" width="56" alt="ClickHouse" title="ClickHouse"></a>&nbsp;&nbsp;
  <a href="https://github.com/databricks/cli/pulls?q=author%3AVivek1106-04"><img src="https://github.com/databricks.png" width="56" alt="Databricks" title="Databricks CLI"></a>
</p>

---

### What I'm doing right now

- **Apache SeaTunnel** - reworking checkpoint scheduling in the Zeta engine: shared trigger scheduling across pipelines ([STIP-40](https://github.com/apache/seatunnel/issues/12339)), lock contention during savepoints, and force-stop futures that never complete.
- **Google ADK for Go** - hunting agent-runtime bugs: lost session state under concurrent appends, loop agents that keep running after a sub-agent fails, SSE timeouts. 4 fixes merged, more in review.
- **Apache Spark** - Catalyst optimizer correctness fixes and new SQL functions (12 PRs open).
- **B.Tech thesis** - a component-swappable LLM agent harness, studying how memory representation changes long-horizon task success and token cost.

---

### Upstream contributions

| Project | What I did | Links |
|---|---|---|
| <img src="https://github.com/apache.png" width="16"> **Apache Spark** | Added `gcd` / `lcm` SQL functions with Catalyst codegen, ANSI overflow semantics, Scala + PySpark APIs. Fixed optimizer correctness bugs in `ReplaceExceptWithFilter`, `LimitPushDown`, and `Expand` pre-aggregation. Enabled shuffle skew accounting so AQE can actually see skew. BloomFilter hot-path speedup. | [#58242](https://github.com/apache/spark/pull/58242) [#57528](https://github.com/apache/spark/pull/57528) [#58046](https://github.com/apache/spark/pull/58046) [#58065](https://github.com/apache/spark/pull/58065) [#58102](https://github.com/apache/spark/pull/58102) [all 12](https://github.com/apache/spark/pulls?q=author%3AVivek1106-04) |
| <img src="https://github.com/apache.png" width="16"> **Apache AsterixDB** (GSoC) | `function_metadata()` datasource function exposing the runtime function registry as queryable rows. MCP assistant panel in the cluster dashboard (~4.7k lines) that answers questions and runs SQL++ against the live cluster. Admin and Connector API docs. Patches landed via Gerrit. | [#51](https://github.com/apache/asterixdb/pull/51) [#52](https://github.com/apache/asterixdb/pull/52) [#48](https://github.com/apache/asterixdb/pull/48) |
| <img src="https://github.com/apache.png" width="16"> **Apache SeaTunnel** | Checkpoint scheduling benchmark (merged), shared trigger scheduling, cooperative worker budgeting, savepoint lock fix, force-stop future fix. Filed the design proposal STIP-40 and 3 bug reports. | [#12418](https://github.com/apache/seatunnel/pull/12418) [#12165](https://github.com/apache/seatunnel/pull/12165) [#12511](https://github.com/apache/seatunnel/pull/12511) [#12623](https://github.com/apache/seatunnel/pull/12623) |
| <img src="https://github.com/ClickHouse.png" width="16"> **ClickHouse** `clickhouse-connect` | Merged a fix so the server-side parameter binder accepts `$` in placeholder names. Before, those queries silently fell back to client-side formatting and went out with no bound parameters. | [#948](https://github.com/ClickHouse/clickhouse-connect/pull/948) |
| <img src="https://github.com/google.png" width="16"> **Google ADK (Go)** | Persisted input/output transcriptions in the database session service, fixed a zero SSE write timeout that failed every response, made flaky tests repeatable. Open: state-row locking in `AppendEvent`, workflow agents stopping on sub-agent error, remote-agent error propagation. | [#1662](https://github.com/google/adk-go/pull/1662) [#1686](https://github.com/google/adk-go/pull/1686) [#1743](https://github.com/google/adk-go/pull/1743) [#1684](https://github.com/google/adk-go/pull/1684) [all 9](https://github.com/google/adk-go/pulls?q=author%3AVivek1106-04) |
| <img src="https://github.com/databricks.png" width="16"> **Databricks CLI** | Serialized U2M OAuth token refreshes across processes. Rejected symlinked directories in templates. | [#6759](https://github.com/databricks/cli/pull/6759) [#6758](https://github.com/databricks/cli/pull/6758) |
| <img src="https://github.com/quantumlib.png" width="16"> **Google Cirq** | 7 merged: `drop_diagonal_before_measurement` transformer, qubit routing on directed device graphs, recursive `CircuitOperation` support, `Gateset.__contains__` crash on unhashable gates. | [#7790](https://github.com/quantumlib/Cirq/pull/7790) [#7810](https://github.com/quantumlib/Cirq/pull/7810) [#7843](https://github.com/quantumlib/Cirq/pull/7843) [#7963](https://github.com/quantumlib/Cirq/pull/7963) [all](https://github.com/quantumlib/Cirq/pulls?q=author%3AVivek1106-04+is%3Amerged) |
| **Also** | Gemini CLI, Omnigent, Qiskit | [gemini-cli](https://github.com/google-gemini/gemini-cli/pulls?q=author%3AVivek1106-04) [omnigent](https://github.com/omnigent-ai/omnigent/pulls?q=author%3AVivek1106-04) |

---

### Things I built

<table>
<tr>
<td width="33%" valign="top">

**[asterixdb-mcp-server](https://github.com/Vivek1106-04/asterixdb-mcp-server)**<br>
<sub>GSoC 2026 &middot; Python &middot; MCP</sub>

Model Context Protocol gateway for Apache AsterixDB. 26 tools, 12 resources, 6 prompts over JSON-RPC 2.0: sync/async SQL++, plan introspection, index advice, schema discovery. OAuth 2.1 (JWKS), multi-tenant isolation, stdio + HTTP transports. 650+ tests at 100% line and branch coverage. Architecture accepted as APE 36.

</td>
<td width="33%" valign="top">

**[agentdb](https://github.com/Vivek1106-04/agentdb)**<br>
<sub>Python &middot; ClickHouse &middot; Databricks</sub>

NL-to-SQL context layer that gives agents a warehouse's *physical* design (sort keys, partitions, column stats) instead of a schema dump. **4.0x fewer bytes read** on a 100M-row ClickBench table. Flags Delta Lake filters outside the 32-column data-skipping window. Ships `agenteval`: 160 tasks over TPC-H + ClickBench, 1,344 tests.

</td>
<td width="33%" valign="top">

**[borgpilot](https://github.com/Vivek1106-04/borgpilot)**<br>
<sub>Python &middot; AsterixDB &middot; Anthropic SDK</sub>

Autonomous SRE agent on Google Borg 2019 traces. Zero hardcoded SQL: it discovers the schema and writes SQL++ itself. Isolated 1 faulty host in a 10,001-machine fleet in 156 ms. Gradient-boosted failure-risk model at 0.897 ROC-AUC; rightsizing engine over 25.7M events.

</td>
</tr>
</table>

---

### Tech I work with

**Languages** &nbsp;
![Python](https://img.shields.io/badge/Python-3776AB?style=flat-square&logo=python&logoColor=white)
![Scala](https://img.shields.io/badge/Scala-DC322F?style=flat-square&logo=scala&logoColor=white)
![Java](https://img.shields.io/badge/Java-ED8B00?style=flat-square&logo=openjdk&logoColor=white)
![Go](https://img.shields.io/badge/Go-00ADD8?style=flat-square&logo=go&logoColor=white)
![TypeScript](https://img.shields.io/badge/TypeScript-3178C6?style=flat-square&logo=typescript&logoColor=white)
![SQL](https://img.shields.io/badge/SQL%20%2F%20SQL%2B%2B-4479A1?style=flat-square&logo=postgresql&logoColor=white)

**Engines** &nbsp;
![Apache Spark](https://img.shields.io/badge/Spark-E25A1C?style=flat-square&logo=apachespark&logoColor=white)
![ClickHouse](https://img.shields.io/badge/ClickHouse-FFCC01?style=flat-square&logo=clickhouse&logoColor=black)
![Databricks](https://img.shields.io/badge/Databricks-FF3621?style=flat-square&logo=databricks&logoColor=white)
![Delta Lake](https://img.shields.io/badge/Delta_Lake-003366?style=flat-square)
![AsterixDB](https://img.shields.io/badge/AsterixDB-D22128?style=flat-square&logo=apache&logoColor=white)
![SeaTunnel](https://img.shields.io/badge/SeaTunnel-1E88E5?style=flat-square&logo=apache&logoColor=white)

**Agents & infra** &nbsp;
![MCP](https://img.shields.io/badge/Model_Context_Protocol-000000?style=flat-square)
![Docker](https://img.shields.io/badge/Docker-2496ED?style=flat-square&logo=docker&logoColor=white)
![Kubernetes](https://img.shields.io/badge/Kubernetes-326CE5?style=flat-square&logo=kubernetes&logoColor=white)
![GitHub Actions](https://img.shields.io/badge/GitHub_Actions-2088FF?style=flat-square&logo=githubactions&logoColor=white)
![pytest](https://img.shields.io/badge/pytest-0A9EDC?style=flat-square&logo=pytest&logoColor=white)

---

### Ask me about

Catalyst optimizer rules &middot; MergeTree sort keys and data skipping &middot; reading `EXPLAIN` plans &middot; building MCP servers that are safe to point at a real database &middot; getting a first PR into an Apache project

<p align="center">
  <picture>
    <source media="(prefers-color-scheme: dark)" srcset="https://raw.githubusercontent.com/Vivek1106-04/Vivek1106-04/output/github-snake-dark.svg">
    <img src="https://raw.githubusercontent.com/Vivek1106-04/Vivek1106-04/output/github-snake.svg" alt="Contribution snake">
  </picture>
</p>

<p align="center"><sub>If something here overlaps with what you're building, open an issue on any of my repos or reach out on LinkedIn.</sub></p>
