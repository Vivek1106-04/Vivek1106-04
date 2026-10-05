<h1 align="center">Vivek Gangavarapu</h1>

<p align="center">
  <b>I find and fix correctness bugs in query optimizers, distributed runtimes, and agent frameworks.</b><br>
  Then I build the tools that let LLM agents use those systems safely.
</p>

<p align="center">
  GSoC 2026 @ Apache Software Foundation &middot; B.Tech CSE @ IIIT Kottayam (2027) &middot; Bangalore, India
</p>

<p align="center">
  <a href="https://github.com/pulls?q=author%3AVivek1106-04+is%3Apr+-user%3AVivek1106-04"><img src="https://img.shields.io/badge/upstream_PRs-59-2ea44f?style=for-the-badge&logo=github" alt="Upstream PRs"></a>
  <a href="https://github.com/pulls?q=author%3AVivek1106-04+is%3Apr+is%3Amerged+-user%3AVivek1106-04"><img src="https://img.shields.io/badge/merged-14-8250df?style=for-the-badge&logo=git-merge&logoColor=white" alt="Merged PRs"></a>
  <a href="https://summerofcode.withgoogle.com/programs/2026/projects/9OKlqIS9"><img src="https://img.shields.io/badge/GSoC_2026-Apache_AsterixDB-F9AB00?style=for-the-badge&logo=google&logoColor=white" alt="GSoC 2026"></a>
  <a href="https://www.linkedin.com/in/vivek-gangavarapu"><img src="https://img.shields.io/badge/LinkedIn-connect-0A66C2?style=for-the-badge&logo=linkedin" alt="LinkedIn"></a>
</p>

<p align="center">
  <sub><b>Contributing to</b> &nbsp; Apache Spark &middot; Apache AsterixDB &middot; Apache SeaTunnel &middot; ClickHouse &middot; Databricks CLI &middot; Google ADK &middot; Google Cirq &middot; Gemini CLI</sub>
</p>

---

## Selected upstream work

I usually start from a wrong answer, a hang, or lost data. I reduce it to a minimal repro, write the failing test, and fix the root cause. Each fix below lists the bug, what it broke, and the change. Merged PRs are marked; the rest are in review.

### Query optimizer correctness &nbsp;<sub>Apache Spark (Catalyst, AQE)</sub>

- **`ReplaceExceptWithFilter` bound the wrong filter**: it matched by name instead of expression id, so `EXCEPT` could return wrong rows. [#58046](https://github.com/apache/spark/pull/58046)
- **`LimitPushDown` stripped a `GlobalLimit` whose cap isn't statically known**, which changed query results. [#58065](https://github.com/apache/spark/pull/58065)
- **Pre-aggregation under `Expand` was unsound** in two cases (duplicate-sensitive aggregates, and empty grouping) and produced wrong `GROUPING SETS` / `CUBE` answers. [#58102](https://github.com/apache/spark/pull/58102) [#58154](https://github.com/apache/spark/pull/58154)
- **`SELECT * EXCEPT` on a nested field lost struct nullness.** [#58477](https://github.com/apache/spark/pull/58477)
- **AQE couldn't see shuffle skew**: skewed block sizes are now recorded by default so adaptive execution can split skewed partitions. [#57528](https://github.com/apache/spark/pull/57528)
- **New SQL functions `gcd` / `lcm`**: Catalyst codegen, ANSI overflow semantics, Scala + PySpark APIs. [#58242](https://github.com/apache/spark/pull/58242)
- Also: DSv2 runtime-filter pushdown, BloomFilter hot-path bitmasking, Spark Connect pipeline dependency planning. [all 12 &rarr;](https://github.com/apache/spark/pulls?q=author%3AVivek1106-04)

### Concurrency and distributed runtimes &nbsp;<sub>SeaTunnel Zeta, Google ADK, Databricks CLI</sub>

- **SeaTunnel: `startSavepoint` held the coordinator lock through a sleep-poll**, which blocked every concurrent checkpoint trigger. I filed the bug and moved the wait outside the lock. [#12511](https://github.com/apache/seatunnel/pull/12511)
- **SeaTunnel: one unexpected throw silently stopped periodic checkpointing** for a pipeline. [issue #12442](https://github.com/apache/seatunnel/issues/12442)
- **SeaTunnel: force-stopped tasks never completed their future**, so job shutdown hung. [#12623](https://github.com/apache/seatunnel/pull/12623)
- **SeaTunnel: design proposal [STIP-40](https://github.com/apache/seatunnel/issues/12339)** to share checkpoint trigger scheduling across all pipelines on a member, plus the benchmark that measures it. `merged` [#12418](https://github.com/apache/seatunnel/pull/12418) [#12165](https://github.com/apache/seatunnel/pull/12165)
- **Google ADK: concurrent appends from different sessions lost `app:` / `user:` state.** The fix locks the state rows in `AppendEvent`. [#1743](https://github.com/google/adk-go/pull/1743)
- **Databricks CLI: parallel processes raced on OAuth U2M token refresh.** Refreshes are now serialized across processes. [#6759](https://github.com/databricks/cli/pull/6759)

### Agent runtimes &nbsp;<sub>Google ADK (Go), Gemini CLI, Omnigent</sub>

- **Session database dropped input/output transcriptions.** `merged` [#1662](https://github.com/google/adk-go/pull/1662)
- **A zero SSE write timeout made every streamed response fail.** `merged` [#1686](https://github.com/google/adk-go/pull/1686)
- **`LoopAgent` / `SequentialAgent` kept running after a sub-agent error**, and remote agents reported failures as events instead of errors. [#1684](https://github.com/google/adk-go/pull/1684) [#1740](https://github.com/google/adk-go/pull/1740)
- **Tests hung on macOS or failed under `-count=N`.** Both are fixed and the tests are repeatable. `merged` [#1638](https://github.com/google/adk-go/pull/1638) [#1657](https://github.com/google/adk-go/pull/1657)
- **Gemini CLI: the agent continued its loop after the user interrupted it.** [#19938](https://github.com/google-gemini/gemini-cli/pull/19938)

### Database drivers and engines &nbsp;<sub>ClickHouse, Apache AsterixDB</sub>

- **ClickHouse Python driver: `$` in parameter names silently disabled server-side binding**, so queries went out with no bound parameters. `merged` [#948](https://github.com/ClickHouse/clickhouse-connect/pull/948)
- **AsterixDB: `function_metadata()`** exposes the engine's runtime function registry as queryable, filterable rows. The change spans the compiler, metadata, and runtime layers of a million-line Java engine. [#51](https://github.com/apache/asterixdb/pull/51)
- **AsterixDB: an MCP assistant panel in the cluster dashboard** that answers questions and runs SQL++ against the live cluster. [#52](https://github.com/apache/asterixdb/pull/52)

### Quantum compilation &nbsp;<sub>Google Cirq, 7 merged</sub>

- Qubit routing on **directed device graphs**, a new `drop_diagonal_before_measurement` transformer, recursive `CircuitOperation` support, and a fix for `Gateset.__contains__` crashing on unhashable gates. `merged` [#7810](https://github.com/quantumlib/Cirq/pull/7810) [#7889](https://github.com/quantumlib/Cirq/pull/7889) [#7790](https://github.com/quantumlib/Cirq/pull/7790) [#7843](https://github.com/quantumlib/Cirq/pull/7843) [#7963](https://github.com/quantumlib/Cirq/pull/7963)

---

## Things I built

<table>
<tr>
<td width="33%" valign="top">

### [asterixdb-mcp-server](https://github.com/Vivek1106-04/asterixdb-mcp-server)
<sub>GSoC 2026 &middot; Python &middot; MCP</sub>

A production MCP gateway for Apache AsterixDB.

- 26 tools, 12 resources, 6 prompts over JSON-RPC 2.0
- OAuth 2.1 with JWKS and DNS-rebinding protection
- Multi-tenant isolation, stdio + HTTP transports
- **650+ tests, 100% line and branch coverage**
- Architecture accepted upstream as **APE 36**

</td>
<td width="33%" valign="top">

### [agentdb](https://github.com/Vivek1106-04/agentdb)
<sub>Python &middot; ClickHouse &middot; Databricks</sub>

An NL-to-SQL context layer that gives agents the warehouse's *physical* design, not a schema dump.

- **4.0x fewer bytes read** on 100M-row ClickBench by grounding queries in the MergeTree sort key
- Flags Delta Lake filters that silently miss data skipping
- `agenteval`: 160 tasks, TPC-H + ClickBench, **1,344 tests**, mypy --strict

</td>
<td width="33%" valign="top">

### [borgpilot](https://github.com/Vivek1106-04/borgpilot)
<sub>Python &middot; AsterixDB &middot; Claude</sub>

An autonomous SRE agent for root-cause analysis on Google Borg 2019 traces.

- Zero hardcoded SQL: discovers the schema and writes its own SQL++
- **Found 1 faulty host among 10,001 machines in 156 ms**
- Failure-risk model at **0.897 ROC-AUC**
- 1,409 rightsizing decisions over 25.7M events

</td>
</tr>
</table>

---

## How I work

- **Repro first.** Every fix comes with a failing test that the fix turns green.
- **Measure, don't guess.** I benchmark performance claims (bytes read, scheduling delay, latency) and commit the harness.
- **Design before code** on anything structural, as in [STIP-40](https://github.com/apache/seatunnel/issues/12339) for SeaTunnel and APE 36 for AsterixDB.
- **Coverage as a contract**: 100% line and branch coverage, enforced in CI on my own projects.

## Stack

![Python](https://img.shields.io/badge/Python-3776AB?style=flat-square&logo=python&logoColor=white)
![Scala](https://img.shields.io/badge/Scala-DC322F?style=flat-square&logo=scala&logoColor=white)
![Java](https://img.shields.io/badge/Java-ED8B00?style=flat-square&logo=openjdk&logoColor=white)
![Go](https://img.shields.io/badge/Go-00ADD8?style=flat-square&logo=go&logoColor=white)
![TypeScript](https://img.shields.io/badge/TypeScript-3178C6?style=flat-square&logo=typescript&logoColor=white)
![SQL](https://img.shields.io/badge/SQL%20%2F%20SQL%2B%2B-4479A1?style=flat-square&logo=postgresql&logoColor=white)
![Apache Spark](https://img.shields.io/badge/Spark-E25A1C?style=flat-square&logo=apachespark&logoColor=white)
![ClickHouse](https://img.shields.io/badge/ClickHouse-FFCC01?style=flat-square&logo=clickhouse&logoColor=black)
![Databricks](https://img.shields.io/badge/Databricks-FF3621?style=flat-square&logo=databricks&logoColor=white)
![MCP](https://img.shields.io/badge/Model_Context_Protocol-000000?style=flat-square)
![Docker](https://img.shields.io/badge/Docker-2496ED?style=flat-square&logo=docker&logoColor=white)
![Kubernetes](https://img.shields.io/badge/Kubernetes-326CE5?style=flat-square&logo=kubernetes&logoColor=white)

<p align="center"><sub>Working on query engines, data infrastructure, or agent runtimes? I'd like to hear about it. Reach me on <a href="https://www.linkedin.com/in/vivek-gangavarapu">LinkedIn</a>.</sub></p>
