# Lifelist

Lightweight PHP recurring routine calendar built on [VC Framework](https://github.com/dsoos1290/vcframework) for PHP 5.3 and newer.

Lifelist displays per-user routines across the previous, current and next week, with flexible recurrence rules, workday exceptions and optional Catholic liturgical year indicators.

## Features

* Per-user routines with add, edit and delete actions, descriptions and custom ordering.
* Daily, weekly, alternating A/B weekly, monthly, quarterly, half-yearly, yearly and seasonal recurrence.
* Previous, current and next week views, with today's date highlighted in the Europe/Budapest timezone.
* Collapsible previous week, subdued next week and horizontally scrollable weeks on mobile.
* Expandable routine descriptions.
* Per-user calendar exceptions for holidays and working weekends.
* Optional Catholic Sunday (A/B/C) and weekday (I/II) lectionary cycle indicators.
* Hungarian and English interface languages.
* User login, password changes, CSRF protection and flash messages.
* MySQLi, optional database table prefixes, Apache URL rewriting and subdirectory support.
* No Composer dependency; PHP 5.3+ compatible.

## Requirements

* PHP 5.3+ with MySQLi.
* MySQL or MariaDB.
* Apache with `mod_rewrite`.
* JavaScript-enabled browser.

## Installation

1. Download the [latest release](https://github.com/sdaniel1335/lifelist/releases/latest) or clone the repository.
2. Copy `private_html/app/config/db-sample.php` to `private_html/app/config/db.php` and configure the database.
3. Import `install.sql` into the configured database for a new installation. An existing `users` table is retained. If using `DB_PREFIX`, update the table names and references in the SQL before importing.
4. Open the application and sign in with `admin` / `admin`.
5. **Immediately change the default password** on the Password page.
6. Add routines and configure calendar exceptions as needed.

**Security:** Change the default credentials before exposing the application to the internet. Keep `private_html` inaccessible to direct HTTP requests and set `APP_ENV` to `prod` for production.

## Configuration

* Application settings: `private_html/app/config/app.php` (`APP_URL` is optional).
* Interface language: set `APP_LANG` to `hu` (default) or `en` in the application settings. Unsupported languages fall back to English.
* Translation dictionaries: `private_html/app/config/lang_hu.php` and `private_html/app/config/lang_en.php`, using scalar constants such as `LANG_HU_WEEK` and `LANG_EN_WEEK`. The helper in `private_html/app/c/lang.php` selects the language: use `lang('WEEK')`. User-entered routine titles and descriptions are not translated.
* Database settings: `private_html/app/config/db.php` (`DB_HOST`, `DB_USER`, `DB_PASS`, `DB_NAME`, `DB_CHAR`, `DB_TIME`, `DB_PREFIX`).
* Catholic calendar indicators: set `LIFELIST_CATH` in `private_html/app/config/lifelist.php` to `true` (default) to display them, or `false` to hide them.

## Recurrence rules

* **Daily:** every day, workdays or rest days.
* **Weekly / A/B weekly:** on a selected weekday. The week containing January 1, 2026 (December 29, 2025 to January 4, 2026) is week A. The cycle alternates every Monday and continues across year boundaries. Existing internal `odd` / `even` values represent A / B; no migration is needed.
* **Monthly:** on a selected day, falling back to the last day of shorter months.
* **Every four weeks:** select 1st A, 2nd A, 1st B or 2nd B and a weekday. The cycle is 1st A -> 1st B -> 2nd A -> 2nd B, anchored to December 29, 2025 as 1st A. It continues across year boundaries and daylight saving changes. Existing fortnightly A/B rules remain available; no database migration is needed.
* **Quarterly:** in one of the quarter's 1-14 seven-day blocks, optionally on a selected weekday. The first block starts on the first day of the quarter. Block 14 is partial and does not exist in every quarter. Without a weekday, the routine appears on every day of the block.
* **Half-yearly:** in a selected month of the half-year beginning in January or July. A day value of `0` means the whole month.
* **Yearly:** on a selected month and day; February 29 falls back to February 28 in non-leap years.
* **Seasonal:** throughout spring (March-May), summer (June-August), autumn (September-November) or winter (December-February).

Workdays default to Monday-Friday. Set holidays and working Saturdays manually in the calendar exceptions below the weekly view; no holiday calendar is downloaded automatically.

Annual week numbering starts on January 1 and ends on December 31, with partial weeks at year boundaries. The A/B cycle is independent of this numbering. The A/B designation for the current and following January 1 week appears below the calendar.

The calendar projects the current rules into the past and future. Editing a routine also changes its past appearances; deleting it removes every appearance. There is no completion tracking or historical log.

## Catholic liturgical year

When enabled, each day displays the Sunday A/B/C and weekday I/II cycles after its workday or rest-day label, for example `Workday (C/II)`.

The liturgical year begins on the first Sunday of Advent. Years divisible by three use cycle C; odd years use I and even years use II. The A/B/C letter is highlighted in red and bold on the first day of the liturgical year.

## Changelog

See [CHANGELOG.md](CHANGELOG.md) for the release history.
