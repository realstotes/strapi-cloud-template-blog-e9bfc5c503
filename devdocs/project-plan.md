```markdown
# CtrlAltResist Website Rebuild: Project Plan

**Date:** March 21, 2025

**Document Purpose:** This document provides a strategic, step-by-step plan for rebuilding the CtrlAltResist website using Cursor IDE, Next.js, and Strapi.  It outlines specific tasks, checklists, and key considerations for each stage of development.

## Phase 1: Project Setup and Configuration (Next.js Frontend)

**Goal:** Establish the Next.js project, configure essential tools, and create the basic project structure.

**Tasks:**

* [x] Create Next.js project using Create Next App: `npx create-next-app@latest ctrlaltresist --ts --eslint --tailwind --src --experimental-app --turbo` (This command combines all preferred options: TypeScript, ESLint, Tailwind CSS, `src` directory, App Router, and Turbopack.)
* [x] Customize Import Alias:  In `tsconfig.json`, configure the `paths` and `baseUrl` for the `~/*` alias to point to the `src` directory.  Ensure `next.config.js` is configured as well.
* [x] Install necessary packages: `npm install axios` (for API calls)
* [ ] Set up directory structure inside `src`:
    * `components/` - For reusable UI components.  Create subdirectories as needed (e.g., `shared/`, `header/`, `footer/`).
    * `styles/` - For global styles and CSS modules. Create `globals.css` and consider modular styles for components.
    * `utils/` - For helper functions and utilities. Create an `api.js` file for fetching content from your Strapi backend.
    * `app/` - This is where pages, layouts, and components related to routing are placed for the App Router. Create `layout.js` and `page.js`.

* [ ] Configure Tailwind CSS: (if not already set up by Create Next App) - Add Tailwind directives to your CSS and configure `tailwind.config.js`. Import `tailwind.css` into the root `layout.tsx` in the `app` directory.  See https://tailwindcss.com/docs/guides/nextjs


## Phase 2: Strapi Backend Setup and Content Modeling

**Goal:** Configure the Strapi backend, define content types, and populate with initial content.  Refer to the original project brief and documentation for details.

**Tasks:**

* [x] Choose Hosting: Strapi Cloud (recommended) or self-hosting (if technical expertise is available).
* [x] Set up Strapi project.
* [ ] Define Content Types in Strapi:
    * `Article`: title, content (rich text), slug, author (relation to Author), category (relation to Category), tags (relation to Tag), publishedAt (date), image (media), etc.
    * `Category`: name, slug.
    * `Author`: name, bio, profile picture (media), bluesky_handle.
    * `Tag`: name, slug.

* [ ] Configure API access: Ensure API access is configured correctly for your chosen hosting method. Note down API base URL for use in Next.js frontend.
* [ ] Populate Strapi with initial content: Create sample articles, categories, authors, and tags for testing.


## Phase 3: Connecting Next.js to Strapi

**Goal:**  Implement data fetching in Next.js to retrieve content from the Strapi API.

**Tasks:**

* [ ] Create API helper functions in `src/utils/api.js`:  Create reusable functions to fetch data from different Strapi content types (articles, categories, authors). Consider using `axios` for API calls.
* [ ] Implement data fetching in Next.js pages/components:  Use `getStaticProps` for fetching data at build time and Server Components in your `/app` directory when using dynamic routes and needing access to backend data for content, for example.

```javascript
// Example: src/app/page.tsx
import { getStaticProps } from '~/utils/api';
import { Article } from '~/components/article'

export default async function Home() {
  const articles = await getStaticProps(); //fetches articles at build time
  // ... component logic ...
}

export async function generateStaticParams() { //get a list of all paths for articles
    const articles = await getArticles()
    return articles.map((article) => ({
      slug: article.attributes.slug
    }))
  }


// Example: src/app/articles/[slug]/page.tsx
import { getArticleBySlug } from '~/utils/api';
import { notFound } from 'next/navigation'


async function ArticlePage({ params }: { params: { slug: string } }) {
    const article = await getArticleBySlug(params.slug)
    if (!article) {
        notFound()
    }
  return (
    <article>
                <h1>{article.attributes.title}</h1>
                {/* rest of your article content */}
            </article>
        )

}
export default ArticlePage;

//utils/api.ts

//fetches articles at build time
export async function getStaticProps() {
        const res = await axios.get("YOUR_STRAPI_URL/api/articles?populate=*")
        const articles = res.data.data
        return articles
}

//fetches a single article based on slug at request time
export async function getArticleBySlug(slug) {
    const res = await axios.get(`YOUR_STRAPI_URL/api/articles?populate=*&filters[slug][$eq]=${slug}`);
    const article = res.data.data[0] //accesses the first element of the returned array, since the slug should be unique, therefore only one article should exist
    return article
    }

//fetches articles to create paths at build time
async function getArticles() {
    const res = await axios.get('YOUR_STRAPI_URL/api/articles')
    const articles = res.data.data
    return articles
    }




```

* [ ] Implement Client Side Filtering in Search component, if needed.



## Phase 4: Core Feature Development

**Goal:** Develop the core features of the website, focusing on the terminal-style header, breaking news system, category sections, and dark mode.

**Tasks:**

* [ ] **Terminal-Style Header:** Create a `Header` component that fetches recent headlines from Strapi and displays them with a typing effect. Consider using a library like `react-typical` for the animation.
* [ ] **Breaking News System:** Create components for the ticker and grid layouts.  Fetch articles tagged as "Breaking News" and display them prominently. Implement auto-refresh functionality when new breaking news articles are posted.
* [ ] **Category Sections:** Create pages and components to display articles based on selected categories.  Implement filtering and sorting options.  Use dynamic routing based on slugs.  Use Server Components in `/app` directory
* [ ] **Unified Theme System (Dark Mode):** Implement the light/dark mode toggle with persistent user preference using local storage, cookies, or a similar mechanism. Integrate the color palettes from `colorthemes.md`. Create context for toggling theme.  Implement smooth fade transition.  Implement a subtle background texture/pattern change (if desired).

## Phase 5: Bluesky Integration and Community Features

**Goal:** Implement Bluesky integration for comments and community engagement, following the approach described in the provided article.  This is a *critical phase* and requires careful planning and testing.

**Tasks:**

* [ ] **Install Bluesky Comments package.**
* [ ] **Comment Component:** Create a `BlueskyComments` component. Handle authentication, display of Bluesky threads, and any necessary moderation features.  
* [ ] **Contingency Plan (Disqus):** Set up Disqus (or another platform) as a fallback if Bluesky's API proves unreliable. Develop a mechanism to easily switch between Bluesky and the fallback.  Implement comment storage in Strapi.
* [ ] **Moderation:** Implement blocking and reporting features, either using Bluesky's capabilities or a custom system.
* [ ] **Profile Integration:**  Link author bylines and comments to Bluesky profiles.  Display Bluesky profile information.
* [ ] **Bluesky Feeds/Widgets (Optional):** Explore integrating Bluesky feeds or widgets onto the website to further enhance community engagement.
* [ ] **Thorough testing** is crucial in this phase due to the Bluesky API's potential instability.  Test on different devices, browsers, and network conditions.


## Phase 6:  Additional Features and Refinements

**Goal:** Implement remaining features, polish the UI/UX, and conduct thorough testing.

**Tasks:**

* [ ] **Search:** Implement search functionality with advanced filtering. Consider server-side search if the dataset is very large.
* [ ] **Social Media Integration:** Add social sharing buttons for supported platforms.  Prioritize Bluesky sharing.  Implement functions for Bluesky posts and integrate user's Bluesky feed, if desired.
* [ ] **Accessibility:**  Conduct accessibility audits and ensure WCAG AA compliance.
* [ ] **SEO:** Implement SEO best practices (meta tags, sitemaps, structured data).
* [ ] **Performance Optimization:**  Optimize images, code splitting, caching, and other performance-enhancing techniques.
* [ ] **Cross-browser/Cross-device Testing:** Test thoroughly on different browsers and devices to ensure a consistent user experience.
* [ ] **User Acceptance Testing (UAT):**  Conduct UAT with target users to gather feedback and identify any remaining issues.

## Phase 7: Deployment and Launch

**Goal:** Deploy the website to production and announce the launch.

**Tasks:**

* [ ] Choose a static hosting provider (e.g., Vercel, Netlify).
* [ ] Configure deployment pipeline (automated deployments from GitHub).
* [ ] Deploy Strapi backend (if self-hosting).
* [ ] Deploy Next.js frontend.
* [ ] Configure domain name and DNS settings.
* [ ] Test thoroughly in production environment.
* [ ] Announce website launch!