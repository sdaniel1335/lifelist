# Changelog

All notable changes to this project will be documented in this file.

## [0.1.0] - 2026-11-13

### Added

- Initial Lifelist application built on [VC Framework](https://github.com/dsoos1290/vcframework) with PHP 5.3+ compatibility.
- MySQLi-backed per-user routines with creation, editing, deletion, descriptions and custom ordering.
- Daily, weekly, alternating A/B weekly, monthly, quarterly, half-yearly, yearly and seasonal recurrence rules.
- Continuous A/B week rotation across year boundaries, anchored to the week containing January 1, 2026.
- Previous, current and next week calendar views with partial weeks at year boundaries and Budapest-based today highlighting.
- Collapsible previous week, subdued next week, expandable descriptions and mobile horizontal scrolling.
- Per-user calendar exceptions for holidays and working weekends.
- Optional Catholic Sunday A/B/C and weekday I/II cycle indicators with Advent year transitions.
- Hungarian and English interface translations with English fallback.
- User authentication, password changes, CSRF protection and flash messages.
- Optional database table prefixes, absolute application URL and subdirectory support.
- Apache URL rewriting and no Composer dependency.
