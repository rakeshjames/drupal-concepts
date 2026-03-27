# Drupal Mastery Training

A comprehensive Drupal enablement program that blends theory, live demos, and labs. Use this guide to deliver consistent training across teams.

---

## Audience & Prerequisites
- Drupal site builders, backend developers, and front-end themers with basic PHP and Git exposure.
- Comfortable with HTML/CSS/JS fundamentals and command-line tooling.
- Local environment ready (Lando/DDEV, Composer, Node toolchain) with access to a Drupal 10 sandbox.

## Delivery Logistics
- Recommended cadence: 4 days (6 hours/day) or 8 half-days.
- Each module combines 30–40 minute lecture, 20 minute demo, and 30–45 minute lab.
- Provide slide deck, repo with starter configs, sample CSVs/APIs, and solution branch per lab.

## Local Environment Setup (DDEV)
1. Install prerequisites: recent Docker Desktop + [DDEV](https://ddev.readthedocs.io/en/stable/). Verify with `ddev version`.
2. Clone the training repository and enter the project directory.
3. Run `ddev config --project-name=drupal-training --docroot=docroot --php-version=8.2 --project-type=drupal10` (adjust values as needed).
4. Start services via `ddev start`; confirm containers and local URLs from the CLI summary.
5. Import the provided database dump with `ddev import-db --src=./resources/db.sql.gz` and files via `ddev import-files --src=./resources/files`.
6. Run `ddev drush cr` and `ddev drush uli` to rebuild caches and obtain a one-time login link.
7. (Optional) Enable Xdebug using `ddev xdebug on` when debugging, then `ddev xdebug off` afterward to keep the stack fast.

---

## Track 1 · Site Building & Content Modeling

### 1. Content Modeling Deep Dive
- **Content types & fields**: field storage vs. instances, reference fields, computed fields, translations.
- **Paragraphs**: bundle planning, reusable components, revision workflow.
- **Lab**: Build `Article` type with hero media, related content paragraph, and moderation states.

### 2. Taxonomy & Content Categorization
- Vocabulary design, hierarchical terms, synonyms, editorial workflows.
- Expose taxonomy via reference fields, tagging widgets, and auto-complete.
- **Lab**: Create `Topics` vocabulary driving contextual Views filters.

### 3. Media & Rich Content Integration
- Media Library configuration, media bundles, responsive images, remote video providers.
- Embed media in CKEditor 5, captioning, DAM considerations.
- **Lab**: Configure reusable image styles and embed gallery in Article node.

### 4. Layout & Navigation
- Block placement, custom block types, block visibility conditions.
- Menu architecture (main, footer, contextual), role-based visibility.
- Layout Builder setup: section templates, overrides, permissions, workflows.
- **Lab**: Assemble landing page with Layout Builder using hero, CTA, and feed sections.

### 5. Entities 101
- Contrast **content** entities (nodes, media, taxonomy) vs. **config** entities (content types, views).
- Entity lifecycle hooks, revisioning, translations, access control handlers.

### 6. Mastering Views
- Displays (page, block, feed, attachment) and inheritance.
- Contextual filters, relationships, exposed filters, aggregations.
- Caching strategies, query tags, debugging.
- **Lab**: Build `Resources` view with contextual author filter and attachment showing featured items.

---

## Track 2 · Custom Module Development

### 1. Module Fundamentals
- File structure (`.info.yml`, routing, services, libraries), Composer autoloading.
- Hooks overview: execution order, return expectations, Configuration vs. Runtime hooks.
- **Lab**: Scaffold `training_extensions` module with `hook_help()` and `hook_entity_insert()` logging.

### 2. Form API & Alterations
- Form arrays, validation/submit handlers, multistep forms, AJAX callbacks.
- `hook_form_alter()` and targeted alters, form states, rebuild patterns.
- **Lab**: Alter node edit form to inject conditional fieldset and validation.

### 3. Theming Preprocess & Render API
- `hook_theme()`, preprocess hooks (`hook_preprocess_node`, `hook_preprocess_field`), render arrays, theme suggestions.
- **Lab**: Add preprocess logic to append contextual links and theme suggestions for Article nodes.

### 4. OOP Patterns & Services
- Controllers returning render arrays/JSON.
- Defining services, dependency injection via constructors/traits, using service container.
- Libraries and asset attachments, menu links, and dynamic routes.
- **Lab**: Build controller that fetches service data and exposes JSON endpoint with permissions.

### 5. Plugin Development
- Plugin discovery via annotations, plugin manager basics.
- Custom block plugins, field types/formatters/widgets lifecycle, config forms.
- **Lab**: Create block plugin that calls a third-party API and caches results.

### 6. Data & Integration APIs
- **Database API / EntityQuery**: select/update, condition groups, metadata/queries, security.
- **Migration API**: architecture (source/process/destination), mapping, process plugins, rollbacks, high-water marks.
- **Event API**: events vs. hooks, subscribers, dispatching custom events.
- **Routing System**: route definitions, parameters, requirements, subscribers/alter hooks, access checks.
- **Caching API**: cache tags/contexts/max-age, cache invalidation patterns, render caching.
- **External APIs**: Guzzle clients, authentication, queue workers for retries.
- **Labs**:
  - Build EntityQuery report with CSV export.
  - Implement CSV-to-node Migration with custom process plugin.
  - Create Event Subscriber reacting to node saves to trigger a webhook.

---

## Track 3 · Theming & Front-End Experience

### 1. Custom Theme Foundations
- Theme `.info.yml`, base themes (Stable, Claro, Olivero), asset libraries, breakpoints.
- Configuration management for themes, enabling/disabling per environment.
- **Lab**: Scaffold `training_theme`, register libraries, and override core styling tokens.

### 2. Preprocess & Twig Mastery
- Twig debugging, template suggestions, includes/extends, filters/functions.
- Hooking into preprocess for nodes, fields, paragraphs; passing variables and cache metadata.
- **Lab**: Customize node and field templates to introduce design tokens and conditional badges.

### 3. Web Technologies Stack
- HTML semantics/accessibility, WAI-ARIA usage.
- Modern CSS/Sass architecture (ITCSS/BEM), variables, mixins, responsive strategy.
- JavaScript behaviors API, ES modules, progressive enhancement, decoupled components.
- Performance considerations (critical CSS, lazy loading, asset aggregation).

### 4. Single Directory Components (SDC)
- SDC structure (component.json, Twig, CSS, JS), schema definitions, props/context.
- Build a "50/50 Card" Paragraph: define fields, SDC component, theming, responsive layout, theming hooks.
- **Lab**: Implement `sdc_5050_card` component consumed by Paragraph bundle and expose toggles for image/text order.

---

## Capstone & Assessment
- Capstone project: Content-heavy microsite with custom module for external feed, tailored theme, and migration for seeding data.
- Peer code review checklist covering coding standards, accessibility, security, and performance.
- Optional certification quiz and demo day with stakeholder feedback.

## Reference Materials
- Drupal documentation: [Site Building Guide](https://www.drupal.org/docs/user_guide/en/index.html), [Developer API Reference](https://api.drupal.org/api/drupal), [Theme Developer Guide](https://www.drupal.org/docs/theming-drupal), [Plugin API](https://www.drupal.org/docs/extending-drupal/extending-and-customizing-drupal/plugins).
- Coding standards: [Drupal PHP Coding Standards](https://www.drupal.org/docs/develop/standards), [Twig Best Practices](https://www.drupal.org/docs/theming-drupal/twig-in-drupal/twig-best-practices), [JavaScript Standards](https://www.drupal.org/docs/develop/standards/javascript), [CSS/Sass Guidelines](https://www.drupal.org/docs/develop/standards/css).
- Tooling references: [Drupal Console](https://drupalconsole.com/), [Drush](https://www.drush.org/latest/), [Devel Module](https://www.drupal.org/project/devel), [Web Profiler](https://www.drupal.org/project/webprofiler), [PHPStan for Drupal](https://github.com/mglaman/phpstan-drupal), [PHPCS Drupal Coder](https://www.drupal.org/project/coder).
- Suggested further learning: [Acquia Certification Prep](https://www.acquia.com/certification), [Drupalize.Me Learning Paths](https://drupalize.me/), [Drupal Events Calendar](https://www.drupal.org/community/events), [Drupal Slack Channels](https://www.drupal.org/slack).
