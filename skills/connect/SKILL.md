---
name: connect
description: Connect the user's Ullbek account. Use when an Ullbek tool says it needs sign-in or "needs authentication" (publishing, a site they already have, anything paid), when the Ullbek tools (create_site, list_sites and the rest) are missing altogether, or when the user asks to connect, sign in or log in to Ullbek. For a new website, try create_site first: it may need no account.
---

A new website may need no connection to start: the `website` skill calls `create_site` first and builds a draft if that works. Connect when a tool says it needs the user's account (publishing, their existing sites, domains and hosting; on some setups `create_site` too), when the Ullbek tools are not there at all, or when the user asks to. Connecting takes a minute, is free, and creates the Ullbek account if they don't have one. Nothing is ever charged by connecting.

## 1. The short way: call the tool they need

If the Ullbek tools are available, call the one the user is waiting on: `publish_site` with their `site_id`, or `create_site` for a new site. If they only want to sign in, or to reach sites they already have, call `connect_account` if that tool is there, otherwise `list_sites`.

- It returns: the account is already connected. Carry on. (One exception: `list_sites` coming back empty with a note that no account is connected. Then call `connect_account`.)
- **Claude on the web, desktop or mobile app, or Cowork:** a card appears in the conversation asking them to connect. The user signs in on ullbek.com in the window it opens (Google or email, or a free account made right there) and approves. When they say "done", make the same call again yourself; don't wait for it to be retried.
- **Claude Code (terminal, VS Code or the desktop app's Code tab):** the result says the server needs sign-in or authentication. Have the user run `/mcp`, choose **plugin:ullbek:ullbek** and pick **Authenticate**; the browser opens Ullbek's sign-in page. When they say "done", make the same call again yourself.

If the user built a draft before connecting, pass the same `site_id` as before, with its key (the part after `.gk_`): the draft moves into their account on that call.

## 2. If the Ullbek tools are missing altogether

Then the plugin's connector is not active in this app. Give only the steps for the app they are using.

**Claude on the web, desktop or mobile app, or Cowork:**
1. Open **Customize → Plugins** and choose **Ullbek — AI website builder**.
2. Open its **Connectors** tab. If it lists **ullbek · Not added**, press **Connect**. (From the plugin's page in the Directory, the same button reads **Finish setup**.)
3. If a sign-in window opens on ullbek.com: continue with Google or email, or create a free account right there, then approve the connection.
4. Come back to this chat and say "done". If the Ullbek tools still don't appear, start a new chat; they load when a chat begins.

**Claude Code:** run `/mcp`, choose **plugin:ullbek:ullbek**, and pick **Authenticate** (or **Reconnect** if it shows as failed). The browser opens Ullbek's sign-in page: continue with Google or email, or create a free account, then approve.

If you can't tell which app they are in, ask in one short question.

## 3. Confirm

When they say it's done, call the tool they were waiting on. If it returns, the connection works. If it still fails, have them repeat the step and check that Ullbek shows as connected. After the first sign-in, access refreshes by itself; they won't need to do this again.

Never ask for their password or any code: the sign-in happens only on ullbek.com, in their own browser.
