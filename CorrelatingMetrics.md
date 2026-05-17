<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Table of Contents**  *generated with [DocToc](https://github.com/thlorenz/doctoc)*

- [Correlating Metrics](#correlating-metrics)
  - [Traditional Application Observability](#traditional-application-observability)
  - [Key Metrics in Traditional Observability](#key-metrics-in-traditional-observability)
  - [LLM and ML Observability: A Paradigm Shift](#llm-and-ml-observability-a-paradigm-shift)
  - [Core LLM-Specific Metrics](#core-llm-specific-metrics)
  - [Correlating Traditional and LLM Metrics](#correlating-traditional-and-llm-metrics)
  - [Tools Enabling Unified Observability](#tools-enabling-unified-observability)
  - [Best Practices for Integration](#best-practices-for-integration)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

# Correlating Metrics  

## Traditional Application Observability

Traditional application observability revolves around monitoring system health
through the **MELT stack**: Metrics, Events, Logs, and Traces. These are used to
assess infrastructure performance, detect outages, and ensure service
reliability. The focus is on deterministic systems where inputs lead to
predictable outputs.

Observability in this context answers: *“Is the system up and performing within
expected parameters?”* It relies heavily on numeric indicators like CPU usage,
memory consumption, HTTP error rates, and request latency.

## Key Metrics in Traditional Observability

Traditional systems track well-defined operational metrics:

- **Latency**: Time taken to process a request.
- **Error Rates**: Percentage of failed requests (e.g., 5xx errors).
- **Throughput**: Requests per second.
- **Resource Utilization**: CPU, memory, disk I/O.
- **Uptime/Availability**: SLA compliance.

These metrics are typically visualized using tools like Datadog, Prometheus, or
ELK Stack, and trigger alerts when thresholds are breached.

## LLM and ML Observability: A Paradigm Shift

While traditional ML observability focuses on model drift, data quality, and
numeric output stability, LLM observability deals with **non-deterministic,
text-based outputs** and complex reasoning chains. LLMs can return different
answers to the same input, making reproducibility difficult.

**Traditional monitoring may show "all green" while users receive incorrect or 
hallucinated responses**. This gap necessitates a new approach that goes beyond 
infrastructure health.

## Core LLM-Specific Metrics

LLM observability introduces qualitative and semantic metrics:

- **Token Usage**: Input/output tokens to track cost and efficiency.
- **Prompt & Response Logging**: Full capture of inputs and outputs for audit
  and debugging.
- **Hallucination Rate**: Frequency of factually incorrect or fabricated
  content.
- **Intent Alignment**: Whether the response actually addresses the user's
  query.
- **Safety & Compliance**: Detection of toxic content, PII leakage, or policy
  violations.
- **Reasoning Quality**: Soundness of logic in multi-step agent workflows.
- **Cost per Query**: Directly tied to token volume and model choice.

These metrics require **semantic evaluation**, often using LLM-as-a-judge or
human-in-the-loop scoring.

## Correlating Traditional and LLM Metrics

To achieve unified observability, teams must **correlate infrastructure metrics
with LLM-specific signals**:

1. **Latency + Token Generation Rate**: A spike in response time might be due to
   long output sequences. Correlate `p99 latency` with `tokens per second` to
   distinguish between network delays and model generation bottlenecks.

2. **Error Rates + Prompt Analysis**: High API error rates could stem from
   malformed prompts or context overflow. Trace errors back to specific prompt
   templates or retrieval failures.

3. **Resource Utilization + Model Load**: GPU/CPU spikes may correlate with
   increased LLM traffic. Use service-level tagging to link model inference
   workloads to infrastructure usage.

4. **Cost + Token & Usage Trends**: Rising costs can be traced to increased
   token consumption. Monitor `cost per token` across models and correlate with
   user engagement metrics.

5. **User Feedback + Output Quality**: Integrate thumbs-up/down feedback with
   evaluation scores to identify patterns in user satisfaction versus model
   confidence.

6. **SLOs Across Layers**: Define SLOs that combine operational (e.g., latency <
   2s) and quality (e.g., hallucination rate < 2%) metrics to reflect true user
   experience.

## Tools Enabling Unified Observability

Modern platforms bridge the gap between traditional and LLM observability:

- **LangSmith**: Combines tracing, evaluations, and real-time monitoring. Shows
  full execution trees and correlates performance with output quality.
- **Vellum.ai**: Offers prompt tracking, eval pipelines, and dataset versioning
  with integration into existing APM tools.
- **Datadog**: Correlates LLM traces with APM data, enabling root cause analysis
  across microservices and AI components.
- **OpenTelemetry (OTel)**: Provides a vendor-agnostic framework for collecting
  metrics, logs, and traces from LLM apps. Projects like **OpenLIT**
  auto-instrument LLM calls and export OTel-compatible data.
- **Elastic Stack**: Ingests prompts, responses, and safety signals into
  Elasticsearch for Kibana-powered dashboards and log search.

These tools allow **end-to-end traceability**, from user request through backend
services to LLM response and evaluation.

## Best Practices for Integration

1. **Instrument Early**: Embed observability into LLM pipelines from
   development, not just production.
2. **Use Structured Logging**: Log prompts, responses, metadata (model version,
   temperature), and evaluation scores in a consistent schema.
3. **Implement Sampling**: Run expensive evaluations (e.g., LLM-as-judge) on a
   sampled subset of traffic to balance cost and insight.
4. **Set Quality-Based Alerts**: Alert on hallucination rate > 5% or intent
   alignment score < 0.7, not just latency or error rates.
5. **Version Control Artifacts**: Track prompt templates, datasets, and
   evaluation criteria to enable reproducibility.
6. **Unify Data in a Single Platform**: Bring LLM traces, metrics, and logs into
   the same dashboard as traditional APM data for holistic visibility.

By integrating traditional and LLM-specific observability, organizations can
move from *"Is the system up?"* to *"Is the system helping the user correctly
and safely?"*
