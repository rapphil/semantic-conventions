<!--- Hugo front matter used to generate the website version of this page:
linkTitle: FaaS
--->

# Semantic Conventions for FaaS Metrics

**Status**: [Experimental][DocumentStatus]

This document defines how to describe an instance of a function that runs without provisioning
or managing of servers (also known as serverless functions or Function as a Service (FaaS)) with metrics.

The conventions described in this section are FaaS (function as a service) specific. When FaaS operations occur,
metric events about those operations will be generated and reported to provide insights into the
operations. By adding FaaS attributes to metric events it allows for finely tuned filtering.

**Disclaimer:** These are initial FaaS metric instruments and attributes but more may be added in the future.

<!-- Re-generate TOC with `markdown-toc --no-first-h1 -i` -->

<!-- toc -->

- [Metric Instruments](#metric-instruments)
  * [FaaS Invocations](#faas-invocations)
- [Attributes](#attributes)
- [References](#references)
  * [Metric References](#metric-references)

<!-- tocstop -->

## Metric Instruments

The following metric instruments MUST be used to describe FaaS operations. They MUST be of the specified
type and units.

### FaaS Invocations

Below is a table of FaaS invocation metric instruments.

| Name                   | Instrument Type ([*](/specification/general/metrics-general.md#instrument-types)) | Unit         | Unit ([UCUM](/specification/general/metrics-general.md#instrument-units)) | Description                                                                  |
|------------------------|---------------------------------------------------|--------------|-------------------------------------------|------------------------------------------------------------------------------|
| `faas.invoke_duration` | Histogram                                         | milliseconds | `ms`                                      | Measures the duration of the invocation                                      |
| `faas.init_duration`   | Histogram                                         | milliseconds | `ms`                                      | Measures the duration of the function's initialization, such as a cold start |
| `faas.coldstarts`      | Counter                                           | default unit | `{coldstart}`                            | Number of invocation cold starts.                                            |
| `faas.errors`          | Counter                                           | default unit | `{error}`                                | Number of invocation errors.                                                 |
| `faas.invocations`      | Counter                                          | default unit | `{invocation}`                           | Number of successful invocations.                                            |
| `faas.timeouts`        | Counter                                           | default unit | `{timeout}`                              | Number of invocation timeouts.                                               |

Optionally, when applicable:

| Name             | Instrument Type ([*](/specification/general/metrics-general.md#instrument-types)) | Unit         | Unit ([UCUM](/specification/general/metrics-general.md#instrument-units)) | Description                                     |
|------------------|---------------------------------------------------|--------------|-------------------------------------------|-------------------------------------------------|
| `faas.mem_usage` | Histogram                                         | Bytes        | `By`                                      | Distribution of max memory usage per invocation |
| `faas.cpu_usage` | Histogram                                         | milliseconds | `ms`                                      | Distribution of CPU usage per invocation        |
| `faas.net_io`    | Histogram                                         | Bytes        | `By`                                      | Distribution of net I/O usage per invocation    |

## Attributes

Below is a table of the attributes to be included on FaaS metric events.

| Name                    | Requirement Level | Notes and examples                                                                                                       |
|-------------------------|-------------------|--------------------------------------------------------------------------------------------------------------------------|
| `faas.trigger`          | Required          | Type of the trigger on which the function is invoked. SHOULD be one of: `datasource`, `http`, `pubsub`, `timer`, `other` |
| `faas.invoked_name`     | Required          | Name of the invoked function. Example: `my-function`                                                                     |
| `faas.invoked_provider` | Required          | Cloud provider of the invoked function. Corresponds to the resource `cloud.provider`. Example: `aws`                     |
| `faas.invoked_region`   | Required          | Cloud provider region of invoked function. Corresponds to resource `cloud.region`. Example: `us-east-1`                  |

More details on these attributes, the function name and the difference compared to the faas.invoked_name can be found at the related [FaaS tracing specification](faas-spans.md).
For incoming FaaS invocations, the function for which metrics are reported is already described by its [FaaS resource attributes](../resource/semantic_conventions/faas.md).
Outgoing FaaS invocations are identified using the `faas.invoked_*` attributes above.
`faas.trigger` SHOULD be included in all metric events while `faas.invoked_*` attributes apply on outgoing FaaS invocation events only.

## References

### Metric References

Below are links to documentation regarding metrics that are available with different
FaaS providers. This list is not exhaustive.

* [AWS Lambda Metrics](https://docs.aws.amazon.com/lambda/latest/dg/monitoring-metrics.html)
* [AWS Lambda Insight Metrics](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/Lambda-Insights-metrics.html)
* [Azure Functions Metrics](https://docs.microsoft.com/azure/azure-monitor/platform/metrics-supported)
* [Google CloudFunctions Metrics](https://cloud.google.com/monitoring/api/metrics_gcp#gcp-cloudfunctions)
* [OpenFaas Metrics](https://docs.openfaas.com/architecture/metrics/)

[DocumentStatus]: https://github.com/open-telemetry/opentelemetry-specification/blob/v1.21.0/specification/document-status.md
