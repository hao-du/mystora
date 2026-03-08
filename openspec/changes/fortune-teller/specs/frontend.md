# Specification: Fortune Teller Frontend Wizard

## Overview
This specification defines the behavior of the React/Vite frontend for the Fortune Teller application.

## BDD Requirements

### Requirement: Multi-step Navigation
- **GIVEN** a user is on Step 1 (Name Input)
- **WHEN** they enter a valid name and click "Next"
- **THEN** the UI animates smoothly to Step 2 (Gender Input).

### Requirement: Form Validation
- **GIVEN** a user is on the Date of Birth step
- **WHEN** they attempt to click "Next" without providing a complete date
- **THEN** the form prevents advancement
- **AND** displays a clear validation error message.

### Requirement: Loading State during API Call
- **GIVEN** the user has completed all wizard steps
- **WHEN** they click "Reveal My Fortune"
- **THEN** the UI displays an engaging loading animation (e.g., drawing a chart or consulting the stars)
- **AND** disables the submit button to prevent duplicate requests.

### Requirement: Displaying the Reading
- **GIVEN** the backend successfully returns a reading
- **WHEN** the loading state resolves
- **THEN** the UI smoothly transitions to the Results page
- **AND** clearly displays the translated Lunar Date
- **AND** displays the `Reading` text in a highly readable, beautifully formatted typography layout.

### Requirement: Preference Selection
- **GIVEN** the user is on the final step before submission
- **WHEN** they toggle the "Use AI for deeper insights" switch
- **THEN** the frontend updates the payload's `ExplanationType` preference accordingly.
