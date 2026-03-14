# Publish Checklist

A public content change is not considered published until all required checks below are complete.

## Required for every new public content item
- [ ] Front matter is complete: `title`, `description`, `permalink`, `author`, `published`
- [ ] Page title and description are clear, specific, and search-facing
- [ ] The page is linked from at least one relevant internal hub page
- [ ] `docs/_data/updates.yml` includes a new entry for this change
- [ ] The page is appropriate for newsletter and/or social distribution
- [ ] Local preview/build was checked

## Required for a significant update to an existing page
- [ ] Keep original `published`
- [ ] Add or update `updated`
- [ ] Review page title/description if the scope changed
- [ ] Add an entry to `docs/_data/updates.yml` if the change is user-visible and meaningful
- [ ] Confirm at least one relevant internal page still links to it
- [ ] Local preview/build was checked

## Do NOT add an updates entry for
- [ ] Typo fixes only
- [ ] Spacing/CSS-only micro-fixes
- [ ] Internal refactors with no user-visible change
- [ ] Metadata-only edits that do not materially change the page

## Add an updates entry for
- [ ] New article
- [ ] New policy
- [ ] New how-to
- [ ] New workflow template or prompt component
- [ ] Major rewrite of an existing page
- [ ] Public terminology change
- [ ] Navigation or information-architecture change
- [ ] Any user-visible change that affects meaning, discovery, or usage


## Copy/paste updates entry template

Use this block every time you publish a meaningful public change.

```yaml
- date: YYYY-MM-DD
  type: article
  title: "Short public update title"
  url: "/public-url/"
```

### Allowed `type` values
- `article`
- `policy`
- `how-to`
- `workflow-template`
- `prompt-component`
- `terminology`
- `navigation`

### Example mappings
- New article → `article`
- New policy page → `policy`
- New how-to page → `how-to`
- New workflow template page or major prompt-library asset → `workflow-template`
- New small reusable prompt add-on → `prompt-component`
- Public rename such as Prompt templates → Prompt library → `terminology`
- Navigation / hub / category restructuring → `navigation`