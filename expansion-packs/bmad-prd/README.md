# Product Requirements Fetcher Expansion Pack

## Overview

This expansion pack extends BMad Method with comprehensive product requirements fetching capabilities. It's designed for teams that need to gather, consolidate, and manage product requirements from various external sources such as Jira, Confluence, GitHub, etc.

## Purpose

While the core BMad flow focuses on getting from business requirements to development (Analyst → PM → Architect → SM → Dev), many projects require sophisticated product requirements gathering and management. This expansion pack adds:

- Enhanced capabilities for fetching product requirements from various sources
- Consolidation of requirements into a unified format
- Improved traceability and context preservation for requirements
- Streamlined workflows for managing requirements throughout the development lifecycle
- Security and compliance validation

## When to Use This Pack

Install this expansion pack when your project requires:

- Gathering product requirements from multiple external sources (e.g., Jira, Confluence, GitHub)
- Consolidating requirements into a unified, actionable format
- Enhancing traceability and context for requirements throughout the development lifecycle
- Managing requirements changes and updates efficiently
- Ensuring security and compliance in requirements management
- Streamlining collaboration between product, engineering, and business teams

## What's Included

### Agents

- `prd.yaml` - Product Requirements Fetcher agent configuration

### Personas

- `prd.md` - Product Requirements Specialist persona (Wiliam)

### Templates

- `fetched-prd-tmpl.yaml` - Product requirements fetching template for specific task or feature

### Tasks

- `list-resources.md` - List all available product requirements sources
- `fetch-prd.md` - Product requirements fetching process with source and key or details of resources
- `auto-fetch-prd.md` - Automated fetching of product requirements from configured sources
- `export-prd.md` - Export fetched product requirements to markdown format

### Data

- `common-prd-resources.md` - Provides a comprehensive list of common sources where Product Requirements Documents (PRDs) and related product information are typically stored across organizations.

---

_Version: 1.0_
_Compatible with: BMad Method v4_
