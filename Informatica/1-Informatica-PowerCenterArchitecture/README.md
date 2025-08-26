## Informatica PowerCenter Architecture

![Informatica Architecture](image.png)

### Core components

- **Domain**: The top‑level container that holds and manages all services and nodes. You administer it via the web‑based Administrator Console.
- **Repository**: A database schema that stores all metadata (sources/targets, mappings, mapplets, workflows, sessions, connections, parameters, versions).
- **Repository Service (RS)**: Fronts the repository database. Handles check‑in/out, queries from client tools, object versioning, security, and locking.
- **Integration Service (IS)**: The runtime engine. It reads session/workflow instructions from the repository, connects to sources/targets, and moves/transforms data. Internally it spawns the DTM process with reader/transformer/writer threads, manages caching, partitions, commits, and recovery.
- **Client tools (PowerCenter Client)**:
  - **Repository Manager**: security, folders, object management, versions.
  - **Designer (Mapping Designer)**: build source/target definitions, mappings, mapplets, reusable transformations.
  - **Workflow Manager**: create sessions, tasks, and workflows; set schedules and runtime properties.
  - **Workflow Monitor**: run/monitor workflows, view logs, throughput, errors, and recovery states.
### Detailed workflow steps

- **Admin setup**
  - Create Domain, add Node(s), apply license.
  - Create Repository database schema; configure Repository Service.
  - Create Integration Service; assign to the Repository.
  - Define users/groups/roles and folders; set connections (relational, FTP/SFTP, file, queue, etc.).

- **Design the mapping (Designer)**
  - Import or define Source/Target definitions.
  - Build a Mapping with needed transformations (e.g., Source Qualifier, Expression, Filter/Router, Lookup, Joiner, Aggregator, Update Strategy, Sequence Generator).
  - Parameterize using mapping parameters/variables where appropriate; consider reusable mapplets.

- **Create the session (Workflow Manager)**
  - Create a Session for the mapping (or a reusable session).
  - Configure runtime properties: connections, pre/post‑SQL, commit interval, error handling, rejects, tracing level, pushdown optimization, partitioning, cache sizes, parameter file path.

- **Assemble the workflow**
  - Create a Workflow; add the Session and any tasks (Command, Decision, Event Wait/Raise, Email, Timer).
  - Link tasks with transitions; set properties like restart/recovery and scheduling (time, dependency, or on‑demand).
  - Validate the workflow.

- **Run and monitor**
  - Start the workflow or wait for the schedule.
  - The Integration Service launches the DTM: creates reader/transformer/writer threads, builds caches (lookups/aggregations), applies partitions, and processes rows.
  - Commits occur per configured interval; rejects go to bad files/tables if configured.
  - Observe progress and logs in Workflow Monitor; drill into session logs for errors and performance.

- **Recovery and promotion**
  - If a run fails, use workflow/session recovery (from last checkpoint/commit).
  - Tune (partitioning, pushdown, indexes, cache sizing).
  - Promote between environments via export/import or deployment groups; override with parameter files and environment‑specific connections.






