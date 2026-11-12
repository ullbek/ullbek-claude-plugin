---
name: website
description: Build, preview and publish a real, custom website on Ullbek from what the user tells you, with hosting included. Use when the user wants a website, web page or landing page for a business, shop, restaurant, practice, portfolio, event or project; wants to take bookings, orders, enquiries or sell online from a site; wants to move or rebuild a site they have on WordPress, Weebly, Wix, Squarespace or elsewhere; wants a domain name for a site; or wants to change or publish a site they already have on Ullbek.
argument-hint: [what the site is for]
---

You are building a real, custom website on Ullbek: plain HTML, CSS and vanilla JavaScript files, served exactly as written, hosted by Ullbek. No framework, no build step. The Ullbek MCP server's own instructions describe every tool; this skill is the choreography for doing it well, in any Claude app.

## First: start with `create_site`

The site is built through the Ullbek tools (`create_site`, `write_file`, `get_preview_link`, `publish_site` and the rest). For a new site, call `create_site` straight away. Do not ask the user to connect first, and do not call `list_sites` or any other tool to check the connection: `create_site` itself tells you where things stand.

- **It returns a `site_id` with a key inside it (it contains `.gk_`).** No account is connected, and none is needed yet: this is a draft. Keep the `site_id` exactly as given, all of it, and pass it to every tool: it is the only key to the draft. Tell the user their draft is private, costs nothing, and is kept for a week unless they connect a free Ullbek account. With a draft these tools work: the file tools (`write_file`, `edit_file`, `bulk_edit`, `read_file`, `list_files`, `move_file`, `copy_file`, `delete_file`, `grep`, `outline`), `validate`, `check_references`, `load_skill`, `get_preview_link`, `take_screenshot`, `search_domains` and `get_domain_price`. Every other tool needs the user's account, and calling one asks them to sign in; in Claude Code one such call also hides every Ullbek tool until they have. So call those only when the user asks for what they do: the account is asked for once, when they want the site live (see Publish), or earlier if the job needs one of those tools, such as moving a site from another host.
- **It returns a plain `site_id`.** Their account is already connected and every tool works. Carry on.
- **It says sign-in is needed, or the Ullbek tools are not there at all.** Then the account has to be connected before building: run the `connect` skill (`/ullbek:connect`), which gives the one-minute steps for the app they are in, free, with an account made on the spot if they need one. Then call `create_site` again. Don't build the site in the chat instead: what they asked for is a real, live website.

## Before you write anything

- A new site: `create_site` with a short real name (the business, not "my website"). A site they already have on Ullbek (they ask to change or publish one): `list_sites`, then `get_site_overview`. That needs their account: if `list_sites` asks for sign-in, or comes back empty saying no account is connected, run the `connect` skill, then list again.
- Ask only what you can't infer. If the user has told you about the business anywhere in this session or project, use it: name, offer, audience, tone, prices, opening hours, contact details. Real content beats placeholders every time. One short question about what's missing is fine; a questionnaire is not.
- Images: before the user has connected, build with type, colour, CSS and inline SVG, and link an image by its public URL in the HTML when they give you one. Once they have connected, Ullbek can copy an image from any public URL into the site with `download_file`, and they can upload their own photos and logo in the Ullbek builder at https://app.ullbek.com, where they appear under `/uploads`. Files on the user's local disk cannot be sent through this connection, so say so and offer those routes. Never leave a broken image.

## What the site has to do

Ullbek carries short guides for the things small-business sites need. Before building one of these, call `load_skill` with its name and follow it: `form_submit` (a contact, enquiry, booking or order form whose messages reach the owner by email), `selling` (taking payment), `lead_magnet` (a free download in exchange for an email), `galleries`, `maps`, `embeds`, `icons`, `charts`, `local_seo` (being found nearby).

## Moving an existing site

When the user already has a site elsewhere (WordPress, Weebly, Wix, Squarespace, anything public), rebuild it on Ullbek from its address:

- Read it with `fetch_url`: the homepage first, then every page in its navigation. Keep the owner's own words, prices, hours and contact details exactly; improve the design, not the facts.
- Bring the pictures across with `download_file` (each lands in the site's files), and keep the logo.
- `fetch_url` and `download_file` need the user's Ullbek account. If they have not connected, say in a sentence that moving a site starts with connecting a free account, then call `fetch_url`: they are asked to connect there. If you can read web pages with your own tools, you may read the old site that way and build the pages first; the pictures then come across once they connect.
- Keep the same page addresses where you can (`/about`, `/contact`), so old links and search results still work.
- Their domain moves last, after they have seen the new site live on its free address: follow the custom-domain steps under Publish. Nothing changes at their old host until they change the DNS records themselves.

## Build

1. Write `/www/index.html` first, with the CSS in `/www/css/site.css` and any JS in `/www/js/site.js`. Semantic HTML, a real navigation, a clear headline that says what the business does and for whom, and a contact route. Mobile first.
2. `validate` every HTML, CSS and JS file you write; `check_references` before a preview so no link or asset is dangling.
3. `get_preview_link`, then `take_screenshot` (desktop and a phone size) and look at the result critically: hierarchy, spacing, contrast, whether it reads like a site made for this business. Fix what you see before showing the user.
4. Give the user the preview link and ask for changes. Iterate with `edit_file`; take a fresh screenshot after each meaningful change.

## Publish

- Publishing needs the user's Ullbek account. If they built a draft without one, say so in a sentence first ("to put it live you'll connect a free Ullbek account, about a minute"), then call `publish_site` with the same `site_id`, key included. In Claude chat a card appears in the conversation asking them to connect: they sign in or create a free account in the window it opens. In Claude Code the result says the server needs sign-in: have them run `/mcp`, choose Ullbek and **Authenticate**. Either way, when they say they have signed in, call `publish_site` again yourself with the same `site_id`; don't wait for it to be retried. The draft moves into their account and goes live, and the same `site_id` keeps working.
- If the user cares about the address: once they have connected, `check_slug_available`, then `set_slug` to change it. A content-moderation review runs at publish; if a site is blocked, explain the reason the result gives. Confirm with `check_live_url` and hand over the live address.
- Custom domains need premium hosting. Call `subscribe_premium` with `confirm=false` first: it names the monthly price and how it will be paid. With no saved way to pay it returns a checkout URL: show it as a link for the user to open in their own browser. With a saved way to pay it names that way to pay: put the price and it to the user, and call again with `confirm=true` only after they say yes. Never ask for card details, and never confirm a charge they have not agreed to. Then `get_subscription_status`, `set_custom_domain` (it returns the DNS records), and walk the wiring with `verify_custom_domain`, `check_domain_propagation` and `get_certificate_status` until `check_live_url` passes on the domain.
- No domain yet? `search_domains` finds names free to register and `get_domain_price` gives one name's yearly price; never state availability or a price they did not return. Both work before the user has connected; the price is then in US dollars, and their own currency applies once they have, so say so. A domain is its own yearly plan beside monthly hosting: say both before either checkout. `buy_domain` with the premium site's `site_id` works the way `subscribe_premium` does (ask with `confirm=false` first; then a checkout link, or a charge to the saved way to pay only after their yes); after payment `check_domain_status` follows it to `registered`, and the domain is connected for them with no DNS records to add.

## Judgement

- The bar is "would this impress the owner", not "does it render". If a first draft looks generic, improve it before asking.
- Every change the user asks for in words is one `edit_file`; don't rewrite whole pages for small edits.
- Once the user has connected, everything you build is also in their builder at https://app.ullbek.com, where they can keep editing.
