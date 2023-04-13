[View code on GitHub](https://github.com/cosmos/cosmos-sdk.git/telemetry/metrics.go)

The `telemetry` package provides a wrapper around application telemetry functionality. It allows metrics to be gathered at any point in time. The package provides a `Metrics` struct that is used to gather metrics. When creating a `Metrics` object, a global metrics is registered with a set of sinks as configured by the operator. In addition to the sinks, when a process gets a `SIGUSR1`, a dump of formatted recent metrics will be sent to `STDERR`.

The `Config` struct defines the configuration options for application telemetry. It has the following fields:
- `ServiceName`: Prefixed with keys to separate services.
- `Enabled`: Enables the application telemetry functionality. When enabled, an in-memory sink is also enabled by default. Operators may also enable other sinks such as Prometheus.
- `EnableHostname`: Enables prefixing gauge values with hostname.
- `EnableHostnameLabel`: Enables adding hostname to labels.
- `EnableServiceLabel`: Enables adding service to labels.
- `PrometheusRetentionTime`: When positive, enables a Prometheus metrics sink. It defines the retention duration in seconds.
- `GlobalLabels`: Defines a global set of name/value label tuples applied to all metrics emitted using the wrapper functions defined in the `telemetry` package.

The `Metrics` struct has the following fields:
- `memSink`: An in-memory sink.
- `prometheusEnabled`: A boolean that indicates whether Prometheus metrics are enabled.

The `Metrics` struct has the following methods:
- `New(cfg Config)`: Creates a new instance of `Metrics`. It takes a `Config` struct as an argument and returns a pointer to a `Metrics` struct and an error. If `Enabled` is `false`, it returns `nil`. It registers a global metrics with a set of sinks as configured by the operator.
- `Gather(format string)`: Collects all registered metrics and returns a `GatherResponse` where the metrics are encoded depending on the type. Metrics are either encoded via Prometheus or JSON if in-memory.

The `telemetry` package also defines the following constants:
- `FormatDefault`: An empty string.
- `FormatPrometheus`: A string that represents the Prometheus format.
- `FormatText`: A string that represents the text format.

The `telemetry` package imports the following packages:
- `bytes`
- `encoding/json`
- `fmt`
- `time`
- `github.com/armon/go-metrics`
- `github.com/armon/go-metrics/prometheus`
- `github.com/prometheus/client_golang/prometheus`
- `github.com/prometheus/common/expfmt`

Example usage:
```go
cfg := telemetry.Config{
    ServiceName: "my-service",
    Enabled: true,
    EnableHostname: true,
    EnableHostnameLabel: true,
    EnableServiceLabel: true,
    PrometheusRetentionTime: 3600,
    GlobalLabels: [][]string{{"chain_id", "cosmoshub-1"}},
}

metrics, err := telemetry.New(cfg)
if err != nil {
    panic(err)
}

response, err := metrics.Gather(telemetry.FormatPrometheus)
if err != nil {
    panic(err)
}

fmt.Println(string(response.Metrics))
```
## Questions: 
 1. What is the purpose of the `telemetry` package in the `cosmos-sdk` project?
- The `telemetry` package provides functionality for gathering and emitting application metrics.
2. What types of metrics formats are supported by this package?
- The package supports three types of metrics formats: default, Prometheus, and text.
3. What is the purpose of the `Metrics` struct and its associated methods?
- The `Metrics` struct is a wrapper around the application telemetry functionality, allowing metrics to be gathered at any point in time. The `Gather` method collects all registered metrics and returns them in the specified format.