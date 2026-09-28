---
name: connect
description: Sign in to Ullbek and confirm the connection works. Use when Ullbek tools report "needs authentication", when the user asks to connect or log in to Ullbek, or right after installing the plugin.
disable-model-invocation: true
---

Connect this session to the user's Ullbek account.

1. Tell the user to run `/mcp`, pick **plugin:ullbek:ullbek**, and choose **Authenticate**. Their browser opens Ullbek's sign-in page: they continue with Google or email, or create a free account right there, then approve the connection. Nothing is charged; connecting is free.
2. Once they say it's done, call `list_sites`. If it returns (even an empty list), the connection works. Report how many sites they have, by name.
3. If it still fails with an authentication error, have them run `/mcp` again and check the server shows as connected. Tokens refresh automatically after the first sign-in.

Then ask what they'd like to build, or point them at `/ullbek:website` for a new site.
