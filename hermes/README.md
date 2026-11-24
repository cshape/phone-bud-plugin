# Phone Bud for Hermes Agent

Lets Hermes place real phone calls with [Phone Bud](https://www.phone-bud.com): one number or a short list of businesses, in the US and Canada. Each call returns a summary, the outcome, key details and the transcript.

A portable Agent Plugins v1 package: `plugin.json`, `mcp.json` (Phone Bud's hosted MCP server, `https://www.phone-bud.com/mcp`) and one skill, `skills/phone-bud/SKILL.md`.

## Install

```
hermes plugins install phone-bud
hermes plugins enable phone-bud
hermes mcp add phone-bud --url https://www.phone-bud.com/mcp --auth oauth
```

The last command opens Phone Bud so you can sign in, or create an account, and allow Hermes. On a server with no browser, run `hermes mcp login phone-bud` and paste the address you land on back into the terminal. Check it with `hermes mcp test phone-bud`.

Then ask Hermes to call someone. The skill has it confirm the number and the request with you before every call.

## Tools

Read: `list_agents`, `list_contacts`, `list_context`, `get_call`, `get_campaign`, `list_campaigns`.

Write: `make_call` and `start_campaign` place real calls; `create_agent` and `update_agent` change your Phone Bud agents. The package marks the server untrusted, so Hermes asks you before each of these.

## What to know before installing

- No local code. Every tool call goes to Phone Bud's server at www.phone-bud.com, signed in as you. The first sign-in creates a Phone Bud account if you don't have one.
- `make_call` and `start_campaign` dial real phone numbers and use your Phone Bud minutes.
- The request you write, the phone number, and the call's transcript and notes pass through the Hermes session, so they reach your model provider. Phone Bud stores calls, recordings and transcripts in your account; see the [privacy policy](https://www.phone-bud.com/privacy).
- Hermes stores and refreshes the sign-in tokens. The tool list comes from Phone Bud's server at run time.
- `hermes mcp add` replaces the package's server entry, trust setting included. Add `trust: untrusted` to the `phone-bud` entry in `~/.hermes/config.yaml` to keep the prompt before each call.

## Limits

- US and Canada numbers only. Calls end at 30 minutes, including hold time.
- The agent says it's an AI if asked, and never claims to be a person or you.
- It can't transfer the call to you, receive calls, or pay for anything.
- Call only people and businesses you have a reason to contact. See the [terms of service](https://www.phone-bud.com/terms) and [acceptable use policy](https://www.phone-bud.com/acceptable-use).

## Pricing

The first call is free, up to 5 minutes. Then CA$8 for 15 minutes, CA$20 for 60 minutes or CA$80 for 300 minutes, billed by the minute (rounded up), with no subscription.

Questions: support@phone-bud.com
