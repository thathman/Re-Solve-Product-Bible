# Booking and Public Scheduling

## Purpose
Re:Solve may support controlled booking experiences for client meetings, consultations, reviews and service appointments without becoming a staff HR scheduling system.

## Booking type
A Booking Type may define:
- name
- purpose
- Operating Entity/Brand
- duration
- location/method
- assigned eligible user/team
- availability source
- buffer
- lead time
- booking horizon
- cancellation/reschedule policy
- intake questions/form
- client/organisation requirement
- confirmation/reminder policy
- external calendar connector
- active state

## Use cases
- discovery call
- onboarding meeting
- project review
- technical consultation
- renewal/account review
- client support escalation meeting
- service appointment where relevant

## Availability
Availability may combine configured booking windows with connected calendars. Re:Solve does not need employee attendance/shift/leave management.

## External/public booking
A booking page may be:
- public
- secure-link only
- Portal only
- invitation only

It should use Operating Entity/Brand identity and the Core UI Framework.

## Booking record
Fields may include:
- booking type
- organiser/owner
- requester/contact
- organisation
- property/project context
- start/end/timezone
- location/meeting link
- status
- intake answers
- notes
- calendar event mapping
- reminders
- cancellation/reschedule history

## States
- CONFIRMED
- TENTATIVE where supported
- CANCELLED
- RESCHEDULED
- COMPLETED
- NO_SHOW if manually recorded and useful

## Calendar connectors
Google/Microsoft/other calendar connectors can provide availability and event creation. Re:Solve remains provider-neutral.

## Notifications
Confirmation, reminder, reschedule and cancellation use the Notification/Communications platform.

## Requests/CRM
Public booking may create/link a Lead/Contact/Request according to explicit routing rules; it should not silently create duplicates.

## Àríyá
Àríyá may find permitted booking types and propose available slots using registered actions. It should not expose private calendar event details when only free/busy is required.

## Acceptance criteria
- booking does not require HR/shift management
- calendar data is minimized to required availability/context
- public booking preserves duplicate/contact rules
- timezone/rescheduling behavior is explicit
- notifications and calendar events are traceable
