---
name: ticket-creator
description: Bug and feature ticket creator. Use when users need to create a bug report, feature request, ticket, issue, or task. Generates standardized tickets ready for JIRA, GitHub Issues, or other tracking systems.
---

# Ticket Creator

## Overview

You help team members create well-structured tickets for bug reports, feature requests, and tasks.

## Ticket Types

### Bug Report Template

```markdown
## Title
[BUG] [Component] - Brief description

## Environment
- Product Version:
- OS/Browser:
- User Role:

## Description
[Clear description of the bug]

## Steps to Reproduce
1.
2.
3.

## Expected Behavior
[What should happen]

## Actual Behavior
[What actually happens]

## Screenshots/Logs
[Attach relevant screenshots or error logs]

## Severity
- [ ] Critical - System down, data loss
- [ ] High - Major feature broken, no workaround
- [ ] Medium - Feature broken, workaround exists
- [ ] Low - Minor issue, cosmetic

## Additional Context
[Any other relevant information]
```

### Feature Request Template

```markdown
## Title
[FEATURE] Brief description

## Problem Statement
[What problem does this solve?]

## Proposed Solution
[How should it work?]

## User Story
As a [type of user], I want [goal] so that [benefit].

## Acceptance Criteria
- [ ] Criteria 1
- [ ] Criteria 2
- [ ] Criteria 3

## Priority
- [ ] Must Have
- [ ] Should Have
- [ ] Nice to Have

## Dependencies
[List any dependencies or blockers]

## Mockups/References
[Attach any designs or reference materials]
```

## Usage

1. Ask user what type of ticket (bug or feature)
2. Gather necessary information through conversation
3. Generate formatted ticket ready for copy-paste

## Example

User: "Login is broken on mobile"

Response:

## Title
[BUG] [Authentication] - Login fails on mobile devices

## Environment
- Product Version: [Ask user]
- OS/Browser: Mobile (iOS/Android - need specifics)
- User Role: All users

## Description
Users are unable to complete the login process when accessing the application from mobile devices.

## Steps to Reproduce
1. Open application on mobile browser
2. Navigate to login page
3. Enter valid credentials
4. Tap "Login" button
5. [Need more details from user]

## Expected Behavior
User should be authenticated and redirected to dashboard.

## Actual Behavior
[Need more details - error message? Blank screen? Redirect loop?]

## Severity
- [ ] Critical
- [x] High - Major feature broken
- [ ] Medium
- [ ] Low

---

**Questions to clarify:**
1. Which mobile OS and browser?
2. What happens when you tap Login? Error message?
3. Does it work on desktop?
4. When did this start happening?
