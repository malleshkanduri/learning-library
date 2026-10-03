# Learning Hub

Generic learning tracker with local + GitHub auto-save.

## Persistence

Every change is written immediately to browser localStorage. If GitHub auto-save is configured, the app then writes the same state to `data/progress.json` through the GitHub Contents API.

The GitHub token is stored only in browser sessionStorage and is not committed or exported.

## Deploy

1. Create a GitHub repository, recommended name: `learning-hub`.
2. Push all files in this package to `main`.
3. In GitHub: Settings -> Pages -> Source -> GitHub Actions.
4. Run/allow the included `Deploy Learning Hub to GitHub Pages` workflow.
5. Open the deployed site.
6. Click `GitHub` in the top navigation.
7. Enter the repository owner/repo/branch/path and a fine-grained token.
8. The token needs repository permission `Contents: Read and write`.
9. Click `Save settings & sync`.

Default settings:
- Owner: malleshkanduri
- Repository: learning-hub
- Branch: main
- Progress path: data/progress.json

Autosave changes to `data/progress.json` do not trigger a Pages redeployment.

## Cross-device behavior

On another device/browser, open the deployed site and configure the GitHub token for that browser session. The app loads `data/progress.json` from GitHub and continues from the shared state.

Because the write API requires the current file SHA, the app refreshes the SHA before every write to reduce conflicts when switching devices.

## Sorting

The top navigation includes a Sort control:
- Newest — newest added first (default)
- Oldest — oldest added first
- Recently Completed — recently finished items first
- Learning Area — alphabetical by area, newest first within each area
- Progress — highest progress first

When the Completed tab is open and the sort is left at Newest, completed items are ordered by completion date, most recently completed first.

The All Items drawer remains an index and is ordered by Learning Area, then In Progress / To Do / Completed, then newest first.

## Header refinement

The header is now separated into two clear tiers:
- Primary row: K Learning Hub + All / To Do / In Progress / Completed
- Utility row: Search, Learning Area, Sort, All Items, sync status, GitHub, Export, Add Learning Item

The layout collapses progressively for tablet and mobile widths.

## Compact header update

Primary row:
- K Learning Hub
- All / To Do / In Progress / Completed
- Icon-only controls for auto-save status, GitHub settings, Export, and Add Learning Item

Secondary row:
- Search
- `Any Area` learning-area filter
- Sort control with an explicit sort icon and `Sort:` labels
- `Browse` opens the complete All Items navigation drawer

Hover the icon-only controls to see their purpose.

## Navigation terminology and icon refinements

- `All` is now `All Learning`, representing the combined stream across every learning area.
- Add Learning Item (`+`) is positioned beside the status navigation, after Completed.
- Auto-save is represented by a cloud/check icon with a small status dot:
  - gray = local
  - amber = saving
  - green = GitHub saved
  - red = sync error
- Hovering the auto-save icon shows the full current persistence status.

## Navigation refinement

- Add Learning Item (+) is now a separate control immediately beside the All Learning / To Do / In Progress / Completed navigation, rather than being inside that segmented group.
- `Any Area` is renamed to `All Learning Tracks`.
- `Browse` is renamed to `All Items / Tasks`.
- `All Items / Tasks` is positioned at the far-right side of the utility row, visually connecting it to the drawer that slides in from the right.

## Terminology

The application now consistently uses **Learning Track** everywhere. Both the main filter and the All Items / Tasks drawer use **All Learning Tracks**. The earlier `Learning Area` wording has been removed from the UI.

## Final terminology

- Application: Learning Library
- Status navigation: All / To Do / In Progress / Completed
- Category concept: Track
- Track filter: All Tracks
- Right-side navigation drawer: All Items
- Individual entries: Learning Items

## Header refinement

- Add Learning Item (+) is now immediately to the left of `All Items` in the utility row.
- The separate GitHub icon has been removed because it duplicated the persistence function.
- One cloud/check icon now represents the complete persistence pipeline: local auto-save plus GitHub synchronization.
- Clicking the cloud/check icon opens GitHub auto-save settings.
- Its status dot communicates local / saving / GitHub-saved / error states.
