# BUG-03: Chime Preview Sounds When Hourly Chime is Set to Off

## 1. Problem Statement
In `Clockity4.html`, clicking "Preview ♫" (`#test-chime-btn`) while the Hourly Chime option is set to `Off` (`state.hourlyChime === 'off'`) triggers a fallback bell chime (`previewType = state.hourlyChime === 'off' ? 'bell' : state.hourlyChime`). If chime is Off, previewing should inform the user that chimes are muted or offer explicit mode selection rather than unexpectedly playing sound.

## 2. Remediation
When chime is set to `off`, clicking Preview should either toast that the chime is off, or only preview when an active chime sound (Bell or Digital) is selected.

## 3. Acceptance Criteria
- [ ] Preview does not play an unprompted chime when hourly chime is disabled (`off`).
