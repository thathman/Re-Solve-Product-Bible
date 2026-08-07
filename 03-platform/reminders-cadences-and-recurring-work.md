# Reminders, Cadences and Recurring Work

## Purpose
Re:Solve should make follow-up and recurring operational work easy without requiring users to create calendar events or automations for every simple reminder.

## Reminder
A Reminder is a lightweight future attention instruction attached to a user and optionally a record.

Fields may include:
- owner/recipient
- title/note
- related record
- due/remind time
- timezone
- state
- snooze
- recurrence where allowed
- completion/dismissal

Reminders feed My Work and Notifications according to personal policy.

## Record reminders
Eligible records may support `Remind me` actions, including Organisations, Contacts, Opportunities, Properties, Projects, Requests, commercial documents, invoices, renewals and knowledge reviews.

## Recurring tasks/work
Tasks and selected Client Actions can recur on a controlled schedule.

A recurrence template defines:
- schedule/timezone
- generation timing
- ownership/assignment rule
- due-date offset
- stop/end rule
- behavior when a prior occurrence remains open

Each occurrence becomes a normal Task/Client Action with its own state. Do not hide work in an opaque recurring template.

## Cadence / Activity Plan
A Cadence is a reusable sequence of follow-up activities used for sales, onboarding, renewals and client-success processes.

Possible steps:
- create task
- schedule reminder
- suggest/send approved email
- suggest/send approved WhatsApp message
- schedule meeting/booking action
- create client Request/Action
- wait period
- condition/stop when outcome occurs

Cadences should reuse Automations and Action Registry rather than becoming a second workflow engine.

## Examples
- new lead follow-up cadence
- proposal follow-up
- onboarding follow-up
- domain/service renewal cadence
- relationship review cadence

## No timesheets/HR
Recurring work does not include employee attendance, shifts, leave, timesheets or HR scheduling.

## Notifications and Attention
A due reminder creates personal attention. Repeated reminders should not create notification storms.

## API/MCP/Àríyá
Àríyá can create a personal reminder or propose a cadence through registered actions when authorized.

## Acceptance criteria
- simple reminders do not require full automation authoring
- recurring tasks create ordinary inspectable task occurrences
- cadences reuse shared workflow/action primitives
- follow-up behavior remains permission-aware
- no HR/timesheet scope is introduced
