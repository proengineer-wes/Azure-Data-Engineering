# Data Quality Validation for SQL Ingestion

## Overview

This document defines the minimum validation rules that should be executed before incremental SQL ingestion data is committed to downstream storage.

## Validation Workflow

1. Validate source connectivity
2. Validate required columns
3. Validate primary key uniqueness
4. Validate NULL constraints
5. Validate data types
6. Validate row count
7. Validate watermark consistency
8. Commit validated records

---

## Validation Rules

### Required Columns

The pipeline must verify that all mandatory columns exist before ingestion.

### NULL Validation

Columns marked as required must not contain NULL values.

### Duplicate Key Detection

The primary key must be unique within the ingestion batch.

### Data Type Validation

Each field should match the expected SQL schema.

### Row Count Validation

Compare the number of extracted rows with the number of successfully processed rows.

### Watermark Validation

The new watermark must always be greater than or equal to the stored watermark.

---

## Failure Handling

If any validation fails:

- Stop the pipeline
- Log the validation error
- Preserve the existing watermark
- Do not load invalid records

---

## Recommended Metrics

Capture the following metrics:

- pipeline_name
- source_table
- rows_read
- rows_valid
- rows_rejected
- validation_errors
- execution_time_seconds
- watermark_before
- watermark_after