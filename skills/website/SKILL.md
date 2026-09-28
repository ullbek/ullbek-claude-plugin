---
name: website
description: Build, preview and publish a real website on Ullbek from what the user tells you. Use when the user wants a website, landing page, portfolio or site for a business, event or project, or wants to change or publish a site they already have on Ullbek.
argument-hint: [what the site is for]
---

You are building a real, custom website on Ullbek: plain HTML, CSS and vanilla JavaScript files, served exactly as written, hosted by Ullbek. No framework, no build step. The Ullbek MCP server's own instructions describe every tool; this skill is the choreography for doing it well from Claude Code.

## Before you write anything

- Orient: `list_sites`. To improve an existing site, `get_site_overview` first. For a new site, `create_site` with a short real name (the business, not "my website").
- Ask only what you can't infer. If the user has told you about the business anywhere in this session or project, use it: name, offer, audience, tone, prices, opening hours, contact details. Real content beats placeholders every time. One short question about what's missing is fine; a questionnaire is not.
- Images: Ullbek can pull an image from any public URL with `download_file`, and the user can upload their own photos and logo in the Ullbek builder at https://app.ullbek.com, where they appear under `/uploads`. Files on the user's local disk cannot be sent through this connection, so say so and offer those two routes. Never leave a broken image.

## Build

1. Write `/www/index.html` first, with the CSS in `/www/css/site.css` and any JS in `/www/js/site.js`. Semantic HTML, a real navigation, a clear headline that says what the business does and for whom, and a contact route. Mobile first.
2. `validate` every HTML, CSS and JS file you write; `check_references` before a preview so no link or asset is dangling.
3. `get_preview_link`, then `take_screenshot` (desktop and a phone size) and look at the result critically: hierarchy, spacing, contrast, whether it reads like a site made for this business. Fix what you see before showing the user.
4. Give the user the preview link and ask for changes. Iterate with `edit_file`; take a fresh screenshot after each meaningful change.

## Publish

- `check_slug_available` if the user cares about the address, `set_slug` to change it, then `publish_site`. A content-moderation review runs at publish; if a site is blocked, explain the reason the result gives. Confirm with `check_live_url` and hand over the live address.
- Custom domains need premium hosting. `subscribe_premium` returns a checkout URL: show it as a link for the user to open in their own browser; you can never charge them. Then `get_subscription_status`, `set_custom_domain` (it returns the DNS records), and walk the wiring with `verify_custom_domain`, `check_domain_propagation` and `get_certificate_status` until `check_live_url` passes on the domain.

## Judgement

- The bar is "would this impress the owner", not "does it render". If a first draft looks generic, improve it before asking.
- Every change the user asks for in words is one `edit_file`; don't rewrite whole pages for small edits.
- Ullbek is the user's account: everything you build is also in their builder at https://app.ullbek.com, where they can keep editing.
