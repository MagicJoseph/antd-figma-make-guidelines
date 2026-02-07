# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a documentation-only repository containing structured guidelines for AI code generators (primarily Figma Make) to correctly use **Ant Design v6** components. There is no build system, no tests, and no application code — only Markdown files.

## Repository Structure

Two parallel guideline sets exist:

- `guidelines/` — AntD v6 with default `@ant-design/icons`
- `guidelines-phosphor/` — AntD v6 with **Phosphor Icons** + **i18n** (i18next/react-i18next)

Both share common structure:
- `Guidelines.md` — entry point with step-by-step reading order for AI consumers
- `overview-components.md` / `overview-icons.md` — component catalog and icon usage
- `design-tokens/` — three-layer token system (Seed → Map → Alias), colors, typography, spacing
- `components/` — per-component guidelines (26 components) with API tables, examples, and usage rules

The Phosphor variant additionally includes:
- `i18n/` — internationalization guidelines with i18next namespace system and AntD locale integration

The `examples/` directory contains a sample guideline set (for a fictional "FPL" design system) used as reference for the format.

## How Guidelines Are Consumed

These Markdown files are uploaded to Figma Make (or fed to other AI tools) as context. The `Guidelines.md` file instructs the AI to read files in a specific order before generating code. When editing guidelines, preserve:

1. The step-by-step reading flow in `Guidelines.md`
2. The consistent Markdown structure: purpose → when to use → API props table → code examples → usage guidelines
3. AntD v6-specific rules (documented in `VALIDATION_REPORT.md`)

## AntD v6 Critical Rules

These must be maintained across all guideline files:

- **React 18+** required (no React 17 support)
- `variant` replaces deprecated `bordered` prop
- `destroyOnHidden` replaces deprecated `destroyOnClose` / `destroyInactiveTabPane`
- Semantic DOM styling via `classNames` and `styles` props (objects or functions)
- Theme customization via `ConfigProvider` with the three-layer token system
- All components imported from `antd` package

## Phosphor Icons Variant

The `guidelines-phosphor/` variant replaces `@ant-design/icons` with `@phosphor-icons/react`. Key differences:
- Uses a `createPhosphorIcon` wrapper to bridge Phosphor icons with AntD's `Icon` component
- Icons have a `weight` prop (`regular`, `bold`, `fill`, `thin`, `light`, `duotone`) instead of Outlined/Filled/TwoTone naming
- The `overview-icons.md` file contains the full AntD-to-Phosphor icon mapping table

## i18n Guidelines (Phosphor variant only)

The `guidelines-phosphor/i18n/` directory contains internationalization guidelines using i18next + react-i18next:
- Namespace-based translation system: `common`, `forms`, `errors`, `components`, plus feature-specific namespaces (e.g. `dashboard`, `settings`)
- All user-facing text must use `t('namespace:key')` — no hardcoded strings
- AntD locale integration via `ConfigProvider` with `locale` prop
- Supported languages: EN, PL, CS (with instructions for adding more)
- The `Guidelines.md` in the Phosphor variant includes i18n as a required reading step and code generation rules

## Editing Guidelines

When adding or modifying component guidelines:
- Keep both `guidelines/` and `guidelines-phosphor/` variants in sync (same components, same API docs, different icon examples)
- Follow the existing Markdown template structure from other component files
- Validate against official AntD v6 API docs — see `VALIDATION_REPORT.md` for the validation checklist
