# 05 Integrations and APIs

## Purpose

This chapter documents technical integrations and external interfaces.

## Integration Types

- Browser libraries via CDN (diagram and code highlighting)
- Static hosting runtime and cache behavior
- Test automation runtime
- Optional data-enrichment sources for model metadata

## Public Interface Surface

Copilot Cockpit does not expose a traditional backend API in normal operation.

Effective interfaces are:

- URL routes and hash-based deep-link conventions
- JSON catalog schema and IDs
- Search result navigation contracts

## Deep-Link Interface Contracts

Examples:

- Instrument target convention
- Model target convention
- Control/scan target convention

These conventions are product-critical and must remain stable or be migrated with backward compatibility notes.

## Compatibility Considerations

- Browser support for modern JS and fetch
- Mermaid rendering compatibility
- Correct static asset and JSON cache behavior

## Change Management

Any integration-related change should include:

1. Impacted pages and contracts
2. Backward-compatibility assessment
3. Regression test plan
4. Rollback strategy
