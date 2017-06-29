# 配置文件说明

基于v2.1.5

配置项|说明
:------|:----
Debug|set debug mode (similar to --debug option)
EnableSyslog|Should logs be directed (in addition) to syslog daemon?
ListenAddress|Where orchestrator HTTP should listen for TCP
ListenSocket|Where orchestrator HTTP should listen for unix socket (default: empty; when given, TCP is disabled)
AgentsServerPort|port orchestrator agents talk back to
MySQLTopologyUser|
MySQLTopologyPassword|my.cnf style configuration file from where to pick credentials. Expecting `user`, `password` under `[client]` section
MySQLTopologyCredentialsConfigFile|
MySQLTopologySSLPrivateKeyFile|Private key file used to authenticate with a Topology mysql instance with TLS
MySQLTopologySSLCertFile|Certificate PEM file used to authenticate with a Topology mysql instance with TLS
MySQLTopologySSLCAFile|Certificate Authority PEM file used to authenticate with a Topology mysql instance with TLS
MySQLTopologySSLSkipVerify|If true, do not strictly validate mutual TLS certs for Topology mysql instances
MySQLTopologyUseMutualTLS|Turn on TLS authentication with the Topology MySQL instances
BackendDB|EXPERIMENTAL: type of backend db; either "mysql" or "sqlite3"
SQLite3DataFile|when BackendDB == "sqlite3", full path to sqlite3 datafile
SkipOrchestratorDatabaseUpdate|When true, do not check backend database schema nor attempt to update it. Useful when you may be running multiple versions of orchestrator, and you only wish certain boxes to dictate the db structure (or else any time a different orchestrator version runs it will rebuild database schema)
PanicIfDifferentDatabaseDeploy|When true, and this process finds the orchestrator backend DB was provisioned by a different version, panic
MySQLOrchestratorHost|
MySQLOrchestratorMaxPoolConnections|The maximum size of the connection pool to the Orchestrator backend.
MySQLOrchestratorPort|
MySQLOrchestratorDatabase|
MySQLOrchestratorUser|
MySQLOrchestratorPassword|
MySQLOrchestratorCredentialsConfigFile|my.cnf style configuration file from where to pick credentials. Expecting `user`, `password` under `[client]` section
MySQLOrchestratorSSLPrivateKeyFile|Private key file used to authenticate with the Orchestrator mysql instance with TLS
MySQLOrchestratorSSLCertFile|Certificate PEM file used to authenticate with the Orchestrator mysql instance with TLS
MySQLOrchestratorSSLCAFile|Certificate Authority PEM file used to authenticate with the Orchestrator mysql instance with TLS
MySQLOrchestratorSSLSkipVerify|If true, do not strictly validate mutual TLS certs for the Orchestrator mysql instances
MySQLOrchestratorUseMutualTLS|Turn on TLS authentication with the Orchestrator MySQL instance
MySQLConnectTimeoutSeconds|Number of seconds before connection is aborted (driver-side)
MySQLOrchestratorReadTimeoutSeconds|Number of seconds before backend mysql read operation is aborted (driver-side)
MySQLDiscoveryReadTimeoutSeconds|Number of seconds before topology mysql read operation is aborted (driver-side). Used for discovery queries.
MySQLTopologyReadTimeoutSeconds|Number of seconds before topology mysql read operation is aborted (driver-side). Used for all but discovery queries.
MySQLInterpolateParams|Do not use sql prepare statement if true
DefaultInstancePort|In case port was not specified on command line
SlaveLagQuery|Synonym to ReplicationLagQuery
ReplicationLagQuery|custom query to check on replica lg (e.g. heartbeat table)
DiscoverByShowSlaveHosts|Attempt SHOW SLAVE HOSTS before PROCESSLIST
InstancePollSeconds|Number of seconds between instance reads
InstanceWriteBufferSize|Instance write buffer size (max number of instances to flush in one INSERT ODKU)
BufferInstanceWrites|Set to 'true' for write-optimization on backend table (compromise: writes can be stale and overwrite non stale data)
InstanceFlushIntervalMilliseconds|Max interval between instance write buffer flushes
SkipMaxScaleCheck|If you don't ever have MaxScale BinlogServer in your topology (and most people don't), set this to 'true' to save some pointless queries
UnseenInstanceForgetHours|Number of hours after which an unseen instance is forgotten
SnapshotTopologiesIntervalHours|Interval in hour between snapshot-topologies invocation. Default: 0 (disabled)
DiscoveryMaxConcurrency|Number of goroutines doing hosts discovery
DiscoveryQueueCapacity|Buffer size of the discovery queue. Should be greater than the number of DB instances being discovered
DiscoveryQueueMaxStatisticsSize|The maximum number of individual secondly statistics taken of the discovery queue
DiscoveryCollectionRetentionSeconds|Number of seconds to retain the discovery collection information
InstanceBulkOperationsWaitTimeoutSeconds|Time to wait on a single instance when doing bulk (many instances) operation
HostnameResolveMethod|Method by which to "normalize" hostname ("none"/"default"/"cname")
MySQLHostnameResolveMethod|Method by which to "normalize" hostname via MySQL server. ("none"/"@@hostname"/"@@report_host"; default "@@hostname")
SkipBinlogServerUnresolveCheck|Skip the double-check that an unresolved hostname resolves back to same hostname for binlog servers
ExpiryHostnameResolvesMinutes|Number of minutes after which to expire hostname-resolves
RejectHostnameResolvePattern|Regexp pattern for resolved hostname that will not be accepted (not cached, not written to db). This is done to avoid storing wrong resolves due to network glitches.
ReasonableReplicationLagSeconds|Above this value is considered a problem
ProblemIgnoreHostnameFilters|Will minimize problem visualization for hostnames matching given regexp filters
VerifyReplicationFilters|Include replication filters check before approving topology refactoring
ReasonableMaintenanceReplicationLagSeconds|Above this value move-up and move-below are blocked
CandidateInstanceExpireMinutes|Minutes after which a suggestion to use an instance as a candidate replica (to be preferably promoted on master failover) is expired.
AuditLogFile|Name of log file for audit operations. Disabled when empty.
AuditToSyslog|If true, audit messages are written to syslog
RemoveTextFromHostnameDisplay|Text to strip off the hostname on cluster/clusters pages
ReadOnly|
AuthenticationMethod|Type of autherntication to use, if any. "" for none, "basic" for BasicAuth, "multi" for advanced BasicAuth, "proxy" for forwarded credentials via reverse proxy, "token" for token based access
OAuthClientId|
OAuthClientSecret|
OAuthScopes|
HTTPAuthUser|Username for HTTP Basic authentication (blank disables authentication)
HTTPAuthPassword|Password for HTTP Basic authentication
AuthUserHeader|HTTP header indicating auth user, when AuthenticationMethod is "proxy"
PowerAuthUsers|On AuthenticationMethod == "proxy", list of users that can make changes. All others are read-only.
PowerAuthGroups|list of unix groups the authenticated user must be a member of to make changes.
AccessTokenUseExpirySeconds|Time by which an issued token must be used
AccessTokenExpiryMinutes|Time after which HTTP access token expires
ClusterNameToAlias|map between regex matching cluster name to a human friendly alias
DetectClusterAliasQuery|Optional query (executed on topology instance) that returns the alias of a cluster. Query will only be executed on cluster master (though until the topology's master is resovled it may execute on other/all replicas). If provided, must return one row, one column
DetectClusterDomainQuery|Optional query (executed on topology instance) that returns the VIP/CNAME/Alias/whatever domain name for the master of this cluster. Query will only be executed on cluster master (though until the topology's master is resovled it may execute on other/all replicas). If provided, must return one row, one column
DetectInstanceAliasQuery|Optional query (executed on topology instance) that returns the alias of an instance. If provided, must return one row, one column
DetectPromotionRuleQuery|Optional query (executed on topology instance) that returns the promotion rule of an instance. If provided, must return one row, one column.
DataCenterPattern|Regexp pattern with one group, extracting the datacenter name from the hostname
PhysicalEnvironmentPattern|Regexp pattern with one group, extracting physical environment info from hostname (e.g. combination of datacenter & prod/dev env)
DetectDataCenterQuery|Optional query (executed on topology instance) that returns the data center of an instance. If provided, must return one row, one column. Overrides DataCenterPattern and useful for installments where DC cannot be inferred by hostname
DetectPhysicalEnvironmentQuery|Optional query (executed on topology instance) that returns the physical environment of an instance. If provided, must return one row, one column. Overrides PhysicalEnvironmentPattern and useful for installments where env cannot be inferred by hostname
DetectSemiSyncEnforcedQuery|Optional query (executed on topology instance) to determine whether semi-sync is fully enforced for master writes (async fallback is not allowed under any circumstance). If provided, must return one row, one column, value 0 or 1.
SupportFuzzyPoolHostnames|Should "submit-pool-instances" command be able to pass list of fuzzy instances (fuzzy means non-fqdn, but unique enough to recognize). Defaults 'true', implies more queries on backend db
InstancePoolExpiryMinutes|Time after which entries in database_instance_pool are expired (resubmit via `submit-pool-instances`)
PromotionIgnoreHostnameFilters|Orchestrator will not promote replicas with hostname matching pattern (via -c recovery; for example, avoid promoting dev-dedicated machines)
ServeAgentsHttp|Spawn another HTTP interface dedicated for orchestrator-agent
AgentsUseSSL|When "true" orchestrator will listen on agents port with SSL as well as connect to agents via SSL
AgentsUseMutualTLS|When "true" Use mutual TLS for the server to agent communication
AgentSSLSkipVerify|When using SSL for the Agent, should we ignore SSL certification error
AgentSSLPrivateKeyFile|Name of Agent SSL private key file, applies only when AgentsUseSSL = true
AgentSSLCertFile|Name of Agent SSL certification file, applies only when AgentsUseSSL = true
AgentSSLCAFile|Name of the Agent Certificate Authority file, applies only when AgentsUseSSL = true
AgentSSLValidOUs|Valid organizational units when using mutual TLS to communicate with the agents
UseSSL|Use SSL on the server web port
UseMutualTLS|When "true" Use mutual TLS for the server's web and API connections
SSLSkipVerify|When using SSL, should we ignore SSL certification error
SSLPrivateKeyFile|Name of SSL private key file, applies only when UseSSL = true
SSLCertFile|Name of SSL certification file, applies only when UseSSL = true
SSLCAFile|Name of the Certificate Authority file, applies only when UseSSL = true
SSLValidOUs|Valid organizational units when using mutual TLS
StatusEndpoint|Override the status endpoint.  Defaults to '/api/status'
StatusSimpleHealth|If true, calling the status endpoint will use the simplified health check
StatusOUVerify    |If true, try to verify OUs when Mutual TLS is on.  Defaults to false
AgentPollMinutes|Minutes between agent polling
UnseenAgentForgetHours|Number of hours after which an unseen agent is forgotten
StaleSeedFailMinutes  |Number of minutes after which a stale (no progress) seed is considered failed.
SeedAcceptableBytesDiff|Difference in bytes between seed source & target data size that is still considered as successful copy
PseudoGTIDPattern|Pattern to look for in binary logs that makes for a unique entry (pseudo GTID). When empty, Pseudo-GTID based refactoring is disabled.
PseudoGTIDPatternIsFixedSubstring|If true, then PseudoGTIDPattern is not treated as regular expression but as fixed substring, and can boost search time
PseudoGTIDMonotonicHint|subtring in Pseudo-GTID entry which indicates Pseudo-GTID entries are expected to be monotonically increasing
DetectPseudoGTIDQuery  |Optional query which is used to authoritatively decide whether pseudo gtid is enabled on instance
PseudoGTIDPreferIndependentMultiMatch | if 'false', a multi-replica Pseudo-GTID operation will attempt grouping replicas via Pseudo-GTID, and make less binlog computations. However it may cause servers in same bucket wait for one another, which could delay some servers from being repointed. There is a tradeoff between total operation time for all servers, and per-server time. When 'true', Pseudo-GTID matching will operate per server, independently. This will cause waste of same calculations, but no two servers will wait on one another.
BinlogEventsChunkSize|Chunk size (X) for SHOW BINLOG/RELAYLOG EVENTS LIMIT ?,X statements. Smaller means less locking and mroe work to be done
SkipBinlogEventsContaining | When scanning/comparing binlogs for Pseudo-GTID, skip entries containing given texts. These are NOT regular expressions (would consume too much CPU while scanning binlogs), just substrings to find.
ReduceReplicationAnalysisCount   |When true, replication analysis will only report instances where possibility of handled problems is possible in the first place (e.g. will not report most leaf nodes, that are mostly uninteresting). When false, provides an entry for every known instance
FailureDetectionPeriodBlockMinutes| The time for which an instance's failure discovery is kept "active", so as to avoid concurrent "discoveries" of the instance's failure; this preceeds any recovery process, if any.
RecoveryPollSeconds  |Interval between checks for a recovery scenario and initiation of a recovery process
RecoveryPeriodBlockMinutes        | (supported for backwards compatibility but please use newer `RecoveryPeriodBlockSeconds` instead) The time for which an instance's recovery is kept "active", so as to avoid concurrent recoveries on smae instance as well as flapping
RecoveryPeriodBlockSeconds        | (overrides `RecoveryPeriodBlockMinutes`) The time for which an instance's recovery is kept "active", so as to avoid concurrent recoveries on smae instance as well as flapping
RecoveryIgnoreHostnameFilters  | Recovery analysis will completely ignore hosts matching given patterns
RecoverMasterClusterFilters| Only do master recovery on clusters matching these regexp patterns (of course the ".*" pattern matches everything)
RecoverIntermediateMasterClusterFilters |Only do IM recovery on clusters matching these regexp patterns (of course the ".*" pattern matches everything)
ProcessesShellCommand  |Shell that executes command scripts
OnFailureDetectionProcesses| Processes to execute when detecting a failover scenario (before making a decision whether to failover or not). May and should use some of these placeholders: {failureType}, {failureDescription}, {failedHost}, {failureCluster}, {failureClusterAlias}, {failureClusterDomain}, {failedPort}, {successorHost}, {successorPort}, {successorAlias}, {countReplicas}, {replicaHosts}, {isDowntimed}, {autoMasterRecovery}, {autoIntermediateMasterRecovery}
PreFailoverProcesses       | Processes to execute before doing a failover (aborting operation should any once of them exits with non-zero code; order of execution undefined). May and should use some of these placeholders: {failureType}, {failureDescription}, {failedHost}, {failureCluster}, {failureClusterAlias}, {failureClusterDomain}, {failedPort}, {successorHost}, {successorPort}, {successorAlias}, {countReplicas}, {replicaHosts}, {isDowntimed}
PostFailoverProcesses      | Processes to execute after doing a failover (order of execution undefined). May and should use some of these placeholders: {failureType}, {failureDescription}, {failedHost}, {failureCluster}, {failureClusterAlias}, {failureClusterDomain}, {failedPort}, {successorHost}, {successorPort}, {successorAlias}, {countReplicas}, {replicaHosts}, {isDowntimed}, {isSuccessful}, {lostReplicas}
PostUnsuccessfulFailoverProcesses       |Processes to execute after a not-completely-successful failover (order of execution undefined). May and should use some of these placeholders: {failureType}, {failureDescription}, {failedHost}, {failureCluster}, {failureClusterAlias}, {failureClusterDomain}, {failedPort}, {successorHost}, {successorPort}, {successorAlias}, {countReplicas}, {replicaHosts}, {isDowntimed}, {isSuccessful}, {lostReplicas}
PostMasterFailoverProcesses| Processes to execute after doing a master failover (order of execution undefined). Uses same placeholders as PostFailoverProcesses
PostIntermediateMasterFailoverProcesses |Processes to execute after doing a master failover (order of execution undefined). Uses same placeholders as PostFailoverProcesses
UnreachableMasterWithStaleSlavesProcesses  |Processes to execute when detecting an UnreachableMasterWithStaleSlaves scenario.
CoMasterRecoveryMustPromoteOtherCoMaster | When 'false', anything can get promoted (and candidates are prefered over others). When 'true', orchestrator will promote the other co-master or else fail
DetachLostSlavesAfterMasterFailover   | synonym to DetachLostReplicasAfterMasterFailover
DetachLostReplicasAfterMasterFailover | Should replicas that are not to be lost in master recovery (i.e. were more up-to-date than promoted replica) be forcibly detached
ApplyMySQLPromotionAfterMasterFailover| Should orchestrator take upon itself to apply MySQL master promotion: set read_only=0, detach replication, etc.
MasterFailoverLostInstancesDowntimeMinutes|Number of minutes to downtime any server that was lost after a master failover (including failed master & lost replicas). 0 to disable
MasterFailoverDetachSlaveMasterHost   | synonym to MasterFailoverDetachReplicaMasterHost
MasterFailoverDetachReplicaMasterHost | Should orchestrator issue a detach-replica-master-host on newly promoted master (this makes sure the new master will not attempt to replicate old master if that comes back to life). Defaults 'false'. Meaningless if ApplyMySQLPromotionAfterMasterFailover is 'true'.
FailMasterPromotionIfSQLThreadNotUpToDate| when true, and a master failover takes place, if candidate master has not consumed all relay logs, promotion is aborted with error
PostponeSlaveRecoveryOnLagMinutes      |Synonym to PostponeReplicaRecoveryOnLagMinutes
PostponeReplicaRecoveryOnLagMinutes    |On crash recovery, replicas that are lagging more than given minutes are only resurrected late in the recovery process, after master/IM has been elected and processes executed. Value of 0 disables this feature
RemoteSSHForMasterFailover       |Should orchestrator attempt a remote-ssh relaylog-synching upon master failover? Requires RemoteSSHCommand
RemoteSSHCommand |A `ssh` command to be used by recovery process to read/apply relaylogs. If provided, this variable must contain the text "{hostname}". The remote SSH login must have the privileges to read/write relay logs. Example: "setuidgid remoteuser ssh {hostname}"
RemoteSSHCommandUseSudo          |Should orchestrator apply 'sudo' on the remote host upon SSH command
OSCIgnoreHostnameFilters   | OSC replicas recommendation will ignore replica hostnames matching given patterns
GraphiteAddr     |Optional; address of graphite port. If supplied, metrics will be written here
GraphitePath     |Prefix for graphite path. May include {hostname} magic placeholder
GraphiteConvertHostnameDotsToUnderscores | If true, then hostname's dots are converted to underscores before being used in graphite path
GraphitePollSeconds  |Graphite writes interval. 0 disables.
URLPrefix        |URL prefix to run orchestrator on non-root web path, e.g. /orchestrator to put it behind nginx.
MaxOutdatedKeysToShow|Maximum number of keys to show in ContinousDiscovery. If the number of polled hosts grows too far then showing the complete list is not ideal.
DiscoveryIgnoreReplicaHostnameFilters   |Regexp filters to apply to prevent auto-discovering new replicas. Usage: unreachable servers due to firewalls, applications which trigger binlog dumps
