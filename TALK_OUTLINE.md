# GitHub & SDLC for Power BI Teams - Talk Outline (25 min)

---

## Part 1: Why Should You Care? (5 min)

### The Problem (2 min)
- "Who here has ever overwritten someone else's Power BI file?"
- "Who has a folder that looks like: Report_v1, Report_v2, Report_FINAL, Report_FINAL_FINAL?"
- Current pain points for data teams:
  - No version history - you can't go back
  - No collaboration safety net - people overwrite each other
  - No review process - changes go live without anyone checking
  - No audit trail - "who changed this measure and why?"
  - No automation - manual publishing, manual validation

### What is SDLC? (3 min)
- **Software Development Life Cycle** - sounds scary, but it's just a process:
  1. **Plan** - what are we changing and why?
  2. **Develop** - make the change in an isolated copy
  3. **Review** - someone else looks at it before it goes live
  4. **Test** - does it still work?
  5. **Deploy** - push it to production with confidence
  6. **Monitor** - is everything still healthy?
- "Data teams already do this informally - we're just adding structure and safety"
- Key message: **SDLC is not about slowing you down, it's about sleeping well at night**

---

## Part 2: Git Basics - The 5-Minute Version (5 min)

### What is Git? (1 min)
- A version control system - think "Track Changes" on steroids
- Every change is saved forever with who/when/why
- You can always go back to any previous version

### Core Concepts - Keep It Simple (2 min)
- **Repository (repo)** = your project folder, but with superpowers
- **Commit** = a saved snapshot with a message ("Added sales KPI measure")
- **Branch** = your own safe copy to work on without affecting anyone else
- **Pull Request (PR)** = "Hey team, I made changes - please review before merging"
- **Merge** = approved changes get combined into the main version

### Show the Flow (2 min)
Draw this on screen:

```
main branch:    ----o--------o--------o------>
                     \      /
feature branch:       o---o
                    (your changes)
```

- "You branch off, make changes, get a review, merge back"
- "Main branch is always the 'source of truth' - what's in production"

---

## Part 3: GitHub Actions & Workflows (8 min)

### What are GitHub Actions? (2 min)
- Automation that runs when things happen in your repo
- "When someone opens a PR -> automatically validate the changes"
- "When code merges to main -> automatically deploy to production"
- Think of it as: **IF this happens THEN do that**

### Anatomy of a Workflow File (3 min)
> **DEMO: Open `.github/workflows/validate-pbi-changes.yml` in the repo**

Walk through the file and explain:
```yaml
name:         # What is this workflow called?
on:           # WHEN does it trigger? (push, pull_request, schedule)
jobs:         # WHAT does it do?
  steps:      # The individual actions, in order
```

Key points:
- It's just a YAML file - human readable
- Lives in your repo under `.github/workflows/`
- GitHub runs it automatically - you don't need to do anything
- You can have multiple workflows for different purposes

### Show Real Workflow Examples (3 min)
> **DEMO: Walk through the 3 workflows in the repo**

1. **validate-pbi-changes.yml** - Runs on every PR
   - Checks that .pbix files aren't committed directly
   - Validates JSON/metadata files are well-formed
   - Posts a summary comment on the PR

2. **deploy-to-workspace.yml** - Runs when PR merges to main
   - Publishes changes to Power BI workspace
   - Could use Power BI REST API or deployment pipelines

3. **scheduled-refresh-monitor.yml** - Runs on a schedule
   - Checks dataset refresh status
   - Alerts on failures via Teams/Slack

---

## Part 4: Putting It All Together - The Data Team Workflow (4 min)

### A Day in the Life (with Git)
1. **Morning**: You get a request to add a new KPI to the sales report
2. **Branch**: Create a branch called `feature/add-sales-kpi`
3. **Develop**: Make your changes (edit measures, add visuals)
4. **Commit**: Save with message "Add gross margin KPI to sales dashboard"
5. **Push & PR**: Push to GitHub, create a Pull Request
6. **Automated checks run**: GitHub Actions validates your changes
7. **Review**: Team lead reviews the PR, suggests a label fix
8. **Fix & re-push**: You fix it, checks run again, all green
9. **Merge**: Approved! Merge to main
10. **Auto-deploy**: GitHub Actions deploys to the Power BI workspace

### Quick GitHub Copilot Mention (1 min)
- GitHub Copilot can help even non-developers:
  - Write workflow YAML files by describing what you want in English
  - Generate DAX measures from descriptions
  - Explain existing code/configs you don't understand
  - Fix errors in YAML/JSON by pasting the error message
- "You don't need to memorize YAML syntax - Copilot writes it for you"

---

## Part 5: Bridge to Next Session (3 min)

### The Missing Piece
- "Everything I showed you works great, but there's a challenge..."
- Power BI .pbix files are **binary** - Git can't show you what changed inside
- It's like tracking changes on a ZIP file - not very useful
- **This is where TMDL comes in** (next session!)

### What's Coming Next
- TMDL = **Tabular Model Definition Language**
- Currently in preview in Power BI
- It breaks your Power BI model into **readable text files**:
  - Measures become individual text files
  - Tables, relationships, roles - all as code
- This means Git can actually show you: "Aviv changed the Gross Margin measure formula"
- **Git + TMDL = true GitOps for Power BI**
- "My colleague [NAME] will deep-dive into TMDL right after this"

### Closing
- "Today: you learned the process and the automation platform"
- "Next session: you'll learn how Power BI content becomes code that fits into this process"
- "Together, these two sessions give you the full picture of GitOps for Power BI"

---

## DEMO CHECKLIST (prep before the talk)

- [ ] Have the GitHub repo open in browser (show Actions tab, PRs, etc.)
- [ ] Have VS Code / GitHub.dev open with the workflow files
- [ ] Have a pre-made PR ready to show (with Actions running)
- [ ] Optional: trigger a workflow live to show the green checkmarks
- [ ] Have this outline open on a second screen/printed out
