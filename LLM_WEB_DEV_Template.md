**LLM-Led Project Template: Django + HTMX + Alpine.js (with Checklists)**

**Guiding Principles:**

*   **Incremental Development:** Build complexity in layers.
*   **Automated Verification:** Each stage concludes with automated tests to ensure objectives are met before proceeding. Checklists track this.
*   **Clear Deliverables:** Tangible outputs for each stage.
*   **LLM Orchestration:** Designed for an LLM PM to define/manage tasks, trigger tests, interpret results, and update checklist status, or for humans to structure work for LLM execution.

---

**Phase 1: Foundational Setup**

*(Done once per project)*

*   **Objective:** Establish the basic project structure, dependencies, and configurations.
*   **Input:** Project requirements.
*   **Key Tasks:** Django project/app setup, dependency installation, basic settings, Tailwind init, `pytest` setup, Git init.
*   **Deliverables:** Initial project structure, `requirements.txt`, `settings.py`, Tailwind config, `pytest.ini`, Git repo.
*   **Verification:** Ensure basic project runs.
*   **Tests Checklist:**
    *   `[ ]` **Django Checks Pass:** `python manage.py check` runs without critical errors.
    *   `[ ]` **Development Server Runs:** `python manage.py runserver` starts successfully.
    *   `[ ]` **Initial Test Suite Runs:** `pytest` (or `manage.py test`) executes without errors (even if no tests are written yet).
    *   `[ ]` **Version Control Initialized:** Project committed to Git.

---

**Phase 2: Static UI Implementation**

**Stage 2.1: Static Mockup (HTML + Tailwind)**

*   **Input:** UI designs/wireframes, style guide.
*   **Objective:** Create static, responsive HTML styled with Tailwind. Focus on layout, typography, responsiveness. No interactivity.
*   **ARIA Focus:** NO.
*   **Key Tasks/LLM Responsibilities:** Write semantic HTML, apply Tailwind classes, ensure basic responsiveness, write verification tests.
*   **Deliverables:** `*.html` file(s), Tailwind CSS output, verification test files.
*   **Tests Checklist:**
    *   `[ ]` **HTML Validation:** Passes W3C validation (or linter like `djlint`).
    *   `[ ]` **CSS Linting:** Passes `Stylelint` (if configured).
    *   `[ ]` **Accessibility - Basic Contrast:** Passes `axe-core` check for critical color contrast issues (via Playwright on static HTML).
    *   `[ ]` **Responsiveness - Visual Check (e.g., Playwright):**
        *   `[ ]` Mobile viewport screenshot matches baseline/expectations.
        *   `[ ]` Tablet viewport screenshot matches baseline/expectations.
        *   `[ ]` Desktop viewport screenshot matches baseline/expectations.
    *   `[ ]` **Visual Regression (Optional):** Passes Playwright visual comparison tests against approved baselines.

---

**Phase 3: Frontend Interactivity (Client-Side)**

**Stage 3.1: Alpine.js Interactivity**

*   **Input:** Static HTML (Stage 2.1), client-side interaction requirements.
*   **Objective:** Add client-side interactivity using Alpine.js. Hardcoded data only. No backend communication.
*   **ARIA Focus:** YES (Add relevant ARIA attributes for interactive elements).
*   **Key Tasks/LLM Responsibilities:** Include Alpine.js, add directives (`x-data`, `@click`, etc.), define state, write Playwright interaction tests.
*   **Deliverables:** Updated `*.html` file(s) with Alpine.js, Playwright test scripts.
*   **Tests Checklist:**
    *   `[ ]` **Playwright - Interaction Tests:**
        *   `[ ]` Test Case 1 (e.g., Dropdown toggle): Simulates click, verifies element visibility change, checks `aria-expanded`.
        *   `[ ]` Test Case 2 (e.g., Client-side validation hint): Simulates input, verifies hint appears/disappears correctly.
        *   `[ ]` ... (Add checklist items for each required interaction)
    *   `[ ]` **JS Linting:** Passes `ESLint` (if applicable).
    *   `[ ]` **Accessibility - Interactive Elements:** Passes `axe-core` check *after* interactions (via Playwright) for issues related to dynamic content/ARIA states.

---

**Phase 4: Backend Integration (Django)**

**Stage 4.1: Django Template Integration**

*   **Input:** Interactive HTML (Stage 3.1).
*   **Objective:** Convert HTML into reusable Django templates (base, partials), render with hardcoded context from a basic view.
*   **Key Tasks/LLM Responsibilities:** Create `base.html`/partials, create view/URL, pass hardcoded context, replace static values with `{{ variable }}`, write Django client tests.
*   **Deliverables:** Django template files, `views.py`, `urls.py`, Django test files (`tests.py`).
*   **Tests Checklist:**
    *   `[ ]` **Django Test Client - View Rendering:**
        *   `[ ]` View returns `200 OK`.
        *   `[ ]` Correct template(s) used (`response.templates`).
        *   `[ ]` Hardcoded context data is present in response HTML.
    *   `[ ]` **Django Template Linting:** Passes `djlint`.
    *   `[ ]` **Python Linting:** Passes `ruff`/`flake8` for `views.py`/`urls.py`.

**Stage 4.2: Django Models**

*   **Input:** Data requirements.
*   **Objective:** Define Django models, create and apply migrations.
*   **Key Tasks/LLM Responsibilities:** Define models in `models.py`, create/apply migrations, write model unit tests.
*   **Deliverables:** Updated `models.py`, migration files, model unit test files.
*   **Tests Checklist:**
    *   `[ ]` **Django Model Checks:** Passes `python manage.py check`.
    *   `[ ]` **Migrations Applied:** Database schema matches models (`makemigrations` produces "No changes detected" after `migrate`).
    *   `[ ]` **Model Unit Tests:** Passes `manage.py test` for all tests in `tests.py` related to models.

**Stage 4.3: Dynamic Views (Connecting Models to Templates)**

*   **Input:** Django templates (Stage 4.1), Django models (Stage 4.2).
*   **Objective:** Update views to fetch data from models and pass dynamically to templates.
*   **Key Tasks/LLM Responsibilities:** Modify views to use ORM, pass querysets/objects to context, update templates to display model data, write view integration tests.
*   **Deliverables:** Updated `views.py`, potentially updated templates, view integration test files.
*   **Tests Checklist:**
    *   `[ ]` **Django Test Client - View Integration Tests:**
        *   `[ ]` Test Case 1 (e.g., List view): Creates test data, requests view, asserts data from DB appears in response HTML.
        *   `[ ]` Test Case 2 (e.g., Detail view): Creates test item, requests view, asserts specific item details appear in response.
        *   `[ ]` ... (Add checklist items for each view/data scenario)
    *   `[ ]` **Python Linting:** Passes `ruff`/`flake8` for `views.py`.

---

**Phase 5: Dynamic Frontend-Backend Interaction (HTMX)**

**Stage 5.1: Implementing HTMX Interactions**

*   **Input:** Dynamic Django views/templates (Stage 4.3), Frontend with Alpine (Stage 3.1/4.3).
*   **Objective:** Implement dynamic partial updates using HTMX.
*   **Key Tasks/LLM Responsibilities:** Add `hx-*` attributes, create/modify views for partial rendering, ensure views handle `request.htmx`, write Playwright E2E tests for HTMX.
*   **Deliverables:** Updated templates with HTMX, updated views, Playwright E2E tests.
*   **Tests Checklist:**
    *   `[ ]` **Playwright - HTMX E2E Tests:**
        *   `[ ]` Test Case 1 (e.g., Load content): Simulates click, waits for HTMX request, asserts target element updated correctly with partial content, asserts NO full page reload.
        *   `[ ]` Test Case 2 (e.g., Form submission): Simulates input/submit, waits for HTMX POST, asserts target updates (e.g., success message or error validation).
        *   `[ ]` ... (Add checklist items for each HTMX interaction)
    *   `[ ]` **Django Test Client - Partial View Tests:**
        *   `[ ]` Test view endpoint directly with `HTTP_HX_REQUEST` header set.
        *   `[ ]` Assert response is `200 OK` and contains the expected HTML *partial*.
    *   `[ ]` **Python Linting:** Passes `ruff`/`flake8` for HTMX view logic.

---

**Phase 6: Refinement & Complex Features (Iterative)**

*(Add stages as needed, defining Objectives, Tasks, Deliverables, and Checklists similarly)*

**Example Stage: Stage 6.1: Django Forms & Validation**

*   **Objective:** Implement forms, handle POST, server-side validation, display errors (potentially via HTMX).
*   **Tests Checklist:**
    *   `[ ]` **Django Test Client - Form POST Tests:**
        *   `[ ]` Test valid form submission: Asserts success response/redirect, data saved to DB.
        *   `[ ]` Test invalid form submission: Asserts response contains form errors, no data saved.
    *   `[ ]` **Playwright - Form E2E Tests:**
        *   `[ ]` Test valid submission via UI: Asserts success feedback/navigation.
        *   `[ ]` Test invalid submission via UI: Asserts validation errors displayed correctly (potentially in HTMX-updated target).
    *   `[ ]` **Python Linting:** Passes for `forms.py` and related view logic.

---

**Adapting for Existing Projects:**

1.  **Analysis Phase:** Run relevant linters, checkers, and existing tests to establish a baseline checklist status.
2.  **Baseline Verification:** Document the initial pass/fail status for all applicable checklist items.
3.  **Targeted Refactoring:** Define refactoring stages with specific checklist goals (e.g., "Achieve 100% pass on Python Linting," "Implement Playwright tests for login flow and achieve pass").
4.  **Feature Integration:** Follow the template, ensuring checklists are completed for each stage of the new feature.

