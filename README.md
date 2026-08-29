# Denly External Uptime Monitor

[![GitHub Actions](https://img.shields.io/badge/GitHub_Actions-Uptime_Probe-2088FF?logo=githubactions&logoColor=white)](.github/workflows/external-uptime.yml)
[![Schedule](https://img.shields.io/badge/Schedule-Every_5_Minutes-2ea44f)](.github/workflows/external-uptime.yml)

An off-host availability monitor for [denlyai.com](https://denlyai.com). The probe runs on GitHub-hosted infrastructure, so it can detect failures even when the application host, local network, tunnel, or container stack is unavailable.

## How It Works

Every five minutes, the workflow:

1. Requests the public health endpoint at "https://denlyai.com/api/healthz".
2. Uses IPv4, a 20-second timeout, and bounded retry behaviour.
3. Verifies that the response body contains "status: ok".
4. Fails the GitHub Actions run when connectivity or dependency health checks fail.

A failed run becomes an external, inspectable signal that the public application or its reported dependencies are unhealthy.

## Reliability Controls

- Runs independently on GitHub-hosted Ubuntu runners
- Supports manual execution through "workflow_dispatch"
- Uses least-privilege, read-only repository permissions
- Cancels overlapping probe runs
- Enforces a three-minute job timeout
- Retries transient network failures before alerting

## Workflow

The complete implementation is in [.github/workflows/external-uptime.yml](.github/workflows/external-uptime.yml).

## Skills Demonstrated

GitHub Actions, scheduled automation, HTTP health checks, JSON validation, retry design, timeout handling, least-privilege permissions, and external service monitoring.

## Scope

This repository monitors availability and reported dependency health. It is not a substitute for full observability, incident management, latency monitoring, synthetic user journeys, or multi-region probes.
