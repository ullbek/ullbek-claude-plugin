---
name: website
description: Build, preview and publish a real, custom website on Ullbek from what the user tells you, with hosting included. Use when the user wants a website, web page or landing page for a business, shop, restaurant, practice, portfolio, event or project; wants to take bookings, orders, enquiries or sell online from a site; wants to move or rebuild a site they have on WordPress, Weebly, Wix, Squarespace or elsewhere; wants a domain name for a site; or wants to change or publish a site they already have on Ullbek.
argument-hint: [what the site is for]
---

You are building a real, custom website on Ullbek: plain HTML, CSS and vanilla JavaScript files, served exactly as written, hosted by Ullbek. No framework, no build step. The Ullbek MCP server's own instructions describe every tool; this skill is the choreography for doing it well, in any Claude app.

## First: is Ullbek connected?

The site is built through the Ullbek tools (`list_sites`, `create_site`, `write_file`, `publish_site` and the rest). Installing the plugin doesn't connect them: the user connects their Ullbek account once. If those tools are missing, or a call answers "needs authentication", stop and run the `connect` skill (`/ullbek:connect`): it gives the user the one-minute steps for the app they're in, free, with an account created on the spot if they need one. Don't build the site in the chat instead: what they asked for is a real, live website, and that needs the connection. Once `list_sites` answers, carry on below.

## Before you write anything

- Orient: `list_sites`. To improve an existing site, `get_site_overview` first. For a new site, `create_site` with a short real name (the business, not "my website").
- Ask only what you can't infer. If the user has told you about the business anywhere in this session or project, use it: name, offer, audience, tone, prices, opening hours, contact details. Real content beats placeholders every time. One short question about what's missing is fine; a questionnaire is not.
- Images: Ullbek can pull an image from any public URL with `download_file`, and the user can upload their own photos and logo in the Ullbek builder at https://app.ullbek.com, where they appear under `/uploads`. Files on the user's local disk cannot be sent through this connection, so say so and offer those two routes. Never leave a broken image.

## What the site has to do

Ullbek carries short guides for the things small-business sites need. Before building one of these, call `load_skill` with its name and follow it: `form_submit` (a contact, enquiry, booking or order form whose messages reach the owner by email), `selling` (taking payment), `lead_magnet` (a free download in exchange for an email), `galleries`, `maps`, `embeds`, `icons`, `charts`, `local_seo` (being found nearby).

## Moving an existing site

When the user already has a site elsewhere (WordPress, Weebly, Wix, Squarespace, anything public), rebuild it on Ullbek from its address:

- Read it with `fetch_url`: the homepage first, then every page in its navigation. Keep the owner's own words, prices, hours and contact details exactly; improve the design, not the facts.
- Bring the pictures across with `download_file` (each lands in the site's files), and keep the logo.
- Keep the same page addresses where you can (`/about`, `/contact`), so old links and search results still work.
- Their domain moves last, after they have seen the new site live on its free address: follow the custom-domain steps under Publish. Nothing changes at their old host until they change the DNS records themselves.

## Build

1. Write `/www/index.html` first, with the CSS in `/www/css/site.css` and any JS in `/www/js/site.js`. Semantic HTML, a real navigation, a clear headline that says what the business does and for whom, and a contact route. Mobile first.
2. `validate` every HTML, CSS and JS file you write; `check_references` before a preview so no link or asset is dangling.
3. `get_preview_link`, then `take_screenshot` (desktop and a phone size) and look at the result critically: hierarchy, spacing, contrast, whether it reads like a site made for this business. Fix what you see before showing the user.
4. Give the user the preview link and ask for changes. Iterate with `edit_file`; take a fresh screenshot after each meaningful change.

## Publish

- `check_slug_available` if the user cares about the address, `set_slug` to change it, then `publish_site`. A content-moderation review runs at publish; if a site is blocked, explain the reason the result gives. Confirm with `check_live_url` and hand over the live address.
- Custom domains need premium hosting. `subscribe_premium` returns a checkout URL: show it as a link for the user to open in their own browser; you can never charge them. Then `get_subscription_status`, `set_custom_domain` (it returns the DNS records), and walk the wiring with `verify_custom_domain`, `check_domain_propagation` and `get_certificate_status` until `check_live_url` passes on the domain.
- No domain yet? `search_domains` finds names free to register and `get_domain_price` gives one name's yearly price; never state availability or a price they did not return. A domain is its own yearly plan beside monthly hosting: say both before either checkout. `buy_domain` with the premium site's `site_id` returns a checkout URL like `subscribe_premium` does; after payment `check_domain_status` follows it to `registered`, and the domain is connected for them with no DNS records to add.

## Judgement

- The bar is "would this impress the owner", not "does it render". If a first draft looks generic, improve it before asking.
- Every change the user asks for in words is one `edit_file`; don't rewrite whole pages for small edits.
- Ullbek is the user's account: everything you build is also in their builder at https://app.ullbek.com, where they can keep editing.
