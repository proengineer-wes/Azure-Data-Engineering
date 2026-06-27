# SQL Ingestion Watermark Validation

## Purpose

The SQL ingestion pipeline uses a stored watermark to support incremental loading.  
Before each execution, the pipeline should validate that the stored watermark exists and is usable.

## Validation Rules

The pipeline should check:

- Watermark value exists
- Watermark value is not empty
- Watermark value is numeric or datetime depending on source configuration
- Watermark value is not greater than the current source maximum value
- Pipeline execution should fail clearly if the watermark is invalid

## Recommended Pipeline Flow

1. Lookup stored watermark
2. Validate watermark value
3. Lookup current source maximum watermark
4. Compare stored watermark against source maximum
5. Copy only new records
6. Write updated watermark after successful copy

## Failure Handling

If the stored watermark is missing or invalid, the pipeline should stop before copying data and return a clear validation error.

Example error:

```txt
Invalid stored watermark: expected non-empty value before SQL incremental ingestion.