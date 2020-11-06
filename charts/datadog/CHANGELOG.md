# Datadog changelog

## 2.4.39

* Fixed a bug where `networkMonitoring.enabled` would not configure the process-agent correctly, causing network data to not be reported.

## 2.4.38

* Move the kube-state-metrics subchart from google's helm registry to charts.helm.sh/stable.

## 2.4.37

* Fix incorrect link for Event Collection in `values.yaml`.

## 2.4.36

* Fix `should-enable-system-probe` helper function to support `helm2`.

## 2.4.35

* Add options to set pod and container securityContext

## 2.4.34

* Add `datadog.networkMonitoring` section to allow the system-probe to be run without network performance monitoring. Deprecates `systemProbe.enabled`.

## 2.4.33

* Introduce overall cluster-name limit of 80
* Remove character limit of single parts of the cluster-name

## 2.4.32

* The `agents.volumeMounts` option is now properly propagated to all agent containers.

## 2.4.31

* Support adding labels to the Agent pods and daemonset via `agents.additionalLabels`.
* Support adding labels to the Cluster Agent pods and deployment via `clusterAgent.additionalLabels`.
* Support adding labels to the Cluster Checks Runner pods and deployment via `clusterChecksRunner.additionalLabels`.

## 2.4.30

* Refactor liveness and readiness probes with helpers to allow user overrides with other types of probes or disabling
  probes entirely.
* Introduce `clusterChecksRunner.healthPort` default setting.
* Use health port defaults instead of hardcoded values.

## 2.4.29

* Add `common-env-vars` to `system-probe` container

## 2.4.28

* Make sure we rollout Agent/CLC/DCA when an upgrade is done (thus triggering a change in token secret)

## 2.4.27

* Remove port defaults from liveness/readiness probes and show error notices on misconfiguration if user overrides are supplying custom node settings.

## 2.4.26

* Revert to Helm2 hash in `requirements.yaml` to retain compatibility with Helm 2

## 2.4.25

* Update default `datadog/agent` image tag to `7.23.0`
* Update default `datadog/cluster-agent` image tag to `1.9.0`

## 2.4.24

* Fix the Cluster Agent's network policy (allow ingress from node Agents)
* Add kube-state-metrics network policy

## 2.4.23

* Add `datadog.envFrom` parameter to support passing references to secrets and/or configmaps for environment
variables, instead of passing one by one.

## 2.4.22

* Add automatic README.md generation from `Values.yaml`

## 2.4.21

* Change `securityContext` variable name to `seLinuxContext` allow setting the PSP/SCC seLinux `type` or `rule`. Backward compatible.

## 2.4.20

* Add NetworkPolicy ingress rules for dogstatsd and APM

## 2.4.19

* Add NetworkPolicy
  Add the following parameters to control the creation of NetworkPolicy:
  * `agents.networkPolicy.create`
  * `clusterAgent.networkPolicy.create`
  * `clusterChecksRunner.networkPolicy.create`
  The NetworkPolicy managed by the Helm chart are designed to work out-of-the-box on most setups.
  In particular, the agents need to connect to the datadog intakes. NetworkPolicy can be restricted
  by IP but the datadog intake IP cannot be guaranteed to be stable.
  The agents are also susceptible to connect to any pod, on any port, depending on the "auto-discovery" annotations
  that can be dynamically added to them.

## 2.4.18

* Fix `config` volume not being mounted in clusterChecksRunner pods.

## 2.4.17

* Update default `Agent` and `Cluster-Agent` image tags: `7.22` and `1.18`.

## 2.4.16

* Add `External Metric` Aggregator config on Chart.

## 2.4.15

* Add `agents.podSecurity.apparmor.enabled` flag (defaulted to `true`).

## 2.4.14

* Fix external metrics on GKE due to Google fix on recent versions (introduced in 2.4.1).

## 2.4.13

* fix Agent `PodSecurityPolicy` with `hostPorts` definition, and missing RBAC.

## 2.4.12

* Add `compliance` and `runtime` `security-agent` support.

## 2.4.11

* Add `NET_BROADCAST` capability for `system-probe`.

## 2.4.10

* Add `scrubbing` option for helm charts to "Orchestrator Explorer" support.

## 2.4.9

* Add `DD_DOGSTATSD_TAG_CARDINALITY` capability.

## 2.4.8

* Fix, Only try to mount `/lib/modules` and `/usr/src` when needed.

## 2.4.7

* Add `eventfd` and `eventfd2` to allowed syscalls for `system-probe`.

## 2.4.6

* Fix Windows deployment support (fixes #15).

## 2.4.5

* Add mount propagation option for `hostVolumes`.

## 2.4.4

* Fix typo in `allowHostPorts`.
* Add support of `MustRunAs` in Agent `PodSecurityPolicy` and `SecurityContextConstraints`.

## 2.4.3

* Fix `Cluster-Agent` RBAC to collect new resources for the "Orchestrator Explorer" support.

## 2.4.2

* Add `install_info` file.

## 2.4.1

* Fix MetricsProvider RBAC setup on GKE clusters

## 2.4.0

* First release on github.com/datadog/helm-charts

## 2.3.41

* Fix issue with Kubernetes <= 1.14 and Cluster Agent's External Metrics Provider (must be 443)

## 2.3.40

* Update documentation for resource requests & limits default values.

## 2.3.39

* Propagate `datadog.checksd` to the clusterchecks runner to support custom checks there.

## 2.3.38

* Add support of DD\_CONTAINER\_{INCLUDE,EXCLUDE}\_{METRICS,LOGS}

## 2.3.37

* Add NET\_BROADCAST capability

## 2.3.36

* Bump default Agent version to `7.21.1`

## 2.3.35

* Add support for configuring the Datadog Admission Controller

## 2.3.34

* Add support for scaling based on `DatadogMetric` CRD

## 2.3.33

* Create new `datadog.podSecurity.securityContext` field to fix windows agent daemonset config.

## 2.3.32

* Always add os in nodeSelector based on `targetSystem`

## 2.3.31

* Fixed daemonset template for go 1.14

## 2.3.29

* Change the default port for the Cluster Agent's External Metrics Provider
  from 443 to 8443.
* Document usage of `clusterAgent.env`

## 2.3.28

* fix daemonset template generation if `datadog.securityContext` is set to `nil`

## 2.3.27

* add systemProbe.collectDNSStats option

## 2.3.26

* fix PodSecurityContext configuration

## 2.3.25

* Use directly .env var YAML block for all agents (was already the case for Cluster Agent)

## 2.3.24

* Allow enabling Orchestrator Explorer data collection from the process-agent

## 2.3.23

* Add the possibility to create a `PodSecurityPolicy` or a `SecurityContextConstraints` (Openshift) for the Agent's Daemonset Pods.

## 2.3.22

* Remove duplicate imagePullSecrets
* Fix DataDog location to useConfigMap in docs
* Adding explanation for metricsProvider.enabled

## 2.3.21

* Fix additional default values in `values.yaml` to prevent errors with Helm 2.x

## 2.3.20

* Fix process-agent <> system-probe communication

## 2.3.19

* Fix the container-trace-agent.yaml template creates invalid yaml when  `useSocketVolume` is enabled.

## 2.3.18

* Support arguments in the cluster-agent container `command` value

## 2.3.17

* grammar edits to datadog helm docs!
* Typo in log config

## 2.3.16

* Add parameter `clusterChecksRunner.rbac.serviceAccountAnnotations` for specifying annotations for dedicated ServiceAccount for Cluster Checks runners.
* Add parameters `clusterChecksRunner.volumes` and `clusterChecksRunner.volumeMounts` that can be used for providing a secret backend to Cluster Checks runners.

## 2.3.15

* Mount kernel headers in system-probe container
* Fix the mount of the `system-probe` socket in core agent
* Add parameters to enable eBPF based checks

## 2.3.14

* Allow overriding the `command` to run in the cluster-agent container

## 2.3.13

* Use two distinct health endpoints for liveness and readiness probes.

## 2.3.12

* Fix endpoints checks scheduling between agent and cluster check runners
* Cluster Check Runner now runs without s6 (similar to other agents)

## 2.3.11

* Bump the default version of the agent docker images

## 2.3.10

* Add dnsConfig options to all containers

## 2.3.9

* Add `clusterAgent.podLabels` variable to add labels to the Cluster Agent Pod(s)

## 2.3.8

* Fix templating errors when `clusterAgent.datadog_cluster_yaml` is being used.

## 2.3.7

* Fix an agent warning at startup because of a deprecated parameter

## 2.3.6

* Add `affinity` parameter in `values.yaml` for cluster agent deployment

## 2.3.5

* Add `DD_AC_INCLUDE` and `DD_AC_EXCLUDE` to all containers
* Add "Unix Domain Socket" support in trace-agent
* Add new parameter to specify the dogstatsd socket path on the host
* Fix typos in values.yaml
* Update "tags:" example in values.yaml
* Add "rate_limit_queries_*" in the datadog.cluster-agent prometheus check configuration

## 2.3.4

* Fix default values in `values.yaml` to prevent warnings with Helm 2.x

## 2.3.3

* Allow pre-release versions as docker image tag

## 2.3.2

* Update the DCA RBAC to allow it to create events in the HPA

## 2.3.1

* Update the example for `datadog.securityContext`

## 2.3.0

* Mount the directory containing the CRI socket instead of the socket itself
  This is to handle the cases where the docker daemon is restarted.
  In this case, the docker daemon will recreate its docker socket and,
  if the container bind-mounted directly the socket, the container would
  still have access to the old socket instead of the one of the new docker
  daemon.
  ⚠ This version of the chart requires an agent image 7.19.0 or more recent

## 2.2.12

* Adding resources for `system-probe` init container

## 2.2.11

* Add documentations around secret management in the datadog helm chart. It is to upstream
  requested changes in the IBM charts repository: https://github.com/IBM/charts/pull/690#discussion_r411702458
* update `kube-state-metrics` dependency
* uncomment every values.yaml parameters for IBM chart compliancy

## 2.2.10

* Remove `kubeStateMetrics` section from `values.yaml` as not used anymore

## 2.2.9

* Fixing variables description in README and Migration documentation (#22031)
* Avoid volumes mount conflict between `system-probe` and `logs` volumes in the `agent`.

## 2.2.8

* Mount `system-probe` socket in `agent` container when system-probe is enabled

## 2.2.7

* Add "Cluster-Agent" `Event` `create` RBAC permission

## 2.2.6

* Ensure the `trace-agent` computes the same hostname as the core `agent`.
  by giving it access to all the elements that might be used to compute the hostname:
  the `DD_CLUSTER_NAME` environment variable and the docker socket.

## 2.2.5

* Fix RBAC

## 2.2.4

* Move several EnvVars to `common-env-vars` to be accessible by the `trace-agent` #21991.
* Fix discrepancies migration-guide and readme reporded in #21806 and #21920.
* Fix EnvVars with integer value due to yaml. serialization, reported by #21853.
* Fix .Values.datadog.tags encoding, reported by #21663.
* Add Checksum to `xxx-cluster-agent-config` config map, reported by #21622 and contribution #21656.

## 2.2.3

* Fix `datadog.dockerOrCriSocketPath` helper #21992

## 2.2.2

* Fix indentation for `clusterAgent.volumes`.

## 2.2.1

* Updating `agents.useConfigMap` and `agents.customAgentConfig` parameter descriptions in the chart and main readme.

## 2.2.0

* Add Windows support
* Update documentation to reflect some changes that were made default
* Enable endpoint checks by default in DCA/Agent

## 2.1.2

* Fixed a bug where `DD_LEADER_ELECTION` was not set in the config init container, leading to a failure to adapt
config to this environment variable.

## 2.1.1

* Add option to enable WPA in the Cluster Agent.

## 2.1.0

* Changed the default for `processAgent.enabled` to `true`.

## 2.0.14

* Fixed a bug where the `trace-agent` runs in the same container as `dd-agent`

## 2.0.13

* Fix `system-probe` startup on latest versions of containerd.
  Here is the error that this change fixes:
  ```    State:          Waiting
      Reason:       CrashLoopBackOff
    Last State:     Terminated
      Reason:       StartError
      Message:      failed to create containerd task: OCI runtime create failed: container_linux.go:349: starting container process caused "close exec fds: ensure /proc/self/fd is on procfs: operation not permitted": unknown
      Exit Code:    128
   ```

## 2.0.11

* Add missing syscalls in the `system-probe` seccomp profile

## 2.0.10

* Do not enable the `cri` check when running on a `docker` setup.

## 2.0.7

* Pass expected `DD_DOGSTATSD_PORT` to datadog-agent rather than invalid `DD_DOGSTATD_PORT`

## 2.0.6

* Introduces `procesAgent.processCollection` to correctly configure `DD_PROCESS_AGENT_ENABLED` for the process agent.

## 2.0.5

* Honor the `datadog.env` parameter in all containers.

## 2.0.4

* Honor the image pull policy in init containers.
* Pass the `DD_CRI_SOCKET_PATH` environment variable to the config init container so that it can adapt the agent config based on the CRI.

## 2.0.3

* Fix templating error when `agents.useConfigMap` is set to true.
* Add DD\_APM\_ENABLED environment variable to trace agent container.

## 2.0.2

* Revert the docker socket path inside the agent container to its standard location to fix #21223.

## 2.0.1

* Add parameters `datadog.logs.enabled` and `datadog.logs.containerCollectAll` to replace `datadog.logsEnabled` and `datadog.logsConfigContainerCollectAll`.
* Update the migration document link in the `Readme.md`.

### 2.0.0

* Remove Datadog agent deployment configuration.
* Cleanup resources labels, to fit with recommended labels.
* Cleanup useless or unused values parameters.
* each component have its own RBAC configuration (create,configuration).
* container runtime socket update values configuration simplification.
* `nameOverride` `fullnameOverride` is now optional in values.yaml.