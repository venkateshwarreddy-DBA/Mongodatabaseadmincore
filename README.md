# Mongodatabaseadmincore

Mongo Scripts : 

Complete List of collections : 
db.products.find()

Limit List for 3 : 
db.products.find({},{}).limit(3)

Fetch with condition : 
db.student.find({ "address.country": "Bharat" })

Update Script :  (Update all)

db.student.updateMany(
  { "address.country": "India" },
  { $set: { "address.country": "Bharat" } }
)

Update with Condition : 

Update with condition where the state = TG
db.student.updateMany(
  { "address.state": "Telangana" },
  { $set: { "address.country": "Bharat" } }
)

Sorting : db.student.find().sort({"address.state":1})

Sorting with Limitation : db.student.find().sort({"address.state":1}).limit(3)

* Rebuilds all indexes on a collection in the background.
  ```javascript
  db.LAB.reIndex({background:true})
  ```
* Retrieves a list of all indexes present on a single collection.
  ```javascript
  db.LAB.getIndexes()
  ```
* Loops through every collection in the database to display their indexes.
  ```javascript
  db.getCollectionNames().forEach(function(collection) { indexes = db[collection].getIndexes(); print("Indexes for " + collection + ":"); printjson(indexes); });
  ```

### Server Monitoring & Metrics

* Checks the total server uptime in seconds (divide by 60 for minutes, 3600 for hours, 84600 for days).
  ```javascript
  db.serverStatus().uptime
  ```
* Displays active, available, and total created connection counts on the server.
  ```javascript
  db.serverStatus().connections
  ```
* Checks global lock details, read/write operation counts, and blocked client queues.
  ```javascript
  db.serverStatus().globalLock
  ```
* Counts total database operations (inserts, queries, updates, deletes) since the last reboot.
  ```javascript
  db.serverStatus().opcounters
  ```
* Monitors resident and virtual RAM usage metrics utilized by MongoDB.
  ```javascript
  db.serverStatus().mem
  ```
* Identifies the hostname of the server to which you are currently connected.
  ```javascript
  db.serverStatus().host
  ```
* Retrieves the current MongoDB server software version.
  ```javascript
  db.serverStatus().version
  ```

### Server Shutdown & Recovery

* Switches to the administrative database and safely shuts down the server instance.
  ```javascript
  use admin
  db.shutdownServer()
  ```
* Forces a server shutdown from any active database connection using an admin command.
  ```javascript
  db.adminCommand({shutdown:1})
  ```
* Repairs data files and clears the lock file after an unexpected server crash.
  ```bash
  mongod –dbpath /data/db --repair
  ```




# Complete MongoDB db.serverStatus() Reference Matrix

The output of `db.serverStatus()` provides an extensive deep-dive window into the memory, performance, locking structure, storage health, and transactional integrity of a MongoDB node. Below is a structured compilation of all primary dot-notation paths, metrics objects, and configurations you can inspect.

---

### `db.serverStatus().asserts`
**Description:** The number of assertions raised since the server started.

*   **`.msg`**: Number of message assertions.
*   **`.regular`**: Number of regular assertions.
*   **`.rollovers`**: Number of times the assert counters have rolled over.
*   **`.user`**: Number of user assertions.
*   **`.warning`**: Number of warning assertions.

---

### `db.serverStatus().batchedDeletes`
**Description:** Metrics related to batched delete operations.

*   **`.buffers`**: Metrics for the buffers used in batched deletes.

---

### `db.serverStatus().catalogStats`
**Description:** Statistics on the internal catalog.

*   **`.collections`**: Number of collections in the catalog.
*   **`.views`**: Number of views in the catalog.

---

### `db.serverStatus().connections`
**Description:** Client connection status and limits.

*   **`.active`**: Number of active client connections performing operations.
*   **`.available`**: Number of unused connections available.
*   **`.awaitingTopologyChanges`**: Connections waiting for topology changes.
*   **`.current`**: Number of incoming active connections from clients.
*   **`.exhaustHello`**: Number of exhaust hello connections.
*   **`.exhaustIsMaster`**: Number of exhaust isMaster connections.
*   **`.threaded`**: Number of connection threads.
*   **`.totalCreated`**: Total number of connections created since startup.

---

### `db.serverStatus().electionMetrics`
**Description:** Replication election metrics (if replica set).

*   **`.catchUpTakeover`**: Metrics for catch-up takeovers.
*   **`.electionTimeout`**: Metrics for election timeouts.
*   **`.freezeTimeout`**: Metrics for freeze timeouts.
*   **`.numIterations`**: Number of election iterations.
*   **`.priorityTakeover`**: Metrics for priority takeovers.
*   **`.stepUpCmd`**: Metrics for step-up commands.

---

### `db.serverStatus().extra_info`
**Description:** Platform-specific system metrics.

*   **`.heap_usage_bytes`**: Heap usage bytes (Linux/macOS).
*   **`.note`**: Fields vary by operating system.
*   **`.page_faults`**: Total page faults (Linux/Windows).

---

### `db.serverStatus().flowControl`
**Description:** Flow control mechanism status under high write loads.

*   **`.enabled`**: Whether flow control is enabled.
*   **`.isLagged`**: Whether the replica set member is lagged.
*   **`.isLaggedAndClientLocksHeld`**: Whether it's lagged while holding client locks.
*   **`.targetRateLimit`**: The target operation rate limit.
*   **`.timeWaitingMicros`**: Time spent waiting for flow control.

---

### `db.serverStatus().freeMonitoring`
**Description:** Status of MongoDB Cloud Free Monitoring.

*   **`.state`**: The registration state (enabled, disabled).

---

### `db.serverStatus().globalLock`
**Description:** Global database lock metrics.

*   **`.activeClients`**: Sub-nested component metrics.
*   **`.currentQueue`**: Sub-nested component metrics.
*   **`.totalTime`**: Total time the global lock has existed.

---

### `db.serverStatus().hedgingMetrics`
**Description:** Metrics for hedged reads in sharded clusters.

*   **`.numAdvantagedOperations`**: Number of operations that successfully benefited from hedging.
*   **`.numTotalOperations`**: Total number of operations hedged.

---

### `db.serverStatus().host`
**Description:** The hostname of the MongoDB instance.


---

### `db.serverStatus().indexBulkBuilder`
**Description:** Internal metrics for bulk index builds.

*   **`.count`**: Active bulk builder instances.

---

### `db.serverStatus().initialSyncProgress`
**Description:** Progress of an initial replication sync (only present during sync).

*   **`.phase`**: Current sync phase status.

---

### `db.serverStatus().internalTransactions`
**Description:** Metrics tracking internal retryable or replica transactions.

*   **`.totalStarted`**: Total internal transactions started.

---

### `db.serverStatus().javaScriptEngine`
**Description:** V8 or current JavaScript engine tracking parameters.

*   **`.totalActiveScopes`**: Active JS scopes across operations.

---

### `db.serverStatus().localTime`
**Description:** The current ISODate time of the server.


---

### `db.serverStatus().locks`
**Description:** Granular lock metrics organized by scope (Global, Database, Collection, Metadata, OpLog).

*   **`.acquireCount`**: Number of times a lock was acquired in a specific mode (R, W, r, w).
*   **`.acquireWaitCount`**: Number of times a lock acquisition had to wait.
*   **`.deadlockCount`**: Number of deadlocks encountered.
*   **`.timeWaitingMicros`**: Total time spent waiting for locks in microseconds.

---

### `db.serverStatus().logicalSessionRecordCache`
**Description:** Statistics for the active logical session cache tracking sessions.

*   **`.activeSessionsCount`**: Number of active sessions currently cached.
*   **`.sessionsCollectionJobCount`**: Number of session collection refresh executions.

---

### `db.serverStatus().mem`
**Description:** System memory utilization as reported by the process.

*   **`.bits`**: Target word size architecture (64).
*   **`.resident`**: Resident memory size in megabytes (RAM currently used).
*   **`.supported`**: Indicates if underlying system provides memory tracking parameters.
*   **`.virtual`**: Virtual memory size in megabytes.

---

### `db.serverStatus().metrics`
**Description:** A deeply nested document holding thousands of sub-metrics.

*   **`.commands`**: Counts and execution times for every database command.
*   **`.cursor`**: Information on open, timed-out, or pinned cursors.
*   **`.document`**: Counts of documents inserted, deleted, updated, or returned.
*   **`.getLastError`**: Statistics on write concern confirmations.
*   **`.operation`**: Counters for internal state operations like fastmod.
*   **`.query`**: Internal details about query execution planning.
*   **`.repl`**: Replication network metrics and executor pools.
*   **`.storage`**: Internal storage layer tracking variables.
*   **`.ttl`**: Statistics on the background execution delete tracking index task.

---

### `db.serverStatus().mirroredReads`
**Description:** Metrics for sampling reads from secondary replica set nodes.

*   **`.mirrored`**: Number of queries mirrored to secondaries.
*   **`.seen`**: Number of eligible queries seen.

---

### `db.serverStatus().network`
**Description:** Network traffic statistics.

*   **`.bytesIn`**: Total bytes received over the network.
*   **`.bytesOut`**: Total bytes sent over the network.
*   **`.numRequests`**: Total network requests processed.

---

### `db.serverStatus().opLatencies`
**Description:** Operation latency percentages for reads, writes, and commands.

*   **`.commands`**: Latency statistics for admin or schema tasks.
*   **`.reads`**: Latency histogram and operation counts.
*   **`.writes`**: Latency statistics for update operations.

---

### `db.serverStatus().opReadConcernCounters`
**Description:** Tracks read concern levels chosen by application clients.

*   **`.available`**: Usage count for available read concern.
*   **`.linearizable`**: Usage count for linearizable read concern.
*   **`.local`**: Usage count for local read concern.
*   **`.majority`**: Usage count for majority read concern.
*   **`.snapshot`**: Usage count for snapshot read concern.

---

### `db.serverStatus().opWriteConcernCounters`
**Description:** Tracks write concern modes submitted by workloads.

*   **`.w1`**: Writes asking for single node acknowledge.
*   **`.wmajority`**: Writes asking for majority confirmations.

---

### `db.serverStatus().opcounters`
**Description:** Database operation counters since last startup.

*   **`.command`**: Total database command executions.
*   **`.delete`**: Total delete operations.
*   **`.getmore`**: Total getmore cursor operations.
*   **`.insert`**: Total insert operations.
*   **`.query`**: Total query operations.
*   **`.update`**: Total update operations.

---

### `db.serverStatus().opcountersRepl`
**Description:** Replication specific operation counters applied to a secondary node.

*   **`.command`**: Replicated command instructions.
*   **`.delete`**: Replicated delete operations.
*   **`.getmore`**: Replicated getmore commands.
*   **`.insert`**: Replicated insert operations.
*   **`.query`**: Replicated queries (empty for secondaries).
*   **`.update`**: Replicated update operations.

---

### `db.serverStatus().operationTime`
**Description:** Timestamp tracking clock sequence for operations (causal consistency).


---

### `db.serverStatus().pid`
**Description:** The process ID.


---

### `db.serverStatus().process`
**Description:** The process name (mongod or mongos).


---

### `db.serverStatus().readConcernCounters`
**Description:** Internal cluster level tracker of read concern properties.


---

### `db.serverStatus().readPreferenceCounters`
**Description:** Tracks read choices passed via drivers (primary, secondaryPreferred, etc.).


---

### `db.serverStatus().repl`
**Description:** Replica set operational configuration block.

*   **`.hosts`**: Array of member host strings.
*   **`.ismaster`**: Boolean representing if this node is currently the primary.
*   **`.secondary`**: Boolean representing if this node is currently a secondary.
*   **`.setName`**: The replica set name.
*   **`.setVersion`**: Current configuration metadata version.

---

### `db.serverStatus().security`
**Description:** Security parameters currently running or enabled.

*   **`.authenticationMechanisms`**: Enabled auth strategies.

---

### `db.serverStatus().shardedIndexConsistency`
**Description:** Periodic index check configuration status across sharded nodes.


---

### `db.serverStatus().sharding`
**Description:** Sharding cluster metrics if this node belongs to a cluster config.

*   **`.configsvrConnectionString`**: Connection string to the config server cluster.

---

### `db.serverStatus().storageEngine`
**Description:** Information about the persistent engine layer.

*   **`.name`**: The engine key string (typically wiredTiger or ephemeralForTest).

---

### `db.serverStatus().tenantMigration`
**Description:** Tenant migration tracking states (MongoDB Atlas specific multi-tenant states).


---

### `db.serverStatus().trafficRecording`
**Description:** Status parameters for incoming system analysis recording frames.


---

### `db.serverStatus().transactions`
**Description:** Multi-document transactional status variables.

*   **`.currentActive`**: Active running transactions.
*   **`.currentInactive`**: Open but inactive transactions.
*   **`.totalAborted`**: Total aborted transaction workflows.
*   **`.totalCommitted`**: Total successfully committed transaction workflows.
*   **`.totalStarted`**: Total multi-document transactions initiated.

---

### `db.serverStatus().transportData`
**Description:** Low level metrics for socket and transport layer frames.


---

### `db.serverStatus().twoPhaseCommitCoordinator`
**Description:** Distributed transaction commit coordinator metrics.


---

### `db.serverStatus().uptime`
**Description:** The total number of seconds the server has been running.


---

### `db.serverStatus().uptimeEstimate`
**Description:** The uptime estimate based on system clocks.


---

### `db.serverStatus().uptimeMillis`
**Description:** The uptime in milliseconds.


---

### `db.serverStatus().version`
**Description:** The version of MongoDB.


---

### `db.serverStatus().watchdog`
**Description:** Storage engine path monitoring checks to ensure health configuration.


---

### `db.serverStatus().wiredTiger`
**Description:** WiredTiger storage engine internal telemetry block containing thousands of parameters.

*   **`.block-manager`**: Metrics regarding blocks written, read, and physical size states.
*   **`.cache`**: Detailed metrics for memory use, eviction rates, dirty bytes, and configuration status.
*   **`.concurrentTransactions`**: Ticket limits and availability for parallel read/write structures.
*   **`.session`**: Active execution context queues.

---













