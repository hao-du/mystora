# Tasks: Fortune Teller Initial Implementation

## 1. Project Initialization & Setup
- [ ] 1.1 Scaffold ASP.NET Core 10 Minimal API project (`FortuneTeller.Api`).
- [ ] 1.2 Scaffold Clean Architecture folders (Domain, Application, Infrastructure).
- [ ] 1.3 Initialize React 19 Frontend with Vite, Tailwind CSS, and Shadcn/UI (`fortune-teller-ui`).
- [ ] 1.4 Setup basic CORS and ensure frontend can communicate with the backend.

## 2. Backend Domain & Infrastructure
- [ ] 2.1 Define Core Domain Models (`BirthData`, `LunarDate`, `TuViChart`, `Reading`).
- [ ] 2.2 Implement `LunarConversionService` to handle Solar-to-Lunar date conversions (accounting for Vietnamese time/leap months).
- [ ] 2.3 Implement the base `ChartCalculationService` with the rules for placing stars in the 12 houses.
- [ ] 2.4 Define `IExplanationEngine` interface.

## 3. Explanation Engines (The "Dual-Engine")
- [ ] 3.1 Implement `RuleBasedExplanationEngine` with a basic, deterministic dictionary of astrological interpretations.
- [ ] 3.2 Implement `GeminiExplanationEngine` integrating the Google Gemini API (using provided key securely).
- [ ] 3.3 Add fallback logic: If `GeminiExplanationEngine` fails or rate-limits, automatically catch and fallback to `RuleBasedExplanationEngine`.

## 4. API Endpoints
- [ ] 4.1 Create POST `/api/v1/readings/calculate` Minimal API endpoint.
- [ ] 4.2 Validate incoming `BirthData` payload.
- [ ] 4.3 Wire up the services to return the correctly calculated chart and reading based on user preference (`RuleBased` or `AI`).

## 5. Frontend Development
- [ ] 5.1 Build the Multi-step Wizard component (Name -> Gender -> Time -> Preference).
- [ ] 5.2 Implement form validation to prevent advancing with an incomplete date.
- [ ] 5.3 Implement Framer Motion transitions between wizard steps.
- [ ] 5.4 Build the API integration layer (`fetch`/`axios`) to call POST `/api/v1/readings/calculate`.
- [ ] 5.5 Create an engaging Loading Component for while the API (specifically Gemini) is processing.
- [ ] 5.6 Build the Results View to elegantly display the Lunar Date, Chart Summary, and final Reading text.

## 6. Testing & Polish
- [ ] 6.1 Write unit tests for `ChartCalculationService` logic.
- [ ] 6.2 Write unit tests for `LunarConversionService`.
- [ ] 6.3 Set up Playwright and write automated end-to-end (E2E) tests for the full wizard flow, verifying both AI and Rule-Based paths trigger successfully in the browser.
