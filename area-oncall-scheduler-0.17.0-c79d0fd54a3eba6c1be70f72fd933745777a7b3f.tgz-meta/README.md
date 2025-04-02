[![CircleCI](https://circleci.com/gh/giantswarm/area-oncall-scheduler/tree/master.svg?style=svg)](https://circleci.com/gh/giantswarm/area-oncall-scheduler/tree/master)

# Area on-call shift scheduler

This project is meant to automatically schedule on-call shifts according to a set of rules.
The rules are hardcoded for `cloud-kaas` area, but it should be modular enough to allow full configurability
and to be used by any area or team. See the `How does it work?` section below for technical details.

To simulate scheduling for a range of dates, run:

```
go run main.go
--start 2021-08-01 \
--end 2021-08-01 \
--scheduler-opsgenie-api-key dbb7ac1b-... \
--scheduler-opsgenie-schedule-name cloud_kaas_schedule \
--scheduler-opsgenie-rotation-id da8b2f62-... \
-v 3 \
--logtostderr=true \
--unavailability-strategies=AFK \
--unavailability-afk-google-calendar-id=giantswarm.io_...@group.calendar.google.com \
--unavailability-afk-allow-nightshift-pattern '(^|[\s:\-[(])(P32|p32)([\s:\-\])]|$)' \
--unavailability-strategies=ConsecutiveWeekends \
--unavailability-consecutive-weekends-cooldown-count=2 \
--unavailability-consecutive-weekends-include-fridays=false \
--unavailability-strategies=MinWait \
--unavailability-minwait-user-config user@giantswarm.io:12 \
--prioritizers=lastshift:1 \
--notifiers=oncallcalendar \
--notifier-oncallcalendar-google-calendar-id=c_g1...@group.calendar.google.com \
--notifier-oncallcalendar-impersonation-user-email=user@giantswarm.io \
--notifiers=slack \
--notifier-slack-token=xoxb-... \
--notifier-slack-channel-id=XXXXXXX \
```

To apply the shifts to opsgenie, add the `--write` flag

## How does it work?

This project uses interfaces to abstract business logic. The building blocks are:

- `Schedulers`: this is an abstraction over an external shift management tool. The goal of this interface is to 
  have knowledge about who is in the rotation, when everybody's last shift was and to schedule shifts.
  The only implementation so far uses `Opsgenie` as a backend.
  See `docs/schedulers` for more details.
- `Unavailability`: this interface defines an abstraction over reasons why one person should not be scheduled in a given date.
  There are a few implementations fo this interface. One example is the `AFK` calendar that connects to Google Calendar and 
  considers a person unavailable for oncall on a specific date if there is a calendar event starting which title start 
  with the person's name.
  See `docs/unavailability` for more details.
- `Priority`: this interface makes it possible to rank available engineers in order of priority to be able to choose 
  who should be scheduled on a given date. The only implementation considers the number of days since last shift as
  the priority.
  See `docs/priority` for more details.
- `Notifier`: this interface allows sending oncallers informations about their shifts. It can be a message, the creation 
  of a calendar entry or anything else.
  See `docs/notifier` for more details.
  
This is a diagram that describe the above interfaces and their interactions:

![Block diagram](diagram.png?raw=true "Block diagram")

1. Get a list of members of the rotation from Opsgenie
2. Apply `unavailability strategies` to check which users are available for the shift
3. Apply the `priority strategies` among available users to rank people according to scheduling rules
4. Write shift override to Opsgenie
5. Add entry in the area oncall calendar (through a `Notifier`)
6. Generate Report about the shift.
