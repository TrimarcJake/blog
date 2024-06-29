---
title: Locksmith (AD CS Remediation Tool) v2024.3 is now available!
creation_date: March 3, 2024
modification_date: April 2, 2024
---


# Locksmith (AD CS Remediation Tool) v2024.3 is now available!

Improvements:
- Eliminated duplicated ownership check in ESC4/5. We can and should have opinions, and the opinion is that only AD Admins should own PKS objects and templates.
- Filtered Deny ACEs from ESC4/5. This is not an Effective Access check, but it does cut down on false positives.
- Added flowcharts that explain severity for each finding.
- Added comment-based help to every function.
- Added instructions for Scans parameter to the README.

In Progress:
- Check to see if Locksmith is up to date. Provide links for latest version if not up to date.
- Check to see if user running Locksmith is a member of the Protected Users group. PUG membership will impact ESC8 checks.
- Check for ESC9. Announced in August 2022! Locksmith should cover this.

Known Issues:
- msPKI-Certificate-Name-Flag check in ESC1-3 currently uses a direct comparison instead of a bitwise comparison. Could result in false negatives.

