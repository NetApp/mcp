# NetApp MCP servers

## Give AI agents useful, governed access to your data estate

NetApp Model Context Protocol (MCP) servers connect AI assistants and agents to
technical documentation, storage operations, infrastructure telemetry, and
enterprise data. Use this catalog to choose the server that matches the outcome
you need—not simply the product you own.

## Choose by outcome

| What you want an AI agent to do | Start with | Why |
| --- | --- | --- |
| Administer ONTAP across one or more clusters | [ONTAP MCP Server](#ontap-mcp-server) | Broad ONTAP administration across NAS, SAN, NVMe, data protection, and core storage services |
| Identify infrastructure problems, investigate performance, and plan capacity | [Harvest MCP Server](#harvest-mcp-server) | Uses current and historical Harvest telemetry from Prometheus or VictoriaMetrics across ONTAP, E-Series, and StorageGRID; Cisco Nexus adds ecosystem visibility |
| Manage Google Cloud NetApp Volumes end to end | [Google Cloud NetApp Volumes MCP Server](#google-cloud-netapp-volumes-mcp-server) | Broad GCNV control-plane coverage, including pools, protection, security, NAS, and iSCSI |
| Provision, clone, and protect datasets or workspaces | [NetApp DataOps Toolkit MCP server family](#netapp-dataops-toolkit-mcp-server-family) | Four task-focused MCP servers for ONTAP, Azure NetApp Files, Google Cloud NetApp Volumes, and Kubernetes, with self-service workflows for developers, data scientists, and platform teams |
| Ground answers and workflows in official NetApp technical documentation | [docs.netapp.com MCP server](#docsnetappcom-mcp-server) | Focused remote service for searching and retrieving published documentation and generating RAG-based answers without a custom integration |
| Review risks, security recommendations, upgrade readiness, and AutoSupport for your NetApp systems | [Active IQ MCP Server](#active-iq-mcp-server) | Uses the AutoSupport data your systems already send to NetApp, so there is nothing to deploy or integrate; covers risks, security recommendations and remediation, support cases, contracts, and upgrade guidance |
| Investigate infrastructure health, performance, capacity, alerts, logs, and collection status in Data Infrastructure Insights | [DII MCP Server](#dii-mcp-server) | Brings tenant-scoped DII inventory, telemetry, events, alerts, collector health, and notification posture into natural-language, read-only investigations |

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

### docs.netapp.com MCP server

**Bring trusted NetApp technical knowledge into the agent workflow.** Give
development, engineering, and support agents a standard interface to find
official NetApp product documentation, retrieve article content, and generate
documentation-grounded answers without building a custom REST, search, or RAG
pipeline.

- **Use it when:** Developers, engineers, support teams, or custom AI agents
  need official NetApp product and procedure context inside an MCP-compliant
  client.
- **Coverage:** Keyword and natural-language documentation search, structured
  retrieval of complete page and article content, RAG-based answer generation,
  and service health. Its source is content published to docs.netapp.com; it
  does not access private tenant data or internal user profiles, and it does not
  provide product telemetry, cluster state, or other environment-specific data.
- **Runs as:** A NetApp-hosted remote HTTP endpoint, deployed statelessly on
  scalable cloud infrastructure.
- **Works with:** Visual Studio Code with GitHub Copilot, Claude Desktop,
  Cursor, custom Python agent frameworks, and other supported MCP-compliant
  clients. Network access and a valid subscription key are required; request a
  key from `ng-docs-mcp@netapp.com` with a brief description of the use case.
- **Start here:** [Get started][docs-mcp-get-started] ·
  [Learn about the server][docs-mcp-learn] ·
  [Developer reference][docs-mcp-reference]

### Active IQ MCP Server

**Give agents Active IQ insights in the tools they already use.** Ask which
systems have critical risks and what to do about them, which security
recommendations apply, which clusters are due for an upgrade, which systems are
approaching end of support, the status of a support case, or what a recent
AutoSupport shows. Answers come from NetApp's analysis of the AutoSupport data
your systems already send, so an agent can go from a question to a recommended
action without a custom integration.

- **Use it when:** Storage and operations teams want risk, security, upgrade,
  and AutoSupport answers inside the AI client they already use—or you are
  building agents and automations that need that context for your NetApp
  systems.
- **Coverage:** Search and discovery across systems, clusters, sites, and
  watchlists; contract and AutoSupport status; risks, security recommendations,
  and corrective actions; support cases; Upgrade Advisor recommendations;
  AutoSupport records and raw section content; and custom on-the-fly GraphQL
  queries. The server is read-only: it cannot modify systems, and results are
  limited to what the authenticated user is authorized to see.
- **Runs as:** A NetApp-hosted remote HTTP endpoint.
- **Works with:** MCP clients that support remote HTTP servers and custom
  request headers, such as Cursor, Claude Desktop, and Visual Studio Code with
  GitHub Copilot. Requires access to Digital Advisor—the NetApp service that
  analyzes AutoSupport data from your installed systems—plus API registration
  and a personal access token (PAT).
- **Start here:** [Learn about the server][active-iq-mcp-learn] ·
  [Get started][active-iq-mcp-get-started]

### DII MCP Server

**Investigate your DII tenant from inventory to operational context.** Give AI
assistants a tenant-scoped, read-only view of normalized infrastructure
resources, performance and capacity telemetry, logs and events, alerts and
monitors, and collection health. For DII users, it goes beyond time-series
telemetry by adding collector, notification, and maintenance-window context
from the same tenant.

- **Use it when:** You use Data Infrastructure Insights and want to validate
  collection coverage and freshness, prioritize active infrastructure issues,
  identify capacity risk, troubleshoot performance, check Kubernetes collector
  currency, or review notification routing and suppression.
- **Coverage:** 26 read-only tools across acquisition units, alerts, data
  collectors, logs and events, maintenance windows, monitors, notification
  rules and webhook target metadata, infrastructure objects and metrics, and
  Kubernetes collectors. Available inventory includes storage, virtualization,
  Kubernetes, ONTAP, Azure NetApp Files, StorageGRID, and related resources.
- **Runs as:** A remote HTTP endpoint supplied for your DII environment at
  `https://<DII_HOST_URL>/api/v1/mcp`.
- **Works with:** Cursor, Claude Code, VS Code, Codex, and other MCP-compatible
  clients that support remote HTTP and your organization's authentication
  method. Requires a DII tenant, an authorized user or service identity, the
  supplied endpoint, and a token generated under Admin > API Access > MCP
  Configuration.
- **Start here:** [Overview][dii-mcp-overview] · [Setup][dii-mcp-setup] ·
  [Tool reference][dii-mcp-tools]

## Similar names, different jobs

- **docs.netapp.com MCP vs. operational MCP servers:** Choose docs.netapp.com
  MCP for published NetApp product documentation and RAG-based answers. It does
  not read or change a deployed environment. Choose ONTAP MCP or GCNV MCP for
  broad resource management, Harvest MCP for current and historical
  infrastructure telemetry, or a DataOps Toolkit MCP server for task-focused
  dataset and workspace operations.
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
[active-iq-mcp-learn]: https://docs.netapp.com/us-en/digital-advisor-automation/learn-digital-advisor-mcp.html
[active-iq-mcp-get-started]: https://docs.netapp.com/us-en/digital-advisor-automation/get-started-digital-advisor-mcp.html
[docs-mcp-get-started]: https://docs.netapp.com/us-en/about/mcp-server-get-started.html
[docs-mcp-learn]: https://docs.netapp.com/us-en/about/mcp-server-learn.html
[docs-mcp-reference]: https://docs.netapp.com/us-en/about/mcp-developer-reference.html
[dii-mcp-overview]: https://review.docs.netapp.com/us-en/data-infrastructure-insights_mcp_docs/mcp_overview.html
[dii-mcp-setup]: https://review.docs.netapp.com/us-en/data-infrastructure-insights_mcp_docs/mcp_setup.html
[dii-mcp-tools]: https://review.docs.netapp.com/us-en/data-infrastructure-insights_mcp_docs/mcp_tools_overview.html

## Licensing

Except where otherwise noted, content maintained directly in this catalog
repository is licensed under the Apache License 2.0; see [LICENSE](LICENSE).
Linked projects and products are separate works governed by their own licenses
and terms.

Copyright © 2026 NetApp, Inc.
