# Ullbek for Claude Code and Cowork

Build, preview and publish a real website from the conversation. [Ullbek](https://www.ullbek.com) is an AI website builder: describe the site you want and Claude writes real, custom pages on Ullbek, hands you a private preview link, and publishes to a free `yourname.ullbek.site` address, or to your own domain on premium hosting.

This plugin connects Claude to your Ullbek account and teaches it how to build well.

## What's inside

| Component | What it does |
|---|---|
| **Ullbek connector** (remote MCP server) | Sites, files, previews, screenshots, publishing, custom domains, form submissions. Signs you in through your browser; nothing to configure. |
| `/ullbek:website` | Build or improve a site from what you tell Claude: preview, iterate, publish. |
| `/ullbek:deploy-folder` | Put a static site from your project folder online on Ullbek. |
| `/ullbek:connect` | Sign in and confirm the connection works. |

## Install

**On claude.ai, the desktop app or Cowork:** open **Customize → Plugins → Discover**, search for
**Ullbek** and add it. It also appears in your Claude Code sessions automatically.

**In Claude Code, straight from this repository:**

```
/plugin install ullbek --marketplace ullbek/ullbek-claude-plugin
```

Then connect your account. On claude.ai and in Cowork, open the plugin's **Connectors** tab and
connect Ullbek. In Claude Code, run `/mcp`, choose **plugin:ullbek:ullbek** and **Authenticate**, or
run `/ullbek:connect`. Your browser opens Ullbek's sign-in page: continue with Google or email, or
create a free account right there, and approve the connection.

## Try it

> Build a website for my dog-grooming business. Use everything I've told you about it, and show me a preview.

Claude creates the site, writes the pages, checks its own work, and gives you a preview link to the real site. Say the word and it publishes. Every change is a sentence.

## Good to know

- **Same account, two doors.** Everything Claude builds is in your normal Ullbek account. Open [app.ullbek.com](https://app.ullbek.com) any time to continue in the Ullbek builder.
- **Claude can never charge you.** Premium hosting and domains are paid only on a secure checkout page you open in your own browser.
- **Images.** Claude can fetch images from public URLs and use anything you upload in the Ullbek builder. Files on your disk can't be sent through the connection.
- **Rate limits** apply per account and are set for real building.

Documentation: https://www.ullbek.com/docs/use-ullbek-in-claude · Support: support@ullbek.com

## Privacy Policy

The connector talks only to Ullbek's own API at `api.ullbek.com`. It receives the arguments of the tools Claude calls (site content, file paths, addresses) and nothing else from your conversation. Ullbek stores what you build in your account; it does not collect your conversation, and does not share data with third parties beyond the service providers that run Ullbek (hosting, payments). Data retention follows your account: delete a site or your account and its files go with it. Full policy: https://www.ullbek.com/privacy · Terms: https://www.ullbek.com/terms · Contact: support@ullbek.com

## License

MIT © DeboLabs Pty Ltd
