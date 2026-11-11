---
name: connect
description: Connect the user's Ullbek account so the Ullbek tools work. Use right after the plugin is installed, whenever the user wants a website but the Ullbek tools (list_sites, create_site and the rest) are missing or report "needs authentication", or when the user asks to connect, sign in or log in to Ullbek.
---

Installing the plugin does not connect it. Until the user connects their Ullbek account, the Ullbek tools are missing or answer "needs authentication". Connecting takes a minute, is free, and creates the Ullbek account if they don't have one. Nothing is ever charged by connecting.

## 1. Check first

If an Ullbek tool such as `list_sites` is available, call it. If it returns (even an empty list), the account is already connected: say so, name their sites if they have any, and move on to what they want to build. Only if the tools are missing or the call fails with an authentication error, walk them through step 2.

## 2. Give the steps for where they are

Give only the steps for the app they are using. Keep it short and friendly.

**Claude on the web, desktop or mobile app, or Cowork:**
1. Open **Customize → Plugins** and choose **Ullbek — AI website builder**.
2. Open its **Connectors** tab. It lists **ullbek · Not added**: press **Connect**. (From the plugin's page in the Directory, the same button reads **Finish setup**.)
3. A sign-in window opens on ullbek.com: continue with Google or email, or create a free account right there, then approve the connection.
4. Come back to this chat and say "done". If the Ullbek tools still don't appear, start a new chat; they load when a chat begins.

**Claude Code (terminal, VS Code or the desktop app's Code tab):**
1. Run `/mcp`, choose **plugin:ullbek:ullbek**, and pick **Authenticate**.
2. The browser opens Ullbek's sign-in page: continue with Google or email, or create a free account, then approve the connection.
3. Come back and say "done".

If you can't tell which app they are in, ask in one short question.

## 3. Confirm

When they say it's done, call `list_sites`. If it returns, the connection works: tell them how many sites they have, by name, and ask what they'd like to build. If it still fails, have them repeat step 2 and check that Ullbek shows as connected. After the first sign-in, access refreshes by itself; they won't need to do this again.

Never ask for their password or any code: the sign-in happens only on ullbek.com, in their own browser.
