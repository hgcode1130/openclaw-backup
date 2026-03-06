# Persistent Operational Rules

## Config-change restart gate (hard rule)
- If any config file is modified, do **not** restart immediately.
- Before any restart, run:
  - `openclaw doctor --non-interactive`
- Only restart when doctor passes without blocking errors.

## Notes
- This rule applies regardless of implementation path (manual edits, scripts, skills, or agents).
