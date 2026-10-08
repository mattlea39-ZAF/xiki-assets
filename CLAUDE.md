# xiki-assets

Public image hosting for Xiki Agency sales and demo assets. The only purpose of
this repo is to turn a local image into a stable URL that returns the raw file
bytes, so tools like the demo builder's "Logo URL" field can load it.

## Why this repo exists

Claude artifact links (`https://claude.ai/artifact/...`) return an HTML viewer
page, never the image itself, even when sharing is public. Any field or agent
that expects a direct image URL fails on them. GitHub raw URLs return the real
file with the correct content type, so images live here instead.

## URL pattern

```
https://raw.githubusercontent.com/mattlea39-ZAF/xiki-assets/main/<filename>
```

Example, the first asset in the repo:

```
https://raw.githubusercontent.com/mattlea39-ZAF/xiki-assets/main/rider.png
```

## Adding an image

1. Copy the file into the repo root. Use a short lowercase name with no spaces,
   e.g. `coach-bryan-logo.png`, not `Screenshot 2026-10-07 at 18.12.37.png`.
2. Commit and push to `main`:
   ```
   git add <filename> && git commit -m "Add <filename>" && git push
   ```
3. Verify before handing the link over. The response must be `200` with an
   `image/*` content type:
   ```
   curl -sS -o /dev/null -w "%{http_code} %{content_type}\n" -L \
     https://raw.githubusercontent.com/mattlea39-ZAF/xiki-assets/main/<filename>
   ```

## Rules

- Keep the repo public. A private repo breaks every URL already in use.
- Never rename or delete a file that has been given out. Add a new file instead.
- Keep files small. Screenshots are fine for demos, but prefer the original
  photo over a screenshot when one is available, since screenshots are low
  resolution (the first asset is only 258 x 344 px).
- Flat structure, no subfolders, so every URL follows the same pattern.
- Only `main` is served. Do not branch for assets.
