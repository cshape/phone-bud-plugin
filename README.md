# Phone Bud plugin

Lets Grok Bot, Cursor and other agents place real phone calls with [Phone Bud](https://www.phone-bud.com): one number or a short list of businesses, in the US and Canada. Each call returns a summary, the outcome, key details and the transcript.

## What's in it

- `mcp.json`: Phone Bud's hosted MCP server, `https://www.phone-bud.com/mcp`, with your API key in the `Authorization` header.
- `skills/phone-bud/SKILL.md`: when to call, confirming with the user first, writing the request, calling a list, and limits. The same file is served at https://www.phone-bud.com/skills/phone-bud/SKILL.md.

## Setup

1. Create an API key in Phone Bud under Settings, Developer.
2. Install the plugin and set `PHONE_BUD_API_KEY` to that key.

Without the plugin, paste this into a Grok Bot chat:

```
Add a custom MCP server named phone-bud.
URL: https://www.phone-bud.com/mcp
Header: Authorization: Bearer <API key>
Ask me for the key in a secure form.

Then install the skill at
phone-bud.com/skills/phone-bud/SKILL.md
and check the connection with list_agents.
```

## Tools

`make_call`, `get_call`, `start_campaign`, `get_campaign`, `list_campaigns`, `list_contacts`, `list_agents`, `create_agent`, `update_agent`.

## Limits

- US and Canada numbers only. Calls end at 30 minutes, including hold time.
- The agent says it's an AI if asked, and never claims to be a person or the user.
- It can't transfer the call to the user, receive calls, or pay for anything.
- Call only people and businesses you have a reason to contact. See the [acceptable use policy](https://www.phone-bud.com/acceptable-use) and [privacy policy](https://www.phone-bud.com/privacy).

## Pricing

The first call is free, up to 5 minutes. Then CA$8 for 15 minutes, CA$20 for 60 minutes or CA$80 for 300 minutes, billed by the minute (rounded up). See [pricing](https://www.phone-bud.com/#pricing).

Questions: support@phone-bud.com
