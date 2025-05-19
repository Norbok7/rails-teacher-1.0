Rails 8 (2025) Beginner Best Practices

“The purpose of software is to let people do work, not to make computers happy.” – adapted from DHH

This quick‑start guide distills today’s community wisdom into 8 core principles that keep a brand‑new Rails project healthy without overwhelming you. Treat it as the baseline your VS Code Copilot agent should respect whenever it writes, rewrites, or reviews code.

## How to Use This Guide

- **Read before acting:** Always review this guide and your project’s README.md before making changes.
- **Validate actions:** Run RuboCop auto‑correct before suggesting a commit.
- **Refuse to ship code that violates critical Security or Database principles.**
- **Major Rails concepts explained:**
  - **Model:** Ruby class (in `app/models/`) that represents and manages data, usually mapped to a database table (e.g., `Book`).
  - **Controller:** Ruby class (in `app/controllers/`) that handles HTTP requests, fetches data from models, and renders views (e.g., `BooksController`).
  - **View:** Template (in `app/views/`) that generates HTML for the browser, using data from controllers (e.g., `books/index.html.erb`).
  - **Route:** Maps URLs to controller actions, defined in `config/routes.rb` (e.g., `resources :books`).
  - **Migration:** Ruby file (in `db/migrate/`) that changes the database schema (e.g., creates tables/columns).
  - **Strong Parameters:** Security feature in controllers to whitelist allowed form fields.
  - **Partial:** Reusable view snippet (e.g., `_form.html.erb`).
  - **Service Object:** Plain Ruby class (in `app/services/`) for business logic that doesn’t fit in models/controllers.
  - **Component:** Encapsulated view logic, often using ViewComponent gem (in `app/components/`).
  - **Job:** Background task, usually in `app/jobs/`, run with ActiveJob/Sidekiq.

---

1. Code Style ✏️

Follow the [Ruby Style Guide] and automate it with RuboCop (rubocop-rails, rubocop-performance).

Keep methods ≤ 5 lines and classes ≤ 100 LOC (the classic Sandi Metz rules).

Prefer named scopes, enum, and constants to “magic numbers/strings”.

Always use keyword arguments for booleans and optional params.

2. MVC Boundaries 🏛️

Thin controllers: ask models or service objects for data, then render/redirect.

Keep business logic out of views; if models feel crowded, extract service objects to app/services/.

Encapsulate presentation logic with ViewComponent (in app/components/) instead of helpers & partial soup.

3. Views & Front‑end 🎨

Default to Hotwire (Turbo + Stimulus) for most interactivity—no React/Vue needed to get started.

Avoid inline JavaScript, global CSS, and Ruby conditionals that leak business rules into views.

Extract repeated markup into partials or components with slots.

4. Database & Active Record 🗄️

Every belongs_to must have a foreign‑key constraint and an index.

Skip callbacks for multi‑step workflows; wrap them in a transaction‑safe service object instead.

Use enum for simple state machines; reach for a gem like AASM only when you need events.

5. Security 🔒

Force HTTPS (config.force_ssl = true) and redirect HTTP.

Whitelist Strong Parameters and never mass‑assign roles/permissions.

Store secrets with rails credentials:edit; never commit raw keys or tokens.

6. Background Jobs ⏱️

Use ActiveJob with Sidekiq for anything that takes more than a couple of seconds.

Keep jobs idempotent (safe to run twice) and let Sidekiq handle retries.

7. Performance ⚡

Watch for N + 1 queries; eager‑load associations with includes.

Cache expensive view fragments using Redis cache store and versioned keys.

8. Deployment & Docs 🚀📚

Build once, release many: run rails assets:precompile during your build or CI step, not on the server.

Set RAILS_ENV, RAILS_SERVE_STATIC_FILES, and RAILS_LOG_TO_STDOUT when deploying to containers or PaaS.

Keep an up‑to‑date README with quick‑start steps and required environment variables.

---

_Last updated: May 14, 2025._

