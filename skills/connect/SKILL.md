---
name: connect
description: Connect Ullbek. Use when the Ullbek tools (create_site, list_sites and the rest) are missing altogether, when an Ullbek tool says it needs sign-in or "needs authentication" (publishing, a site they already have, anything paid), or when the user asks to connect, sign in or log in to Ullbek. For a new website, try create_site first: it may need no account.
---

There are two different things a person may need, and they are not the same step:

- **Turning the Ullbek tools on.** If the tools are not there at all, the plugin's connector has not been added in this app yet. In Claude chat that is four presses and no sign-in (section 2). After it a new website needs no account: the `website` skill calls `create_site` and builds a draft.
- **Connecting their Ullbek account.** Needed when a tool says so: publishing, their existing sites, domains and hosting (on some setups `create_site` too), or when the user asks to sign in (section 1). It takes a minute, is free, and creates the Ullbek account if they don't have one.

Nothing is ever charged by either.

## 1. Connect their account: call the tool they need

If the Ullbek tools are available, call the one the user is waiting on: `publish_site` with their `site_id`, or `create_site` for a new site. If they only want to sign in, or to reach sites they already have, call `connect_account` if that tool is there, otherwise `list_sites`.

- It returns: the account is already connected. Carry on. (One exception: `list_sites` coming back empty with a note that no account is connected. Then call `connect_account`.)
- **Claude on the web, desktop or mobile app, or Cowork:** a card appears in the conversation asking them to connect. The user signs in on ullbek.com in the window it opens (Google or email, or a free account made right there) and approves. When they say "done", make the same call again yourself; don't wait for it to be retried.
- **Claude Code (terminal, VS Code or the desktop app's Code tab):** the result says the server needs sign-in or authentication. Have the user run `/mcp`, choose **plugin:ullbek:ullbek** and pick **Authenticate**; the browser opens Ullbek's sign-in page. When they say "done", make the same call again yourself.

If the user built a draft before connecting, pass the same `site_id` as before, with its key (the part after `.gk_`): the draft moves into their account on that call.

## 2. If the Ullbek tools are missing altogether

Then the plugin's connector is not active in this app. Give only the steps for the app they are using.

**Claude on the web, desktop or mobile app, or Cowork.** Say first that it is four presses, with no sign-in and nothing to pay, then give the steps:

1. Open **Customize → Plugins** and choose **Ullbek — AI website builder**.
2. Open its **Connectors** tab. It lists **ullbek · Not added**: press **Connect**. (From the plugin's page in the Directory, the same button reads **Finish setup**.)
3. Claude opens its **Add custom connector** form with Ullbek's name and address already filled in, and its usual note about only connecting to developers you trust. Press **Continue**.
4. On the next step, **Authentication**, **No sign-in** is already chosen. Leave it and press **Add**.
5. The row now reads **Not connected**: press **Connect** once more. It connects there and then.
6. Come back to this chat and say "done". If the Ullbek tools still don't appear, start a new chat; they load when a chat begins.

Claude's screens change now and then. If theirs differ, the aim is the same: get **ullbek** to read as connected on that Connectors tab. If a sign-in window on ullbek.com opens on the way, that is fine too: they continue with Google or email, or create a free account right there, then approve.

If they ask why it says "No sign-in": a draft website needs no account, so the connection opens without one. Anything on their account (publishing, their sites, payments) asks them to sign in to Ullbek first.

**Claude Code:** run `/mcp` and choose **plugin:ullbek:ullbek**. If it shows as connected, the tools are there: carry on. If it shows as needing sign-in or failed, pick **Authenticate** (or **Reconnect**). The browser opens Ullbek's sign-in page: continue with Google or email, or create a free account, then approve.

If you can't tell which app they are in, ask in one short question.

## 3. Confirm

When they say it's done, call the tool they were waiting on: `create_site` for a new website (with the connector just added and no account it returns a draft, which is the expected result), or the tool that asked for sign-in. If it returns, the connection works. If it still fails, have them repeat the step and check that Ullbek shows as connected. After the first sign-in, access refreshes by itself; they won't need to do this again.

Never ask for their password or any code: the sign-in happens only on ullbek.com, in their own browser.
