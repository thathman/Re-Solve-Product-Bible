# Client Success and Account Operations

## Purpose
Client Success gives staff a relationship-level view after an Organisation becomes an active client. It complements CRM acquisition, Projects delivery, Support context and Billing without duplicating them.

## Core concepts

### Account Team
Named operational responsibilities on an Organisation, such as:
- Account Owner
- Technical Owner
- Delivery/Project Owner
- Finance Owner
- Support/Relationship Owner

This is assignment/ownership metadata, not HR.

### Client Health
A derived, explainable relationship state assembled from relevant evidence.

Potential factors:
- open/at-risk projects
- unresolved client actions
- property posture/incidents
- renewal exposure
- support escalations
- overdue receivables
- contract/service status
- onboarding/offboarding state
- recent relationship activity
- manually recorded risk/context

Health must show reasons and freshness. Avoid opaque magic scores as the only explanation.

### Relationship Review
A periodic account/QBR-style record that captures:
- current goals/context
- services
- projects
- properties
- renewals
- support/incidents
- commercial opportunities
- receivables
- risks/issues
- decisions
- actions
- client-facing summary where used

## Main surfaces
Client Success may live primarily inside `Clients` and Organisation 360 rather than becoming an unnecessarily separate root app.

Views:
- Portfolio Overview
- At Risk / Needs Attention
- Renewals
- Onboarding
- Relationship Reviews
- Former/Offboarding

## Client health states
Suggested semantic states:
- HEALTHY
- WATCH
- AT_RISK
- CRITICAL
- ONBOARDING
- OFFBOARDING
- UNKNOWN

The state is not a credit score or employee-performance metric.

## Touch/follow-up
Relationship activity can include meetings, calls, emails, notes, Requests and meaningful WhatsApp communications according to connector/privacy policy.

Users may set reminders/follow-ups through My Work and the shared Reminder system.

## Renewals
Upcoming service/contract/property renewals should appear alongside account context, with responsibility and next action.

## Sales handoff
Renewal or expansion opportunity may create/link an Opportunity without losing client context.

## Attention and notifications
Examples:
- client health degraded
- major renewal approaching with no owner/action
- onboarding blocked
- client review overdue
- important relationship follow-up due

Do not notify on every underlying domain event if Attention already groups the condition.

## Àríyá
Àríyá may produce an account briefing explaining the current state using permitted source records and freshness.

## Reports
Client Success reporting may cover:
- portfolio health distribution
- upcoming renewals
- onboarding status
- relationship reviews due
- client risks
- expansion/renewal pipeline

No HR/timesheet utilization reporting is included.

## Acceptance criteria
- relationship health is explainable
- account team responsibilities do not create HR records
- client success reuses Projects/Billing/Support/Properties rather than duplicating their truth
- renewals and onboarding are first-class operational concerns
- Àríyá can summarize with evidence
