# kk-payments SLI and SLO Definition

## Overview

This document defines the proposed service level indicators and objectives for kk-payments. These targets are proposed targets (not yet measured against production traffic).

---

# SLI 1: Availability

## Definition
Percentage of successful payment service responses over total requests.

## Measurement Method
- Data source: nginx access logs and health endpoint monitoring
- Calculation:
  Successful responses (HTTP 200-399) / Total requests × 100
- Measurement window:
  30-day rolling window

## SLO Target
99.9% availability over 30 days.

---

# SLI 2: Latency

## Definition
Percentage of payment requests completed within 500 milliseconds.

## Measurement Method
- Data source: nginx request timing logs
- Calculation:
  Requests under 500ms / Total requests × 100
- Measurement window:
  30-day rolling window

## SLO Target
95% of payment requests complete within 500ms over 30 days.

---

# SLI 3: Payment Error Rate

## Definition
Percentage of payment requests resulting in server-side failure.

## Measurement Method
- Data source: application logs and monitoring metrics
- Calculation:
  Failed payment requests (HTTP 500-599) / Total payment requests × 100
- Measurement window:
  30-day rolling window

## SLO Target
Error rate must remain below 0.5% over 30 days.

---

# Automated Rollback Thresholds

| SLI | Automated Rollback Threshold | Relationship to SLO |
|---|---|---|
| Availability | 3 consecutive failed health checks within 15 seconds | Prevents prolonged outage before 30-day target is impacted |
| Latency | Response time exceeds 2 seconds for 3 consecutive checks | Protects user experience before latency budget is exhausted |
| Payment Error Rate | Error rate exceeds 5% over 1 minute | Detects severe deployment regressions before customer impact spreads |

---

# What We Do Not Commit To

## CPU Utilization
CPU usage is excluded because high infrastructure utilization does not always correlate with customer-visible failure.

## Deployment Duration
Deployment speed is excluded because rapid deployments are less important than deployment correctness and safe rollback capability.

