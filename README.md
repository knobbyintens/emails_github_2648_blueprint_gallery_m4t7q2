# Integration Blueprint Gallery

Static-site source for the Integration Blueprint Gallery. Each blueprint page
lives in `blueprints/` as a markdown file with YAML front matter.

Published pages are rendered on the public gallery. Draft pages stay in the
repository for review and are not published.

## Front matter

- `title` — display title
- `slug` — stable page identifier
- `category` — always `integration-blueprint`
- `status` — `published` or `draft`
- `published_at` — publication or planned publication date
- `summary` — one-paragraph description
- `tags` — optional topic tags
- `repo_url` — optional link to the blueprint's companion implementation repository
