---
name: generate-proposal
description: Generate a professional proposal from a meeting transcript. Analyzes conversation, extracts key decisions and action items, and outputs a structured proposal in markdown and Word formats.
argument-hint: '[transcript-file] [--meeting-with NAME] [--prepared-by NAME] [--project-name NAME] [--output-dir DIR] [--lang en|nl|both]'
license: MIT
---

# Generate Professional Proposal from Meeting Transcript

Convert meeting transcripts into structured, professional proposals. Analyzes the conversation, extracts key information, and outputs multiple formats (.md and .docx).

## Usage

```
/generate-proposal path/to/transcript.txt --meeting-with "Client Name" --prepared-by "Your Name" --project-name "Project_Name"
```

Minimal usage (interactive, Claude will ask for details):
```
/generate-proposal path/to/transcript.txt
```

## What This Skill Does

1. **Reads meeting transcript** and identifies key discussion points, decisions, action items, timelines, and resource needs
2. **Generates a structured proposal** following the included template:
   - Executive Summary
   - Project Overview & Objectives
   - Multi-Phase Implementation Plan
   - Timeline & Resource Allocation
   - Organizational Requirements
   - Business Model & Revenue Strategy
   - Success Metrics
   - Next Steps & Conclusion
3. **Creates Word document** (.docx) with professional formatting
4. **Optionally translates to Dutch** with `--lang nl` or `--lang both`

## Workflow

### Step 1: Gather Context

If not provided via arguments, interactively ask for:

1. **Transcript file path** (required)
2. **Who was the meeting with?** (name, role, organization)
3. **Who is preparing this proposal?** (your name)
4. **Project name** (used for file naming)
5. **Output directory** (default: same folder as transcript)
6. **Language** (default: English. Use `--lang nl` for Dutch, `--lang both` for both)

### Step 2: Analyze Transcript

Read the transcript and extract:
- **Key discussion points** and decisions made
- **Project scope** and objectives discussed
- **Timeline** mentions (dates, phases, milestones)
- **Resource requirements** (people, tools, budget)
- **Action items** and owners
- **Success criteria** mentioned
- **Concerns or risks** raised
- **Business model** elements (pricing, revenue, costs)

### Step 3: Generate Proposal

Use the template structure from `proposal-template.md` as a guide. Fill each section with specific, concrete content extracted from the transcript:

- Replace all placeholder text with real content from the transcript
- Keep sections that are relevant, remove sections without supporting content
- Add sections if the transcript covers topics not in the template
- Use active voice, specific language, named actors
- No filler words, no jargon, no vague declaratives

### Step 4: Generate Output

**Markdown output** (.md): always generated as the base format.

**Word output** (.docx): generated using the included `scripts/proposal_generator.py` if python-docx is available. The script converts markdown to a professionally formatted Word document with:
- Styled headers (24pt, 18pt, 14pt hierarchy)
- Bullet points and numbered lists
- Bold text preservation
- Horizontal separator lines
- Default font: Calibri 11pt

If python-docx is not installed, output .md only and note the dependency.

**Dutch translation** (`--lang nl` or `--lang both`):
- Claude translates the full proposal content (not just headers)
- Dutch business terminology and professional tone
- Saved as `{ProjectName}_Voorstel.md` / `.docx`

### Step 5: Save and Confirm

- Save to specified output directory (or transcript's folder)
- Show list of generated files
- Clean up temporary files

## Output Files

| Language | Markdown | Word |
|----------|----------|------|
| English | `{ProjectName}_Proposal.md` | `{ProjectName}_Proposal.docx` |
| Dutch | `{ProjectName}_Voorstel.md` | `{ProjectName}_Voorstel.docx` |

## Options

| Flag | Required | Description | Default |
|------|----------|-------------|---------|
| `transcript` | Yes | Path to meeting transcript (.txt, .md) | - |
| `--meeting-with` | No | Person/org you met with | Asked interactively |
| `--prepared-by` | No | Your name on the proposal | Asked interactively |
| `--project-name` | No | Name for file output | Asked interactively |
| `--output-dir` | No | Where to save files | Transcript's folder |
| `--lang` | No | `en`, `nl`, or `both` | `en` |
| `--no-docx` | No | Skip Word document generation | false |

## Tone Guidelines

- Direct and professional: this is a client-facing document
- Use active voice, specific language, named actors
- No filler words, no jargon, no passive voice
- Quantify where possible (timelines, budgets, metrics)
- Keep the executive summary under 3 paragraphs
- Each phase should have concrete deliverables, not vague promises

## Tips

1. **Transcript quality matters**: include speaker names, clear discussion points, and any mentioned dates or numbers
2. **Review before sending**: always review generated proposals before sharing with clients
3. **Project naming**: use underscores instead of spaces (`AI_Training` not `AI Training`)
4. **Customization**: edit `proposal-template.md` to match your preferred proposal structure
