---
name: guideline-reviewer
description: "Review code and UI for compliance with Dynatrace Experience Standards (GUIDElines). Use when: (1) reviewing app code for GUIDEline compliance, (2) checking if UI components follow Dynatrace standards, (3) validating component usage (AppHeader, DataTable, FilterField, etc.), (4) ensuring accessibility/WCAG compliance, (5) reviewing terminology usage, (6) checking settings implementations. Triggers on: 'review for guidelines', 'check compliance', 'does this follow standards', 'GUIDEline review', 'Dynatrace standards'."
allowed-tools: view, edit, create, bash, glob, grep, ask_user, sql
---

# GUIDEline Reviewer

Review Dynatrace app code and UI for compliance with the mandatory Dynatrace Experience Standards.

## Quick Reference: Which GUIDEline Applies?

| Component/Pattern | GUIDEline | Reference |
|-------------------|-----------|-----------|
| `AppHeader`, navigation, tabs, help menu, app logo | AppHeader | [appheader.md](references/appheader.md) |
| `DataTable`, rows, columns, sorting, selection, pagination | DataTable | [datatable.md](references/datatable.md) |
| `FilterField`, filtering, query syntax, suggestions | FilterField | [filterfield.md](references/filterfield.md) |
| Connection setup, OAuth, API keys, credentials | Connections | [connections.md](references/connections.md) |
| Permission errors, access denied, missing access | Permissions | [permissions.md](references/permissions.md) |
| Settings schema, app preferences, configuration | Settings | [settings.md](references/settings.md) |
| Dashboard, tiles, ready-made dashboards | Dashboards | [dashboards.md](references/dashboards.md) |
| "Alert" vs "notification" terminology | Terminology | [alerting-terminology.md](references/alerting-terminology.md) |
| Grail table names, view names, naming conventions | Grail Naming | [grail-naming.md](references/grail-naming.md) |
| Accessibility, WCAG, keyboard nav, screen readers | Accessibility | [accessibility.md](references/accessibility.md) |

## Review Workflow

### 1. Identify Components
Scan the code/UI to identify which Dynatrace components are used:
- Navigation: AppHeader, tabs, help menu
- Data display: DataTable, FilterField
- User flows: connections, permissions, settings
- Content: dashboards, terminology

### 2. Load Relevant GUIDElines
Load only the references needed for the components found. Do NOT load all references.

### 3. Check Compliance
For each component, verify against the mandatory rules in the guideline:
- **DO** rules: Must be implemented
- **DON'T** rules: Must be avoided
- **Scenarios**: Match implementation to correct scenario

### 4. Report Findings
Use severity levels:
- **Critical**: Violates mandatory rule, blocks compliance
- **Warning**: Deviates from recommendation, should fix
- **Info**: Suggestion for improvement

### 5. Generate Checklist
For formal reviews, generate a checklist from `assets/checklist-template.md`.

## Automated Checks

Run automated checks before manual review:

```bash
# Check for common violations in a file or directory
python3 scripts/check_guidelines.py /path/to/code/

# Check specific guideline
python3 scripts/check_guidelines.py /path/to/code/ --guideline appheader
```

## Documentation Lookup (dt-app MCP)

The reference files contain GUIDEline rules (what you MUST/MUST NOT do). For implementation details, use the **dt-app MCP server**:

```python
# Component documentation (props, examples, usage)
strato_get_component("AppHeader")
strato_get_component("DataTable")
strato_get_component("FilterField")

# Search for components
strato_search("modal")

# SDK documentation
sdk_get_doc("@dynatrace-sdk/client-query")
```

Reference files include `*(dt-app MCP: ...)*` hints indicating which MCP call to use for implementation details.

## Common Violations Quick Reference

### AppHeader
- Missing help menu (mandatory)
- App logo doesn't navigate to home
- Wrong icon order in menus

### DataTable
- Missing keyboard navigation
- Inconsistent selection behavior
- No loading states

### FilterField
- Deviating from documented syntax
- Missing debounce on suggestions
- No syntax validation feedback

### Accessibility
- Missing aria-labels
- No keyboard focus indicators
- Insufficient color contrast

### Terminology
- Using "notification" when "alert" is correct (requires user action)
- Using "alert" when "notification" is correct (no action required)

## Output Formats

### Quick Review
Brief summary with pass/fail per guideline and critical issues only.

### Detailed Review
Full report with:
- Component inventory
- Per-guideline compliance status
- Specific violations with line references
- Remediation suggestions

### Checklist
Interactive checklist for tracking compliance during development.

### Design Team Report
After presenting findings, **always offer** to create a shareable markdown report file:

> "Would you like me to create a GUIDEline review report file for sharing with your design team?"

If accepted, generate a report named `GUIDEline-review-XX.md` in the project root with:
- Executive summary table (category, status, critical/warning/pass counts)
- Detailed checklists per GUIDEline category with pass/fail status
- Code snippets showing current vs. required implementation
- Priority action items (P0-P3) with file locations
- Files to change summary
- Sign-off section for Development, Design, and Accessibility roles
- Appendix with GUIDEline reference links

Use incrementing numbers (01, 02, 03...) for multiple reviews.
