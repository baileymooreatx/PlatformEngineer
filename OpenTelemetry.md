<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Table of Contents**  *generated with [DocToc](https://github.com/thlorenz/doctoc)*

- [OpenTelemetry](#opentelemetry)
- [Core Components](#core-components)
- [How OpenTelemetry Works](#how-opentelemetry-works)
- [Benefits of OpenTelemetry](#benefits-of-opentelemetry)
- [OpenTelemetry vs. Predecessors](#opentelemetry-vs-predecessors)
- [Getting Started & Resources](#getting-started--resources)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

## OpenTelemetry

OpenTelemetry is an **open-source, vendor-neutral observability framework**
developed under the Cloud Native Computing Foundation (CNCF). It standardizes
how telemetry data, such as **traces, metrics, and logs**, is generated,
collected, processed, and exported from cloud-native and distributed
applications.

Unlike observability backends, **OpenTelemetry is not a storage or visualization
tool**. Instead, it acts as the universal instrumentation layer that connects
your application to any backend of your choice, including open-source tools like
Jaeger and Prometheus, or commercial platforms like Dynatrace, Google Cloud
Observability, and Signoz.

## Core Components

OpenTelemetry consists of several key components that work together:

1. **APIs**: Language-specific interfaces that define how to generate telemetry
   data.
2. **SDKs**: Implement the APIs and handle data processing, batching, and
   exporting. Supported in over 12 languages including Java, Python, Go, and
   JavaScript.
3. **Automatic Instrumentation**: Libraries that capture telemetry without
   modifying source code, enabling quick onboarding.
4. **OpenTelemetry Collector**: A **vendor-agnostic proxy** that receives,
   processes, and exports telemetry data using over 200 components.
5. **OpenTelemetry Protocol (OTLP)**: The standard wire format for transmitting
   telemetry data across services and to backends.
6. **Semantic Conventions**: Standardized naming for common telemetry data types
   to ensure consistency.

## How OpenTelemetry Works

OpenTelemetry enables **end-to-end observability** by correlating traces,
metrics, and logs through **context propagation**. When a request enters a
distributed system, OpenTelemetry injects contextual data (like trace IDs) that
flows across service boundaries.

This allows developers and SREs to:

- Track a single request across microservices (**distributed tracing**).
- Monitor system health via metrics (e.g., CPU usage, request latency).
- Debug issues using correlated logs tied to specific requests.

Data flows from instrumented applications → SDK → Collector → Observability
backend, where it’s stored and visualized.

## Benefits of OpenTelemetry

- **Vendor Neutrality**: Instrument once, export to any backend. **No vendor
  lock-in**.
- **Unified Standard**: Combines logs, metrics, and traces into a **single
  telemetry pipeline**.
- **Reduced Overhead**: Eliminates need for multiple agents or SDKs from
  different vendors.
- **Auto-Instrumentation**: Collect data in minutes without code changes.
- **Extensibility**: Customize exporters, processors, and receivers for unique
  use cases.
- **Industry Adoption**: Backed by major companies like Google, Microsoft,
  Amazon, and Red Hat.

## OpenTelemetry vs. Predecessors

OpenTelemetry was formed in **2019** through the merger of two projects:

- OpenTracing (led by CNCF): Focused on distributed tracing only.
- OpenCensus (led by Google): Covered tracing and metrics with built-in
  exporters.

| Aspect               | OpenTracing   | OpenCensus               | OpenTelemetry                  |
|----------------------|---------------|--------------------------|--------------------------------|
| Scope                | Tracing only  | Tracing + Metrics        | **Traces, Metrics, Logs**      |
| Type                 | API spec only | Libraries with exporters | **Full framework + Collector** |
| Auto-Instrumentation | Limited       | Moderate                 | **Extensive**                  |
| Status               | Archived      | Maintenance only         | **Active development**         |

OpenTelemetry combines the best of both, offering a complete, future-proof
solution.

## Getting Started & Resources

To begin with OpenTelemetry:

1. Choose your language (e.g., Python, Go, Java).
2. Add the OpenTelemetry SDK and auto-instrumentation agent.
3. Configure the OpenTelemetry Collector to export data via OTLP.
4. Send data to your preferred backend.

Free resources include:

- Official [Getting Started Guide](https://opentelemetry.io/docs/)
- Interactive [OpenTelemetry Demo](https://github.com/open-telemetry/opentelemetry-demo)
- Training courses and community SIGs
