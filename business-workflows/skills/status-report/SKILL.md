---
name: status-report
description: Status report generator. Use when users need to write a weekly report, status update, progress report, or team update. Generates professional status reports.
---

# Status Report Generator

## Overview

You help team members create clear, professional status reports for weekly updates, project reviews, or stakeholder communications.

## Report Format

```markdown
# Status Report - [Date/Period]

## Summary
[1-2 sentence overview of the period]

## Completed This Period
- [Task 1] - [Brief outcome/impact]
- [Task 2] - [Brief outcome/impact]
- [Task 3] - [Brief outcome/impact]

## In Progress
| Task | Status | ETA | Notes |
|------|--------|-----|-------|
| Task A | 70% | [Date] | [Any blockers] |
| Task B | 30% | [Date] | On track |

## Blocked/Needs Attention
- [Blocker 1]: [What's needed to unblock]
- [Blocker 2]: [What's needed to unblock]

## Next Period Plans
- [ ] Planned task 1
- [ ] Planned task 2
- [ ] Planned task 3

## Metrics (if applicable)
- KPI 1: [Value] (Target: [Target])
- KPI 2: [Value] (Target: [Target])

## Risks & Concerns
- [Risk 1]: [Mitigation plan]

## Help Needed
- [Request 1]
- [Request 2]
```

## Information Gathering

Ask the user:
1. What period is this report for?
2. What did you complete?
3. What are you working on now?
4. Any blockers or concerns?
5. Plans for next period?

## Writing Style

- **Be specific**: Use numbers and concrete outcomes
- **Be concise**: Bullet points over paragraphs
- **Highlight blockers**: Make them visible for quick action
- **Show progress**: Percentages or milestones help
- **Forward-looking**: Include next steps

## Example

User: "I need to write my weekly report. This week I fixed the login bug, reviewed 3 PRs, and started on the new dashboard feature."

Response:

# Status Report - Week of [Current Date]

## Summary
Productive week focused on bug fixes and code quality, with initial progress on the dashboard redesign project.

## Completed This Period
- Fixed critical login bug (JIRA-1234) - Users can now log in with all valid email formats
- Reviewed and approved 3 pull requests - Unblocked team members on payment and notification features
- Set up development environment for dashboard project

## In Progress
| Task | Status | ETA | Notes |
|------|--------|-----|-------|
| Dashboard Redesign | 15% | [2 weeks out] | Initial components scaffolded |

## Blocked/Needs Attention
- None currently

## Next Period Plans
- [ ] Complete dashboard header and navigation components
- [ ] Write unit tests for login fix
- [ ] Start API integration for dashboard data

## Help Needed
- Need design specs for dashboard charts from Design team
