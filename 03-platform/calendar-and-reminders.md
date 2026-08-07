# Platform — Calendar, Agenda and Time-Based Commitments

## Purpose
Give Users one place to understand permitted time-based commitments across Re:Solve without becoming a full calendar provider or an HR scheduling system.

Reminder behavior is further defined in `03-platform/reminders-cadences-and-recurring-work.md`.
Public/client booking is defined in `03-platform/booking-and-public-scheduling.md`.

## Sources
Calendar/Agenda can aggregate:
- Task due dates;
- Project Milestones;
- Client Actions;
- Approvals;
- Requests/follow-ups;
- Invoice/payment-schedule due dates;
- Client Service/Contract Renewals;
- Domain/Hosting/SSL Renewal Obligations;
- Maintenance windows;
- Incident milestones/updates where scheduled;
- Reminders;
- Booking records/meetings;
- commercial Cadence steps;
- plugin events;
- synced Google/Microsoft/other calendar events where configured.

There are no employee shifts, leave, attendance or Timesheet entries.

## Views
- Agenda — primary operational/mobile view;
- Day;
- Week;
- Month;
- My Calendar;
- Team Calendar where permitted;
- filtered by Organisation/Property/Project/type;
- Saved Views where useful.

Avoid building a complex calendar client when Agenda/list presentation answers the question better.

## Time-source contract
Every item should identify:
- source record/type;
- start/due/end as applicable;
- timezone;
- editable/read-only authority;
- source/provider;
- recurrence source where applicable;
- state;
- deep link/registered action;
- freshness for external/synced items.

A synced external event remains externally authoritative unless its sync contract says otherwise.

## Reminders
A Reminder is lightweight future attention attached to a User and optionally a source record.

Fields may include title/note, owner User, related record, remind time/timezone, state, snooze, optional recurrence and completion/dismissal.

Reminder does not replace the source record's own due date and should not create duplicate source state.

## Recurring work
Recurring Task definitions and Cadences may generate future source Tasks/steps. Calendar should show generated actionable occurrences rather than an opaque endless template where practical.

## Booking
Booking Types/records can create calendar commitments and optional external calendar events. Re:Solve should use free/busy or minimized event data when full event details are unnecessary.

## Actions
Depending on source:
- create Reminder;
- snooze;
- open source;
- reschedule where source allows;
- create/follow Booking;
- mark Reminder done;
- perform registered source action.

Calendar cannot invent edit permission for an external/read-only event.

## Calendar connectors
External calendar connectors may provide:
- availability/free-busy;
- read selected events;
- create/update mapped Re:Solve bookings/meetings;
- sync status/health.

Mappings and provenance prevent duplicate event creation. Sync direction/conflict policy is explicit.

## Attention / Notifications
Upcoming or overdue source conditions may generate Attention/Notifications according to domain policy. Calendar is a visualization/interaction surface, not the authority deciding urgency.

Reminder delivery can use permitted in-app/push/email/WhatsApp channels, with dedupe and quiet-hour policy.

## Àríyá
Àríyá may answer `what is due this week?`, explain schedule conflicts, create personal Reminders and propose Booking slots through registered actions. It must not expose private external calendar details when only availability is authorized.

## API / MCP
Examples:
- list_my_agenda
- list_upcoming_deadlines
- create_reminder
- snooze_reminder
- list_booking_types
- get_available_booking_slots

External calendar writes require connector permission and source ownership rules.

## PWA/mobile
Agenda is primary mobile mode. Push/Notification deep links return to source context. Timezone/locale/DST behavior is explicit. Offline state may show safely cached agenda with freshness; scheduling changes normally require connectivity unless specifically replay-safe.

## Accessibility
Calendar has an accessible list/agenda alternative; date navigation, selection and event details work by keyboard and screen reader.

## Acceptance criteria
- time commitments remain linked to authoritative source records;
- Reminder and source due date are distinct;
- external authority/editability is clear;
- Booking uses calendar connectors without becoming HR scheduling;
- renewals/maintenance/client actions can appear coherently;
- no Timesheet/attendance/leave/shift feature is introduced.

## Lovable build slices
1. Agenda with fictional unified sources.
2. Day/week/month + filters/Saved Views.
3. Reminders/snooze/recurrence.
4. Booking records + availability.
5. external calendar connector mappings/provenance.
6. mobile/PWA/timezone polish.
