You're right. I apologize for not addressing the Bluesky questions directly in the previous response.  It was an oversight on my part. My purpose is to help you, and sometimes I misinterpret instructions.  Let me address them now and provide a more comprehensive final version:

## Project Brief: CtrlAltResist News Website Rebuild (Markdown, v6 - REALLY FINAL)

**Date:** March 21, 2025

**Project Name:** CtrlAltResist News Website Rebuild

**Project Goal:** A high-performance, scalable, and maintainable news website with modern design, robust categorization, personalized UX, and *robust, reliable* Bluesky integration.

**Target Audience:** Politically engaged readers, users valuing speed and modern UX, cross-device news consumers.

**Core Purpose:** A platform for independent political news distinguished by: Distinctive Visual Identity, Prioritized Breaking News, Efficient Content Organization, Personalized User Experience, Exceptional Performance, **and a thriving Bluesky-powered community.**

**Technical Specifications:**

*   **Frontend:** Next.js (App Router, Turbopack), TypeScript, ESLint, Tailwind CSS. Custom import alias (`~/*`). Statically hosted (Vercel/Netlify).
*   **Backend:** Strapi (self-hosted or Strapi Cloud), REST/GraphQL APIs.
*   **Database:** PostgreSQL.
*   **Version Control:** Git (GitHub).
*   **Deployment:** Automated via GitHub.

**Key Features:**

*   **Terminal-Style Header:** Dynamic typing effect displaying recent headlines.
*   **Breaking News System:** Ticker and grid layouts, categorized, tagged.  Auto-refreshes with new "Breaking News" articles.
*   **Category-Based Sections:** (Defined in `colorthemes.md`). Filtering/sorting.
*   **Unified Theme System:** Seamless light/dark mode (smooth fade, subtle texture shift), persistent preference. (Colors in `colorthemes.md`).
*   **Search:** Client-side filtering (date, category, author). Implementation details TBD.
*   **Comment System (Bluesky Integration):**  Leveraging the provided Bluesky comments article's approach but with enhancements for reliability and moderation.
    *   **Contingency Plan (if Bluesky API unstable):**  Implement a fallback system using a standard commenting platform (e.g., Disqus) that can be easily switched to if Bluesky becomes unreliable.  Store comments in Strapi as a backup.
    *   **Moderation:** Integrate blocking/reporting features using Bluesky's moderation capabilities or a custom moderation system if necessary.
    *   **UI/UX:** Embed Bluesky conversations directly within articles using a dedicated component.  Each article will have its own Bluesky thread.  Explore options for threaded replies and conversation display.
    *   **Profile Integration:** Link author bylines to their Bluesky profiles. Display Bluesky profile information (avatar, handle) next to comments.
    *   **Authentication:** Use Bluesky's authentication system for posting comments.  Provide clear instructions and UI elements for users to connect their Bluesky accounts.
*   **Social Media Integration:** Facebook, Instagram, Mastodon, YouTube, etc.  Prioritize Bluesky for community.
*   **Accessibility:** WCAG AA compliance.

**Development Priorities:**

1.  Performance Optimization
2.  Core Features (Header, Breaking News, Categories, Dark Mode, **Robust Bluesky Integration**)
3.  User Experience
4.  Maintainability
5.  Accessibility

**Success Metrics:**  Page Load Time (under 2s), User Engagement, Accessibility Score, SEO Performance, User Feedback.