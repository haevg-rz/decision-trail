# Changelog

All notable changes to **the-way** (the method) are recorded here. The method is
versioned with semver; adopting projects cite the version they copied (ADR-0008).

The format is loosely based on [Keep a Changelog](https://keepachangelog.com/).

## [1.2.0] - 2026-06-28

### Changed
- ADR-0010 — adopters keep the full method text in `docs/working-method.md`;
  the adopter's `AGENTS.md` carries only a fixed `## How we work` pointer (the
  same in every repo). Pins down the previously-undefined merge text and closes
  a circular reference (`AGENTS.md` → `0001` → `AGENTS.md`) that left the method
  text nowhere. Amends ADR-0009. The `starter/` skeleton moves its method body
  to `starter/docs/working-method.md`.

## [1.1.0] - 2026-06-28

### Changed
- ADR-0009 — adopting projects use conventional, unbranded locations
  (`docs/decisions/` for ADRs, plus `docs/ideas/`, `docs/plans/`); the branded
  `the-way/` subfolder is dropped. Amends ADR-0005 and ADR-0008. The `starter/`
  skeleton is restructured to `AGENTS.md` + `docs/{ideas,decisions,plans}/`.

## [1.0.0] - 2026-06-28

First settled release of the method. The full lifecycle is mechanized in plain
markdown, every choice borrowed from an existing standard and recorded as an ADR.

### Added
- ADR-0001 — record decisions as ADRs (`decisions/`).
- ADR-0002 — capture ideas as small markdown files (`ideas/`).
- ADR-0003 — a proposal is an ADR in the `proposed` status.
- ADR-0004 — a plan carries a decision into action (`plans/`); execution is the
  plan in motion.
- ADR-0005 — repo layout and cross-linking conventions.
- ADR-0006 — `AGENTS.md` as the tool-agnostic entry point.
- ADR-0007 — `AGENTS.md` as the single source of truth; concept phase settled.
- ADR-0008 — adopt the-way via a copied `starter/` skeleton; version this repo
  as the standard.
