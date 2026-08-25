# NetApp MCP servers

## Give AI agents useful, governed access to your data estate

NetApp Model Context Protocol (MCP) servers connect AI assistants and agents to
storage operations, infrastructure telemetry, and enterprise data. Use this
catalog to choose the server that matches the outcome you need—not simply the
product you own.

## Choose by outcome

| What you want an AI agent to do | Start with | Why |
| --- | --- | --- |
| Administer ONTAP across one or more clusters | [ONTAP MCP Server](#ontap-mcp-server) | Broad ONTAP administration across NAS, SAN, NVMe, data protection, and core storage services |
| Identify infrastructure problems, investigate performance, and plan capacity | [Harvest MCP Server](#harvest-mcp-server) | Uses current and historical Harvest telemetry from Prometheus or VictoriaMetrics across ONTAP, E-Series, and StorageGRID; Cisco Nexus adds ecosystem visibility |
| Manage Google Cloud NetApp Volumes end to end | [Google Cloud NetApp Volumes MCP Server](#google-cloud-netapp-volumes-mcp-server) | Broad GCNV control-plane coverage, including pools, protection, security, NAS, and iSCSI |
| Give agents semantic access to content indexed by AIDE | [AI Data Engine MCP Server](#ai-data-engine-aide-mcp-server) | Reuses AIDE's vector search to ground agent responses in relevant enterprise content |
| Search existing file shares while preserving user permissions | [NetApp Neo MCP Server](#netapp-neo-mcp-server-early-access) | Makes indexed SMB, NFS, and S3 content available to AI with identity-aware access control |
| Provision, clone, and protect datasets or workspaces | [NetApp DataOps Toolkit MCP server family](#netapp-dataops-toolkit-mcp-server-family) | Four task-focused MCP servers for ONTAP, Azure NetApp Files, Google Cloud NetApp Volumes, and Kubernetes, with self-service workflows for developers, data scientists, and platform teams |

## MCP server details

### ONTAP MCP Server

**Move from storage advice to storage action.** Give AI agents a validated,
centrally managed path to discover and operate ONTAP instead of relying on
generated scripts or making users translate recommendations into manual steps.

- **Use it when:** Storage and infrastructure teams need broad administration,
  multi-cluster workflows, or a shared MCP service for ONTAP.
- **Coverage:** API discovery and read access, volumes, SVMs, qtrees, snapshots,
  snapshot policies, SnapMirror, QoS, NFS, SMB/CIFS, LUNs and igroups, iSCSI,
  FCP, NVMe, DNS, and network interfaces. A read-only mode is available when
  agents should inspect but not change the environment.
- **Runs as:** A self-hosted Streamable HTTP service, distributed as a container
  image and Helm chart.
- **Works with:** NetApp AFX, AFF, FAS, Amazon FSx for NetApp ONTAP, Cloud
  Volumes ONTAP, and ONTAP Select.
- **Start here:** [Documentation](https://netapp.github.io/ontap-mcp/latest/) ·
  [Source](https://github.com/NetApp/ontap-mcp)

### Harvest MCP Server

**Turn infrastructure telemetry into decisions.** Ask which systems need
attention, where latency is rising, or when capacity will run out—without
manually navigating dashboards or writing PromQL. Harvest spans ONTAP, E-Series,
and StorageGRID, with Cisco Nexus providing additional ecosystem visibility, so
each answer draws on portfolio-wide telemetry history collected by Harvest and
stored in the deployment's Prometheus or VictoriaMetrics database. That observed
history—health, capacity, performance, alerts, and trends—improves problem
diagnosis and grounds recommendations and subsequent management actions.
Harvest MCP queries the time-series database; it does not serve as the database
or change infrastructure configuration.

- **Use it when:** Operations teams need portfolio-wide health summaries,
  active-alert context, capacity analysis, performance investigation and
  problem diagnosis, or trend-based planning grounded in current and historical
  telemetry—or when an LLM or AI agent needs that trusted, portfolio-wide
  context to guide decisions and inform actions it performs through other
  active-management MCP servers.
- **Coverage:** Current and historical telemetry collected by Harvest from
  ONTAP, E-Series, and StorageGRID storage systems, plus Cisco Nexus switches
  for ecosystem visibility. Harvest MCP queries this data from Prometheus or
  VictoriaMetrics to analyze health, capacity, latency, IOPS, throughput,
  alerts, and growth trends; it does not change storage configuration.
- **Runs as:** Local stdio or self-hosted HTTP, distributed as a container image
  or native binary.
- **Works with:** An existing Harvest deployment and its Prometheus or
  VictoriaMetrics time-series store.
- **Start here:** [Documentation][harvest-docs] · [Source][harvest-source]

Harvest MCP supports observe-to-act infrastructure-management workflows by
helping identify, diagnose, and explain problems evident in health, capacity,
performance, alerts, and trends. Pair it with the relevant active management
MCP server—for example, ONTAP MCP—to execute an approved action.

### Google Cloud NetApp Volumes MCP Server

**Give AI agents broad, Google Cloud-native control of enterprise storage.**
This is the GCNV choice for platform and infrastructure teams that need more
than dataset provisioning: it spans capacity pools, data services, protection,
identity integration, encryption, and block and file storage.

- **Use it when:** You want comprehensive GCNV resource management from Cursor,
  Gemini CLI, Claude, or another MCP client.
- **Coverage:** Storage pools; NFS, SMB, and iSCSI volumes; snapshots; backup
  vaults, backups, and backup policies; replication; Active Directory; KMS
  configurations; quota rules; host groups; and long-running operations.
  ONTAP-mode pools also provide guarded access to supported ONTAP REST
  operations. Delete operations are intentionally excluded.
- **Runs as:** Local stdio or self-hosted HTTP/SSE, distributed as the
  `gcnv-mcp-server` npm package.
- **Works with:** Google Cloud NetApp Volumes, including ONTAP-mode storage
  pools.
- **Start here:** [Source and setup](https://github.com/NetApp/gcnv-mcp-server)

### AI Data Engine (AIDE) MCP Server

**Ground AI responses in content already indexed by AIDE.** The server exposes
AIDE's vector-based semantic search through MCP, allowing an agent to retrieve
the documents most relevant to a user's question.

- **Use it when:** You already use NetApp AI Data Engine and want an MCP client
  to use its RAG search as a source of enterprise context.
- **Coverage:** A focused `netapp_data_engine_search` tool for semantic document
  retrieval through the AIDE RAG API. It retrieves content; it does not manage
  storage or ingest data.
- **Runs as:** A local stdio server, distributed as the `netapp-aide-mcp`
  Python package.
- **Works with:** NetApp AI Data Engine.
- **Start here:** [Source and setup][aide-source] ·
  [AIDE documentation][aide-docs]

### NetApp Neo MCP Server (Early Access)

**Make existing enterprise file content useful to AI without migrating the
underlying storage or weakening file permissions.** NetApp Neo indexes
unstructured data and exposes permission-aware search and retrieval to a broad
set of AI platforms.

- **Use it when:** You need an on-premises or sovereign path from enterprise
  file shares to ChatGPT Enterprise, Claude, Azure AI, Google agent platforms,
  or custom agents.
- **Coverage:** File and full-text search, windowed content retrieval, share
  discovery, and named-entity search across indexed SMB, NFS, and S3 data.
  Results can be filtered using existing ACLs mapped to Microsoft Entra
  identities.
- **Runs as:** A Streamable HTTP endpoint within the containerized NetApp Neo
  deployment, with OAuth 2.0 or API-key authentication.
- **Works with:** NetApp Neo and the file shares it has indexed.
- **Start here:** [MCP guide][neo-mcp] ·
  [NetApp Neo overview][neo-overview] · [Source][neo-source]

Choose AIDE when semantic retrieval from an existing AIDE knowledge base is the
goal. Choose Neo when you need to crawl file shares, preserve file-level access,
and expose search and content retrieval to multiple AI ecosystems.

### NetApp DataOps Toolkit MCP server family

**Shorten the path from a data request to a usable dataset or workspace.**
This family contains four individual, task-focused MCP servers—one each for
ONTAP, Azure NetApp Files, Google Cloud NetApp Volumes, and Kubernetes—not one
cross-platform server. These focused, local MCP servers expose repeatable
DataOps workflows to agents. They are designed for developer and data-science
self-service rather than general storage administration.

All DataOps Toolkit MCP servers use local stdio transport and are distributed
as Python packages.

#### DataOps Toolkit MCP Server for ONTAP

- **Why you'd use it:** Give developers and data scientists fast,
  storage-efficient dataset lifecycle operations without exposing the full
  ONTAP administrative surface.
- **Coverage:** Create, list, mount, clone, and snapshot volumes; SnapMirror;
  FlexCache; SMB shares; qtrees; and qtree metrics.
- **Works with:** NetApp AFX, AFF, FAS, Amazon FSx for NetApp ONTAP, Cloud
  Volumes ONTAP, and ONTAP Select.
- **Start here:** [Documentation and setup](https://github.com/NetApp/netapp-dataops-toolkit/blob/main/netapp_dataops_traditional/docs/mcp_server.md)

#### DataOps Toolkit MCP Server for Azure NetApp Files

- **Why you'd use it:** Let Azure-based data teams create protected,
  high-performance datasets through simple agent workflows.
- **Coverage:** NFS and SMB volume provisioning, listing, cloning, snapshots,
  and cross-region replication, with reusable Azure infrastructure defaults.
- **Works with:** Azure NetApp Files.
- **Start here:** [Documentation and setup](https://github.com/NetApp/netapp-dataops-toolkit/blob/main/netapp_dataops_traditional/docs/anf_mcp_server_readme.md)

#### DataOps Toolkit MCP Server for Google Cloud NetApp Volumes

- **Why you'd use it:** Add a small, data-centric GCNV toolset to local agent
  workflows while keeping the same patterns used by the other DataOps Toolkit
  servers.
- **Coverage:** Volume provisioning and listing, clones, snapshots, and
  replication.
- **Works with:** Google Cloud NetApp Volumes.
- **Start here:** [Documentation and setup](https://github.com/NetApp/netapp-dataops-toolkit/blob/main/netapp_dataops_traditional/docs/gcnv_mcp_server_readme.md)

#### DataOps Toolkit MCP Server for Kubernetes

- **Why you'd use it:** Give data scientists self-service JupyterLab workspaces
  and persistent datasets while platform teams retain Kubernetes and storage
  policy control.
- **Coverage:** Create, list, clone, and snapshot JupyterLab workspaces and
  persistent volumes, plus FlexCache creation.
- **Works with:** Kubernetes with NetApp Trident, backed by AFF, FAS, Amazon FSx
  for NetApp ONTAP, Azure NetApp Files, Google Cloud NetApp Volumes, or Cloud
  Volumes ONTAP.
- **Start here:** [Documentation and setup](https://github.com/NetApp/netapp-dataops-toolkit/blob/main/netapp_dataops_k8s/docs/mcp_server_k8s.md)

## Similar names, different jobs

- **ONTAP MCP vs. DataOps Toolkit for ONTAP:** Choose ONTAP MCP for broad,
  multi-cluster storage administration. Choose DataOps Toolkit for ONTAP for a
  smaller, local, data-lifecycle toolset aimed at end-user self-service.
- **GCNV MCP vs. DataOps Toolkit for GCNV:** Choose GCNV MCP for broad
  control-plane management, protection, security, and NAS/SAN coverage. Choose
  the DataOps Toolkit server for focused volume, clone, snapshot, and
  replication workflows.
- **Harvest MCP telemetry context:** Harvest brings portfolio-wide telemetry
  context to infrastructure-management workflows across ONTAP, E-Series, and
  StorageGRID, with Cisco Nexus providing additional ecosystem visibility. It
  queries current and historical Harvest-collected data from Prometheus or
  VictoriaMetrics. It helps identify, diagnose, and explain problems but does
  not make configuration changes. For observe-to-act workflows, pair it with
  the relevant active management MCP server, such as ONTAP MCP, to execute an
  approved action.
- **AIDE MCP vs. Neo MCP:** AIDE provides semantic search over an existing AIDE
  index. Neo builds a permission-aware search and retrieval layer over
  enterprise file shares.

## Catalog scope

The active catalog includes publicly documented MCP servers published by
NetApp that can be connected to an MCP client. Internal-only projects and
client extensions that do not expose a separately usable MCP server are out of
scope. Early-access projects are labeled, and retired projects are kept
separate from the active catalog.

Every new or updated entry should state:

1. The outcome and customer value
2. When to choose it over adjacent NetApp MCP servers
3. The products, resources, and operations it covers
4. Its transport and deployment model
5. Where to find current documentation and source

## Archived projects

- [NetApp Workload Factory GenAI MCP Server](archive/NetApp-KnowledgeBase-MCP-server/)
  is retained for historical reference and is not part of the active catalog.

[harvest-docs]: https://netapp.github.io/harvest/latest/mcp/overview/
[harvest-source]: https://github.com/NetApp/harvest
[aide-source]: https://github.com/NetApp/aide-mcp-server
[aide-docs]: https://docs.netapp.com/us-en/ai-data-engine/index.html
[neo-mcp]: https://netapp.github.io/Innovation-Labs/projects/mlai/neo/core/m-mcp.html
[neo-overview]: https://netapp.github.io/Innovation-Labs/projects/mlai/neo/core/introduction.html
[neo-source]: https://github.com/NetApp/Innovation-Labs

## License

> Note: This licensing information applies to this repository. Other
> repositories linked from this README have their own licenses.

Licensed under the Apache License, Version 2.0 (the "License").

You may obtain a copy of the License at [apache.org/licenses/LICENSE-2.0](http://www.apache.org/licenses/LICENSE-2.0).

Unless required by applicable law or agreed to in writing, software distributed
under the License is distributed on an _"AS IS"_ basis, without WARRANTIES or
conditions of any kind, either express or implied.

See the License for the specific language governing permissions and limitations
under the License.

© 2026 NetApp, Inc. All Rights Reserved.
