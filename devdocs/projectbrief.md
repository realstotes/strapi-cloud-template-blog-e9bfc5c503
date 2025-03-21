## Project Brief: CtrlAltResist News Website Rebuild (Markdown)

**Date:** March 21, 2025

**Project Name:** CtrlAltResist News Website Rebuild

**Project Goal:** Rebuild CtrlAltResist as a high-performance, scalable, and maintainable news website using a modern tech stack, decoupling the frontend and backend for enhanced flexibility and future-proofing.

**Target Audience:**

*   Politically engaged readers seeking independent journalism.
*   Users who value a fast, clean, and modern user experience.
*   Consumers of news across multiple devices (desktop, mobile, tablet).

**Core Purpose:**

Provide a platform for independent political news that distinguishes itself through:

*   **Distinctive Visual Identity:** A unique and modern aesthetic reflecting the publication's independent and tech-savvy approach.
*   **Prioritized Breaking News:** A robust system for highlighting and delivering urgent updates, ensuring readers receive critical news first.
*   **Efficient Content Organization:** Clear and intuitive navigation with category-based sections for easy content discovery.
*   **Personalized User Experience:** Dark mode, reading preferences, and responsive design to cater to individual user needs.
*   **Exceptional Performance:** Fast loading times and smooth interactions, even under high traffic, achieved through a statically generated frontend.

**Technical Specifications:**

*   **Frontend:** Next.js (App Router, Turbopack) with TypeScript, ESLint, and Tailwind CSS. Custom import alias (`~/*`) for improved code organization. Deployed to a static hosting provider (e.g., Vercel, Netlify).
*   **Backend (Headless CMS):** Strapi (self-hosted or Strapi Cloud), providing content via REST or GraphQL APIs.
*   **Database:** PostgreSQL (or other database supported by Strapi).
*   **Version Control:** Git (GitHub).
*   **Deployment Workflow:** Automated deployments triggered by code pushes to the GitHub repository.

**Key Features:**

*   **Terminal-Style Header:** A visually distinctive header reminiscent of a terminal interface, featuring a dynamic typing effect.  This element will enhance brand recognition.  *Question: What specific text should the typing effect display?  Should it be dynamic (e.g., latest headlines) or static (e.g., the website name)?*
*   **Breaking News System:** Prominent ticker and grid layouts for breaking news, categorized and tagged for targeted delivery. Real-time updates (if feasible). *Question:  How frequently should the breaking news be updated? Should there be an option for users to dismiss or minimize the breaking news section?*
*   **Category-Based Sections:** Dedicated sections for major news categories (Politics, Economy, etc.) with customized layouts and filtering options. *Question: What specific categories should be included?  Should sub-categories be supported?*
*   **Unified Theme System (Core Function):** Seamless light and dark mode toggle with persistent user preference storage. *Question:  What is the exact color scheme for light and dark modes?  Please provide specific hex codes for primary colors (background, text, links, accents), secondary colors, and any tertiary colors.  How should the transition between modes be implemented (instant, fade, etc.)?*  *Example: Light Mode: Background: #ffffff, Text: #333333, Links: #007bff. Dark Mode: Background: #1a202c, Text: #e2e8f0, Links: #90cdf4.*  *Should there be other visual cues beyond color changes to indicate the current mode?*
*   **Search Functionality:** Robust search capabilities allowing users to quickly find relevant articles. *Question:  Should the search be client-side or server-side?  Should it include filtering options (by date, category, author)?*
*   **Comment System:** Integration with a commenting platform (e.g., Disqus) to foster community engagement. *Question:  Which commenting platform is preferred? Should commenting be enabled by default for all articles?*
*   **Social Media Integration:**  Easy sharing of articles on social media platforms. *Question: Which social media platforms should be integrated (Facebook, Twitter, X, etc.)?*
*   **Accessibility:** Adherence to WCAG guidelines for inclusive access. *Question:  Any specific accessibility requirements beyond WCAG AA compliance?*

**Development Priorities:**

1.  Performance Optimization
2.  Core Feature Implementation
3.  User Experience
4.  Maintainability
5.  Accessibility

**Success Metrics:**

*   Page Load Time (under 2 seconds)
*   User Engagement (time-on-site, bounce rate, pages/visit)
*   Accessibility Score (WCAG)
*   SEO Performance (search rankings, organic traffic)
*   User Feedback