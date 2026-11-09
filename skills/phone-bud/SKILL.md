---
name: phone-bud
description: Place real phone calls to US and Canada numbers through Phone Bud's MCP server, one call or a short list of businesses, and report back the answer. Use when the user asks you to call a business or person, check stock, prices, hours or availability by phone, book, move or cancel an appointment, get through a phone menu or wait on hold, or ask several places the same question.
---

# Phone calls with Phone Bud

Phone Bud's MCP server (`https://www.phone-bud.com/mcp`) places outbound calls with an AI voice agent. Each call returns a summary, the outcome, key details and the transcript.

## Before every call

- Confirm the number, who it belongs to, and what to ask or say with the user. A call can't be taken back once it connects, and it uses the user's Phone Bud minutes.
- Call only people and businesses the user has a reason to contact. No marketing calls or cold outreach.
- Numbers must be in the US or Canada, in E.164 format: `+15551234567`.
- Leave out card numbers and passwords.

## One call: `make_call`

Pass `to_phone`, or `contact_name` for a saved contact. Put the request in `system_prompt`:

- Who the agent calls for, and that it is their AI assistant.
- The one thing to find out or say.
- Anything a phone menu may ask for, such as an order or account number.
- For bookings: the times that work, and whether to book or only ask what's open.
- The user's own number, if they want a call back.
- "If anyone asks, say you're an AI. Never claim to be a person or the user."

`system_prompt` replaces the agent's default instructions, so include that last line every time.

`make_call` returns when the call ends. It waits up to `max_wait_seconds` (600 by default, up to 1800); if the call is still going then, it hangs up and returns what it has. Raise it for long holds.

```
make_call({
  to_phone: "+15555550100",
  system_prompt: "You are Sam Lee's AI assistant, calling a hardware store. If anyone asks, say you're an AI. Never claim to be a person or Sam. Ask if they have the 20-volt drill battery in stock today, and the price. Don't buy anything."
})
```

## Several places: `start_campaign`

Use it to ask several numbers the same thing, such as prices from five caterers.

- `name`, `goal` (the overall aim) and `ask_script` (what to ask on every call).
- `entries`: one per number, with `to_phone` and a `display_name`.
- `output_fields`: what to pull out of each call, such as price or availability.
- Calls go one at a time by default. `mode: "parallel"` with `concurrency` (up to 5) runs several at once.

The campaign runs in the background. Check `get_campaign` for progress and each call's results, then give the user a short comparison.

## Reporting back

Lead with the answer from the notes. Add key details such as names, times and prices. Quote the transcript only if the user asks, or if the notes and the transcript disagree.

## Limits

- Calls end at 30 minutes, including hold time. The first call on an account is free, up to 5 minutes.
- The agent can't transfer the call to the user, receive calls, or pay for anything.
- Calls come from a shared Phone Bud number. If the user has verified their own number in Phone Bud, pass it as `from_phone`.
- If a tool says the account is out of minutes, send the user to https://www.phone-bud.com/app/settings/billing.
