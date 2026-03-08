# Specification: Fortune Teller Backend API

## Overview
This specification defines the behavior of the ASP.NET Core 10 backend API for calculating and explaining "Lá số tử vi" charts.

## BDD Requirements

### Requirement: Calculate Tử Vi Chart
- **GIVEN** a valid `BirthData` payload containing Name, Gender, Solar Date, and Time
- **AND** the preference `ExplanationType` is set to "RuleBased"
- **WHEN** a POST request is made to `/api/v1/readings/calculate`
- **THEN** the system returns a `200 OK`
- **AND** the response contains the converted `LunarDate`
- **AND** the response contains the calculated `TuViChart` data structure
- **AND** the response contains a locally generated `Reading` string based on dictionary rules.

### Requirement: Convert Solar to Lunar Date
- **GIVEN** a Solar date of "1990-05-15" (UTC+7 assumed)
- **WHEN** the `LunarConversionService` processes the date
- **THEN** it correctly identifies the corresponding Vietnamese Lunar date
- **AND** correctly identifies if it is a leap month.

### Requirement: AI Explanation Generation
- **GIVEN** a successfully calculated `TuViChart`
- **AND** the preference `ExplanationType` is set to "AI"
- **WHEN** the `GeminiExplanationEngine` is invoked
- **THEN** it sends a properly formatted prompt containing the chart data to the Google Gemini API
- **AND** returns the resulting natural language `Reading`.

### Requirement: AI Fallback
- **GIVEN** a request specifying `ExplanationType` = "AI"
- **WHEN** the Google Gemini API returns an error, times out, or rate limits
- **THEN** the system catches the exception
- **AND** automatically falls back to the `RuleBasedExplanationEngine`
- **AND** returns a `200 OK` with a flag indicating the fallback occurred.

### Requirement: Invalid Input Handling
- **GIVEN** an API request missing required fields (e.g., missing Time of Birth)
- **WHEN** a POST request is made to `/api/v1/readings/calculate`
- **THEN** the API returns a `400 Bad Request` with validation errors.
