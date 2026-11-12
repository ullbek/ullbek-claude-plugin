# Ullbek for Claude Code and Cowork

Build, preview and publish a real website from the conversation. [Ullbek](https://www.ullbek.com) is an AI website builder: describe the site you want and Claude writes real, custom pages on Ullbek, hands you a private preview link, and publishes to a free `yourname.ullbek.site` address, or to your own domain on premium hosting.

This plugin connects Claude to your Ullbek account and teaches it how to build well.

## What's inside

| Component | What it does |
|---|---|
| **Ullbek connector** (remote MCP server) | Sites, files, previews, screenshots, publishing, custom domains (one you already own, or a new one found and bought from the conversation), form submissions. Signs you in through your browser when you publish; nothing to configure. |
| `/ullbek:website` | Build or improve a site from what you tell Claude: preview, iterate, publish. |
| `/ullbek:deploy-folder` | Put a static site from your project folder online on Ullbek. |
| `/ullbek:connect` | Turn the connection on, or sign in, and confirm it works. |

## Install

**On claude.ai, the desktop app or Cowork:** open **Customize → Plugins → Discover**, search for
**Ullbek** and add it. It also appears in your Claude Code sessions automatically.

**In Claude Code, straight from this repository:**

```
/plugin install ullbek --marketplace ullbek/ullbek-claude-plugin
```

**On claude.ai, the desktop app and Cowork, turn the connection on first.** It is four presses and no
sign-in: open **Customize → Plugins → Ullbek — AI website builder → Connectors** and press **Connect**
next to **ullbek** (the Directory page calls it **Finish setup**); Claude opens its **Add custom
connector** form with Ullbek's details filled in, so press **Continue**; on the **Authentication** step
leave **No sign-in** chosen and press **Add**; then press **Connect** once more. In Claude Code the
tools are usually there as soon as the plugin is installed; if they aren't, run `/mcp`, choose
**plugin:ullbek:ullbek** and **Authenticate**. Or ask Claude to "connect Ullbek" and it walks you
through it (`/ullbek:connect`).

**Then just ask for a website.** Claude builds a private draft on Ullbek with no account. You connect a
free Ullbek account when you want it published: Claude shows a sign-in card in the conversation (in
Claude Code it asks you to run `/mcp`), and your browser opens Ullbek's sign-in page, where you
continue with Google or email, or create a free account right there, and approve the connection. A
draft nobody connects is kept for a week.

## Try it

> Build a website for my dog-grooming business. Use everything I've told you about it, and show me a preview.

Claude creates the site, writes the pages, checks its own work, and gives you a preview link to the real site. Say the word and it publishes. Every change is a sentence.

## Good to know

- **Same account, two doors.** Everything Claude builds is in your normal Ullbek account. Open [app.ullbek.com](https://app.ullbek.com) any time to continue in the Ullbek builder.
- **Nothing is charged without your yes.** Claude never sees or asks for your card details. Premium hosting, domains and credits are paid on a secure checkout page you open in your own browser; if you have saved a way to pay in your Ullbek account, Claude names the price and that way to pay, and it is charged only after you say yes.
- **Images.** Claude can fetch images from public URLs and use anything you upload in the Ullbek builder. Files on your disk can't be sent through the connection.
- **Rate limits** apply per account and are set for real building.

Documentation: https://www.ullbek.com/docs/use-ullbek-in-claude · Support: support@ullbek.com

## Privacy Policy

The connector talks only to Ullbek's own API at `api.ullbek.com`. It receives the arguments of the tools Claude calls (site content, file paths, addresses) and nothing else from your conversation. Ullbek stores what you build in your account; it does not collect your conversation, and does not share data with third parties beyond the service providers that run Ullbek (hosting, payments). Data retention follows your account: delete a site or your account and its files go with it. Full policy: https://www.ullbek.com/privacy · Terms: https://www.ullbek.com/terms · Contact: support@ullbek.com

## License

MIT © DeboLabs Pty Ltd
