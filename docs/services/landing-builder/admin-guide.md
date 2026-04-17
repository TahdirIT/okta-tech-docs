# Admin Guide (Tenant)

A tenant admin with `landing.edit` opens **Settings → Landing page**.

## Editor layout

```
┌─────────────────────────────────────────────────────────────────────────┐
│ Draft ●   [↶] [↷]   [mobile | tablet | desktop]   [ع | EN]  Save  Publish│
├──────────────┬──────────────────────────────────────────┬────────────────┤
│ Blocks       │              Canvas                      │   Inspector    │
│ Theme        │                                          │                │
│ SEO          │  (click a block to select, drag to move) │  (edit fields) │
└──────────────┴──────────────────────────────────────────┴────────────────┘
```

## Actions

- **Click a block thumb** in the left sidebar → appends to the end of the canvas.
- **Click a block on canvas** → selects it; the inspector shows its fields
  and shared settings (padding, background, max width).
- **Drag the ⋮⋮ handle** → reorder. Keyboard is also supported via the
  SortableJS accessibility wrapper.
- **Duplicate (⎘)** / **Delete (×)** buttons appear on hover over the selected block.
- **Locale switch** (`ع` / `EN`) toggles which locale you're editing — content
  is stored per-locale so you switch freely without losing work.
- **Device switch** (phone / tablet / desktop) changes the canvas width
  for visual check; it does NOT hide blocks. For per-device visibility, use
  the "Visibility" toggles inside each block's inspector.

## Draft vs Published

- Every edit goes to `draft_blocks`. The public page continues to serve
  `published_blocks` until you press **Publish**.
- **Save Draft** persists the draft without publishing.
- **Publish** copies draft → published and marks the page visible to visitors.
- An admin with `landing.publish` can also **Unpublish**, which reverts to
  showing a placeholder page to visitors.

## Saving

The editor autosaves every 5 seconds while visible. The "Unsaved" indicator
turns to "Saved HH:MM:SS" once persisted.

## Undo / Redo

`↶` / `↷` buttons. History is kept per session (50 snapshots). After a page
refresh, history resets but the draft itself is preserved.

## Tips

- Use **Theme → Primary color** to retint all CTAs in one click.
- Use **SEO** tab to set per-locale `<title>` and meta description; the
  public page writes these into `<head>` automatically.
- Avoid inline HTML unless strictly necessary — it's a Super Admin feature.
