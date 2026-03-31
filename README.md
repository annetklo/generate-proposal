# Generate Proposal - Claude Code Plugin

Convert meeting transcripts into structured, professional proposals. Claude analyzes the conversation, extracts key decisions and action items, and outputs a proposal in markdown and Word formats.

## Install

```bash
claude plugin add github:annetklo/generate-proposal
```

## Usage

Interactive (Claude will ask what it needs):
```
/generate-proposal path/to/transcript.txt
```

With arguments:
```
/generate-proposal path/to/transcript.txt --meeting-with "Jane Smith, CTO, Acme Corp" --prepared-by "Your Name" --project-name "Platform_Integration"
```

## What it does

You give Claude a meeting transcript. Claude reads the full conversation and produces a structured proposal:

1. **Executive Summary** of the project and value proposition
2. **Project Overview** with objectives and core principles
3. **Implementation Plan** with phased approach, deliverables per phase, and timelines
4. **Resource Allocation** with roles, responsibilities, and time commitments
5. **Organizational Requirements** and gaps to address
6. **Business Model** with revenue strategy and expected outcomes
7. **Success Metrics** per phase with concrete targets
8. **Next Steps** with owners and deadlines

## Example output

```
## Executive Summary

Acme Corp needs a unified data platform to replace three disconnected
systems. This proposal outlines a 12-week, three-phase approach: data
audit (weeks 1-3), migration architecture (weeks 4-8), and pilot
rollout (weeks 9-12). Expected outcome: 40% reduction in data
reconciliation time and a single source of truth for all departments.

## Implementation Plan

### Phase 1: Data Audit & Requirements (Weeks 1-3)
**Focus:** Map current data flows and identify integration points

**Deliverables:**
- Data flow diagram covering all three systems
- Gap analysis report with prioritized integration points
- Technical requirements document for migration architecture
```

## Output files

| Language | Markdown | Word |
|----------|----------|------|
| English | `{ProjectName}_Proposal.md` | `{ProjectName}_Proposal.docx` |
| Dutch | `{ProjectName}_Voorstel.md` | `{ProjectName}_Voorstel.docx` |

## Options

| Flag | Required | Description | Default |
|------|----------|-------------|---------|
| `transcript` | Yes | Path to meeting transcript | - |
| `--meeting-with` | No | Person/org you met with | Asked interactively |
| `--prepared-by` | No | Your name on the proposal | Asked interactively |
| `--project-name` | No | Name for file output | Asked interactively |
| `--output-dir` | No | Where to save files | Transcript's folder |
| `--lang` | No | `en`, `nl`, or `both` | `en` |
| `--no-docx` | No | Skip Word document generation | - |

## Language support

Default output is English. Use `--lang nl` for Dutch, or `--lang both` to generate both languages.

## Customization

Edit `proposal-template.md` inside the plugin to change the default proposal structure (add/remove sections, reorder, change prompts).

## Requirements

- Claude Code CLI
- Optional: `python-docx` for .docx output (`pip install python-docx`)

## License

MIT — Built by [Mission Relearn](https://missionrelearn.com), an AI consultancy in the Netherlands.
