# workers-scale
As a day2 operation, we can use this utility to scale our openshift cluster's worker nodes to a desired count and capture their bootup times.

### Build & Install
```
make build && make install
```
> **NOTE**: Might require sudo access
### Options
```
$ workers-scale

Utility to scale our openshift cluster's worker nodes to a desired count and capture their bootup times as day 2 operation

Usage:
  workers-scale [flags]
  workers-scale [command]

Available Commands:
  completion  Generate the autocompletion script for the specified shell
  help        Help about any command
  version     Print the version number of kube-burner

Flags:
      --metrics-profile strings       Comma separated list of metrics profiles to use (default [metrics-nodebootup.yml,metrics-nodebootup-report.yml])
      --metrics-endpoint string       YAML file with a list of metric endpoints, overrides the es-server and es-index flags
      --start int                     Epoch start time
      --end int                       Epoch end time
      --es-server string              Elastic Search endpoint
      --es-index string               Elastic Search index
      --uuid string                   Benchmark UUID (default "c8d20efb-d12d-425c-b8ea-de98aefb101e")
      --gc                            Garbage collect created resources (default true)
      --metrics-directory string      Directory to dump the metrics files in, when using default local indexing (default "collected-metrics")
      --mc-kubeconfig string          Path for management cluster kubeconfig
      --step duration                 Prometheus step size (default 30s)
      --additional-worker-nodes int   Additional workers to scale (default 3)
      --enable-autoscaler             Enables autoscaler while scaling the cluster
      --scale-event-epoch int         Scale event epoch time
      --user-metadata string          User provided metadata file, in YAML format
      --tarball-name string           Dump collected metrics into a tarball with the given name, requires local indexing
      --log-level string              Allowed values: debug, info, warn, error, fatal (default "info")
  -h, --help                          help for workers-scale
```
### Examples
1. Manually scale a cluster to desired node count and capture bootup times.
```
$ workers-scale --additional-worker-nodes 24
```
2. Auto scale a cluster to a desired node count and capture bootup times. Also disable garbage collection.
```
$ workers-scale --additional-worker-nodes 24 --enable-autoscaler --gc=false
```
3. Without any scaling, simply capture bootup times on an already scaled cluster. We just have to specify the timestamp when the scale event was triggered.
```
$ workers-scale --scale-event-epoch 1725635502
```