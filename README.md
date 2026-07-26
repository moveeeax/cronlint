# cronlint

> The 03:00 job that never fires, and the one that fires twice.

**Status:** 🚧 In development

## Overview

Validate crontab and systemd timer schedules, warning on overlapping runs, jobs that cannot finish before the next start, and February-only expressions.

## Features

- Parses crontab syntax (ranges, steps, `@reboot`, `@daily`) and systemd `OnCalendar` expressions in one pass
- Expands the next N firings so you can read what a schedule actually does instead of what it looks like
- Flags schedules that can never fire: day 30 of February, day 31 in a 30-day-only month list
- Warns when a job's recorded runtime exceeds its interval, i.e. runs that will overlap themselves
- Detects thundering herds where dozens of jobs land on the same minute of the same hour
- Calls out DST explicitly: the hour that happens twice and the hour that does not happen at all

## Stack

Go + cobra, robfig/cron/v3 for cron parsing, `systemd-analyze calendar` for cross-checking `OnCalendar`.

## Usage

```bash
cronlint check /etc/crontab /etc/cron.d /etc/systemd/system/*.timer --next 5 --format json
```

## License

MIT
