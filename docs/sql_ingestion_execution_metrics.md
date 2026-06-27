# SQL Ingestion Execution Metrics

## Overview

This document defines the execution metrics that should be captured for every SQL incremental ingestion pipeline run.

The objective is to improve operational visibility, troubleshooting, and long-term monitoring.

---

## Execution Metrics

Each pipeline execution should capture:

| Metric | Description |
|---------|-------------|
| pipeline_name | Name of the executed pipeline |
| run_id | Unique execution identifier |
| source_table | SQL source table |
| target_dataset | Destination dataset |
| start_time | Pipeline start time (UTC) |
| end_time | Pipeline completion time (UTC) |
| duration_seconds | Total execution time |
| rows_read | Number of records read |
| rows_written | Number of successfully written records |
| rows_rejected | Number of rejected records |
| watermark_before | Stored watermark before execution |
| watermark_after | Updated watermark after execution |
| execution_status | Success / Failed |
| failure_reason | Error message when execution fails |

---

## Monitoring Goals

Execution metrics should support:

- Pipeline monitoring
- SLA reporting
- Failure investigation
- Performance analysis
- Incremental load verification

---

## Success Criteria

A successful pipeline execution should include:

- Valid execution metadata
- Updated watermark
- Accurate row counts
- Successful completion status

---

## Failure Criteria

If execution fails:

- Preserve the previous watermark
- Record failure reason
- Record execution duration
- Record partial row counts if available