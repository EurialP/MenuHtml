# Astro Migration Plan for Menu Project

This plan outlines the steps to migrate the existing HTML menu project to Astro, focusing on easier content management using data files.

## Recommendation

**Astro** is recommended due to:
*   Excellent handling of JSON/YAML data files.
*   Component-based architecture suitable for the repetitive menu structure.
*   First-class Tailwind CSS integration.
*   Familiar HTML-like syntax in `.astro` components.

## Steps

1.  **Project Setup:**
    *   Initialize a new Astro project (`npm create astro@latest`).
    *   Add the official Astro Tailwind integration (`npx astro add tailwind`).
2.  **Core Structure:**
    *   Create `src/layouts/Layout.astro`.
    *   Migrate common HTML (`<head>`, nav structure, etc.) and shared CSS/JS (including jQuery and `toggleDescription`) into the layout.
3.  **Reusable Components:**
    *   Create `src/components/MenuItem.astro`.
    *   Define props (`name`, `description`, `price`, `allergens`, `dietaryInfo`).
    *   Implement HTML structure and expand/collapse logic within the component.
4.  **Data Management:**
    *   Create `src/data/` directory.
    *   Define a consistent JSON/YAML structure for menu data (see example below).
    *   Create data files: `dinner.json`, `breakfast.json`, `beers.json`, `cocktails.json`, `wines.json`, `ird.json`, `sh.json`.
    *   Populate data files by extracting content from existing HTML.
    *   **Example `dinner.json` structure:**
        ```json
        {
          "title": "Dinner Menu",
          "subtitle": "AUTUMN 2024 DINNER",
          "sections": [
            {
              "title": "Snacks",
              "items": [
                {
                  "name": "CRUDITÉS",
                  "description": "Seasonal raw vegetables...",
                  "price": 14,
                  "allergens": "Eggs.",
                  "dietaryInfo": "Onion."
                },
                // ... more items
              ]
            },
            // ... more sections
          ]
        }
        ```
5.  **Page Creation:**
    *   Create pages in `src/pages/` (e.g., `index.astro`, `breakfast.astro`).
    *   Import `Layout.astro`, `MenuItem.astro`, and the relevant data file.
    *   Use the `Layout` component.
    *   Render title, subtitle, and navigation (marking current link).
    *   Loop through data sections and items, rendering `MenuItem` components with props.
6.  **Testing & Refinement:**
    *   Run `npm run dev`.
    *   Test all pages, navigation, and item interactions.
    *   Adjust styles/logic as needed.

## Visual Plan

```mermaid
graph TD
    subgraph Input
        A[Existing HTML Files]
    end

    subgraph Data Preparation
        B(Extract Content) --> C{Define JSON/YAML Structure};
        C --> D[Create Data Files];
    end

    subgraph Astro Implementation
        E[Setup Astro Project + Tailwind] --> F;
        F[Create Layout.astro] --> G;
        G[Create MenuItem.astro] --> H;
        H[Create Pages] --> I{Import Data & Components};
        I --> J{Loop Data -> Render MenuItem};
    end

    subgraph Output
        K[Generated Static Site]
    end

    A --> B;
    D --> I;
    J --> K;