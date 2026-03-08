# Design: Fortune Teller Web App (Phase 1)

## Architecture
The application will use a Monolithic, Client-Server architecture.

### Backend (ASP.NET Core 10)
-   **Framework:** ASP.NET Core 10 using Minimal APIs.
-   **Structure:** Clean Architecture (Domain, Application, Infrastructure, Presentation/API layers).
-   **Core Domain:**
    -   `BirthData`: Value object containing Name, Gender, Solar Date, Time.
    -   `LunarDate`: Value object resulting from conversion.
    -   `TuViChart`: Entity representing the calculated 12 houses and stars.
    -   `Reading`: The final synthesized explanation.
-   **Infrastructure:**
    -   `LunarConversionService`: Handles Solar to Lunar calculations.
    -   `ChartCalculationService`: Implements the mathematical rules to place stars based on Lunar Data.
    -   `ExplanationEngine`: An interface (`IExplanationEngine`) with two implementations:
        1.  `RuleBasedExplanationEngine`: Uses an internal dictionary of star/house meanings.
        2.  `GeminiExplanationEngine`: Calls the Google Gemini API to synthesize the chart into natural text.

### Frontend (React / Vite)
-   **Framework:** React 19 (via Vite for fast builds).
-   **Styling:** Modern CSS framework (Tailwind CSS) + Shadcn/UI for accessible, beautiful components.
-   **State Management:** React Context or Zustand for the multi-step wizard state.
-   **Animation:** Framer Motion to handle smooth transitions between wizard steps (e.g., sliding out the "Name" step, sliding in the "Birthdate" step).
-   **Communication:** `fetch` or `axios` to communicate with the ASP.NET Minimal API backend.

## Data Flow
1.  User enters data in the React Wizard step-by-step.
2.  React POSTs `BirthData` and `ExplanationPreference` (Rule vs. AI) to `/api/v1/readings/calculate`.
3.  ASP.NET Minimal API receives the request.
4.  `LunarConversionService` converts the Solar Date to Lunar.
5.  `ChartCalculationService` generates the raw `TuViChart`.
6.  The requested `IExplanationEngine` takes the `TuViChart` and generates the final `Reading` text.
7.  The API returns the combined `TuViChart` (for visual display if desired) and the `Reading` text.
8.  React displays the result beautifully to the user.

## External Dependencies
-   **Google Gemini API:** Required for the `GeminiExplanationEngine`. An API key (`AIzaSyAa0yU1pMcbT...`) will be injected securely via `appsettings.json` / Environment Variables.
-   **Lunar Calendar Library:** A specialized .NET library (or ported algorithm) to accurately convert Vietnamese Lunar dates (which occasionally differ from Chinese Lunar dates).

## Testing Strategy
-   **Backend:** xUnit for unit testing the `ChartCalculationService` (asserting specific stars land in specific houses for known birthdates).
-   **Frontend:** Vitest + React Testing Library for component testing.
-   **End-to-End (E2E):** Playwright for automating the full wizard flow and verifying UI behavior in the browser.

## Risks & Trade-offs
-   **Gemini API Latency:** External API calls take time. The frontend must implement loading skeletons or engaging animations while waiting for the AI response.
-   **Gemini Costs/Limits:** The free tier of Gemini has rate limits. If traffic spikes, it will fail.
    -   *Mitigation:* Catch API failures gracefully and automatically fallback to the `RuleBasedExplanationEngine` so the user still gets a reading.
-   **Lunar Conversion Accuracy:** Vietnamese leap months sometimes differ from Chinese leap months. We must ensure the algorithm used specifically accounts for the Vietnamese timezone (UTC+7).
