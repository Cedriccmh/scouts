# Changelog

All notable changes to the Scouts project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [1.0.0] - 2024-10-21

### Added

#### Core System
- **Semantic-First Hybrid Search**: Implemented semantic retrieval → symbolic refinement → targeted read strategy
- **Parallel Scout System**: Support for 2-3 concurrent scout agents with independent investigation areas
- **Index-Based Navigation**: Memory Bank index as central knowledge hub for on-demand loading
- **Iterative Refinement**: Support for up to 3 rounds of progressive investigation

#### Architecture
- **withScout Command** (`commands/withScout.md`):
  - Lightweight index-based pre-check (Step 0)
  - Task type identification (Bug/Debug, Feature Development, Refactoring)
  - Structured "Known Information" template for scout coordination
  - Responsibility boundary matrix between coordinator and scouts
  - 5-step workflow with quality control checkpoints

- **Scout Agent** (`agents/scout.md`):
  - 8-step investigation workflow
  - Context reception mechanism from coordinator
  - On-demand knowledge loading from ProjectWiki and SvnLog
  - Standardized report generation with metadata
  - Quality control checklist (70%+ question coverage requirement)

#### Knowledge Ecosystem
- **Memory Bank Structure**:
  - `.kilocode/rules/memory-bank/index.md` - Central index with pointers
  - `.kilocode/ProjectWiki/` - Architecture docs and API specs
  - `.kilocode/SvnLog/` - Version control history
  - `.kilocode/sub-memory-bank/report/` - Consolidated reports
  - `.kilocode/sub-memory-bank/scout/` - Individual scout reports

#### Documentation
- **README.md**: Quick start guide with architecture overview
- **scouts-system-design.md**: System architecture and design principles
- **hybrid-search-workflow.md**: Semantic-first retrieval guidelines
- **scouts-system.md**: User guide with best practices

### Design Principles
- **On-Demand Loading**: Avoid context pollution by loading only index-referenced knowledge
- **Role Separation**: Clear boundaries between planner (withScout) and investigators (scouts)
- **Index-Centric**: Knowledge routing through central index, not full scanning
- **Semantic Priority**: Meaning-based retrieval before keyword matching

### Features
- Task type-driven search strategy optimization
- Cross-area connection mapping in consolidated reports
- Automatic report persistence with date-based naming
- Support for Bug/Debug, Feature Development, and Refactoring task types
- Future-ready for recorder agent integration (Phase 4)

---

## [Unreleased]

### Planned
- **Recorder Agent**: Automatic Memory Bank index updating
- **Advanced Analytics**: Investigation metrics and performance tracking
- **Template Library**: Pre-built investigation templates for common patterns
- **Visual Reports**: Diagram generation for architecture and dependency maps

---

## Version History

- **1.0.0** (2024-10-21): Initial release with core investigation framework

