# Proposal: Fortune Teller Web App (Phase 1 - Lá Số Tử Vi)

## The Problem
Users looking for traditional Vietnamese astrology (Lá số tử vi) readings currently face interfaces that are either visually outdated, overly complex, or output dense, archaic astrological terminology that is very difficult for a modern layperson to understand. There is a need for a streamlined, beautiful, and accessible experience that translates complex predictive data into straightforward, human-readable insights.

## The Solution
We will build a modern, bilingual (Vietnamese/English) Web Application focused on "Lá số tử vi" as its initial offering. It will prioritize an exceptional User Experience (UX) and comprehensible results.

Key components of the solution:
1.  **Modern Onboarding:** A step-by-step wizard for data entry (Name, Gender, Time of Birth) rather than a bulky form.
2.  **Smart Date Handling:** Automatic conversion from Solar (Gregorian) dates to Lunar dates, removing a major point of friction for modern users.
3.  **Dual Explanation Engine:**
    *   **Rule-Based Mode:** A deterministic, fast, dictionary-driven text generation based on traditional meanings.
    *   **AI-Enhanced Mode (Premium/Experimental):** Integration with Google Gemini API to synthesize the raw chart data into cohesive, highly readable, and naturally flowing narrative summaries.
4.  **Stateless Architecture:** The initial version will not require user accounts or database persistence, allowing for rapid development and deployment. (State can be managed client-side or kept purely ephemeral per session).
5.  **Robust Tech Stack:** ASP.NET Core 10 (Minimal APIs, Clean Architecture) for a solid backend foundation that can scale to a full-account system later. The frontend will use the latest React ecosystem (e.g., Vite/Next.js) with modern styling and animations.

## Impact
-   **User Experience:** Will drastically lower the barrier to entry for understanding personal astrological charts.
-   **Architecture:** Establishes a clean Monolithic foundation in ASP.NET 10 that is ready for future expansion into user accounts, saved histories, and additional divination methods (e.g., Tarot, I Ching).
-   **Cost/Capability:** By implementing a switchable AI/Rule-based system, we provide a premium experience while maintaining a fallback that avoids API costs.
