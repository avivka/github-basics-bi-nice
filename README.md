# Power BI GitOps Demo

This repository demonstrates how data teams can use **Git** and **GitHub Actions** to manage Power BI assets with proper SDLC processes.

## Repository Structure

```
.github/workflows/          # Automated workflows
  validate-pbi-changes.yml  # Validates every Pull Request
  deploy-to-workspace.yml   # Auto-deploys on merge to main
  scheduled-refresh-monitor.yml  # Daily health check

power-bi/
  datasets/                 # Dataset configurations
  measures/                 # DAX measures as individual files
  reports/                  # Report metadata
```

## Workflow

1. **Branch** - Create a feature branch for your change
2. **Develop** - Edit measures, datasets, or report configs
3. **Pull Request** - Open a PR for team review
4. **Automated Validation** - GitHub Actions checks your changes
5. **Review & Approve** - Team lead reviews and approves
6. **Merge & Deploy** - Changes auto-deploy to Power BI workspace

## Why GitOps for Power BI?

- **Version History** - See every change, by whom, and why
- **Collaboration** - Work on changes without overwriting each other
- **Quality Gates** - Automated checks before anything goes live
- **Audit Trail** - Full traceability for compliance
- **Automation** - No more manual publishing
