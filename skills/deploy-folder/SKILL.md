---
name: deploy-folder
description: Publish a local folder of static HTML, CSS and JavaScript to Ullbek hosting. Use when the user has a static site in the current project and wants it hosted, deployed or put online.
argument-hint: [path to the site folder]
---

Deploy a static site from the user's disk to Ullbek hosting.

1. Confirm the folder (`$ARGUMENTS`, or ask). It must be a finished static site: HTML, CSS, JS, SVG, JSON, fonts and text assets, with an `index.html` at its root. A framework source tree that needs a build step must be built first; deploy the build output.
2. `list_sites`; reuse the matching site if one exists, otherwise `create_site` named after the project.
3. Copy text files with `write_file`, keeping the folder's relative paths under `/www` (for example `about/index.html` → `/www/about/index.html`). Binary files (images, fonts, PDFs) cannot be sent through this connection: if they are already hosted somewhere public, fetch them with `download_file` from that URL into the same path; otherwise tell the user which files to upload in the Ullbek builder at https://app.ullbek.com, and where they'll land. List exactly what you copied and what you couldn't.
4. `check_references` on the result, `get_preview_link`, and give the user the preview.
5. On their word, `publish_site`, then `check_live_url`. Report the live address. Repeat the copy step for later changes; only changed files need rewriting.
