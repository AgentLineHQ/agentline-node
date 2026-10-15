# Reference
## Voice
<details><summary><code>client.voice.<a href="/src/api/resources/voice/client/Client.ts">get</a>() -> unknown</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Get the current account-level default voice for AI phone agents.

Returns which voice is used for all AI agents under this account
unless overridden at the agent level or per-call.

Returns account_id, default_voice_id (the stored preset name or UUID,
null when none is set) and resolved_voice_id (the voice UUID calls will
actually use).
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.voice.get();

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**requestOptions:** `VoiceClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.voice.<a href="/src/api/resources/voice/client/Client.ts">reset</a>() -> unknown</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Reset account voice to the system default.

Removes the account-level voice override so all AI agents fall back
to the system default voice during phone calls (unless they have
their own voice_id configured), starting with their next call. The
previous value is not kept: read it with get_account_voice first if it
may be needed again.

Returns account_id, default_voice_id null, resolved_voice_id (the
system default) and a message.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.voice.reset();

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**requestOptions:** `VoiceClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.voice.<a href="/src/api/resources/voice/client/Client.ts">set</a>({ ...params }) -> unknown</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Set the account-level default voice for AI phone agents.

This becomes the default voice for ALL AI agents under this account,
controlling how they sound on phone calls. Individual agents or
specific calls can still override this setting.

Voice resolution priority:
  1. Per-call voice_id (make_outbound_call)
  2. Agent voice_id (update_agent)
  3. Account default (this tool)
  4. System default (Supportive Male)

Returns account_id, default_voice_id (as sent) and resolved_voice_id
(the UUID it resolves to). An unknown preset or malformed UUID returns
HTTP 400.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.voice.set({
    voice_id: "voice_id"
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `AgentlineApi.VoiceSettingUpdate` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `VoiceClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.voice.<a href="/src/api/resources/voice/client/Client.ts">list</a>() -> unknown</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

List all available voice presets for AI phone agents.

Returns named TTS (text-to-speech) voice presets that can be used
when configuring AI agents or making phone calls. Each voice defines
how your AI agent sounds on the phone.

Returns {"voices": [...], "default_voice_id", "usage_hint"}: each voice
has preset_name (e.g. "female-1"), voice_id (UUID), name and description.
Pass either preset_name or voice_id as voice_id to create_agent,
update_agent, make_outbound_call or set_account_voice.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.voice.list();

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**requestOptions:** `VoiceClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## Agents
<details><summary><code>client.agents.<a href="/src/api/resources/agents/client/Client.ts">list</a>() -> unknown</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

List all AI voice agents configured on your account.

Returns every AI phone agent you've created, including their
system prompts, voice settings, and associated phone numbers.
Useful for checking which agents are ready to make or receive calls.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.agents.list();

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**requestOptions:** `AgentsClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.agents.<a href="/src/api/resources/agents/client/Client.ts">create</a>({ ...params }) -> AgentlineApi.AgentOut</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Create a new AI voice agent for telephony.

Adds an agent to the account with its own system prompt, voice and
greeting. Creating an agent is free; it cannot call until it has a
number, so call buy_phone_number next with the returned id as agent_id.

Returns the new agent, including its id (agt_...). A voice_id that is
not a preset from list_available_voices or a voice UUID is rejected, as
is a transfer_number that differs from owner_phone (HTTP 400).
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.agents.create({
    name: "name"
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `AgentlineApi.AgentCreate` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `AgentsClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.agents.<a href="/src/api/resources/agents/client/Client.ts">get</a>({ ...params }) -> unknown</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Get details of a specific AI voice agent.

Returns the agent's full configuration including system prompt,
voice settings, greeting, and transfer number.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.agents.get({
    agent_id: "agent_id"
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `AgentlineApi.GetAgentsRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `AgentsClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.agents.<a href="/src/api/resources/agents/client/Client.ts">delete</a>({ ...params }) -> unknown</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Delete an AI voice agent.

Permanently removes the agent with its calls and transcripts, messages,
conversations, contacts and webhook. Cannot be undone. Phone numbers
assigned to it are detached, not released: they stay active
on your account and can be reassigned to another agent.

Returns {"deleted": true, "agent_id": ...}.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.agents.delete({
    agent_id: "agent_id"
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `AgentlineApi.DeleteAgentsRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `AgentsClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.agents.<a href="/src/api/resources/agents/client/Client.ts">update</a>({ ...params }) -> unknown</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Update an AI voice agent's configuration.

Overwrites the fields you send; omitted fields keep their values and the
old values are not kept. Changes apply to the next inbound or outbound
call the agent handles; calls already in progress are unaffected.

Returns the full updated agent. Sending no fields, an unknown voice_id or
a transfer_number other than owner_phone returns HTTP 400.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.agents.update({
    agent_id: "agent_id"
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `AgentlineApi.AgentUpdate` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `AgentsClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## Billing
<details><summary><code>client.billing.<a href="/src/api/resources/billing/client/Client.ts">getBalance</a>() -> unknown</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Get your AI telephony account balance and rate card.

Returns the current balance, currency, billing rates for calls,
phone numbers, and inbound SMS, plus what the balance can cover.
Use this to check affordability before paid telephony operations.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.billing.getBalance();

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**requestOptions:** `BillingClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.billing.<a href="/src/api/resources/billing/client/Client.ts">getExpenditure</a>({ ...params }) -> unknown</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Get a detailed expenditure breakdown for AI telephony usage.

Shows total spend split by category (voice calls, phone number
provisioning, top-ups, refunds) with counts and averages.
Useful for tracking how much your AI agents are spending on
phone calls and phone numbers.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.billing.getExpenditure();

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `AgentlineApi.GetExpenditureBillingRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `BillingClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.billing.<a href="/src/api/resources/billing/client/Client.ts">listCallCharges</a>({ ...params }) -> unknown</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

List individual call charges from AI agent phone calls.

Each entry includes the voice call duration, cost, direction
(inbound/outbound), phone numbers involved, and timestamp.
Shows exactly how much each AI agent call cost.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.billing.listCallCharges();

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `AgentlineApi.ListCallChargesBillingRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `BillingClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.billing.<a href="/src/api/resources/billing/client/Client.ts">listNumberCharges</a>({ ...params }) -> unknown</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

List phone number provisioning charges.

Shows the cost of each phone number bought for your AI agents,
including the number, country, and current status.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.billing.listNumberCharges();

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `AgentlineApi.ListNumberChargesBillingRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `BillingClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.billing.<a href="/src/api/resources/billing/client/Client.ts">getSummary</a>({ ...params }) -> unknown</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Month-over-month spending summary.

Returns total debits grouped by month for trend analysis.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.billing.getSummary();

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `AgentlineApi.GetSummaryBillingRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `BillingClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## Calls
<details><summary><code>client.calls.<a href="/src/api/resources/calls/client/Client.ts">list</a>({ ...params }) -> unknown</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

List voice calls made by your AI agents.

Returns call history with optional filters by agent or status.
Each entry includes direction (inbound/outbound), duration,
phone numbers, and current status.

Filters:
  - agent_id: only calls for a specific AI agent
  - status: "initiated", "in-progress", "completed", or "failed"
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.calls.list();

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `AgentlineApi.ListCallsRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `CallsClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.calls.<a href="/src/api/resources/calls/client/Client.ts">create</a>({ ...params }) -> unknown</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Make an outbound phone call from your AI agent.

Dials a real person or business from the agent's number. The agent holds
the whole conversation on its own with its system prompt, voice and
greeting (or this call's overrides). The call reaches a third party and
is billed to the account at $0.10 per minute, first minute charged in
full, so confirm with the user first. Not idempotent: every successful
call dials again.

Prerequisites: an agent with an active number from buy_phone_number
(HTTP 400 otherwise) and at least $0.50 of balance (HTTP 402 otherwise).

Returns right after dialing with the call id (call_...), agent_id,
from_number, to_number, direction, status and started_at; the call runs
on its own. Check get_call_details for progress and call
get_call_transcript once status is completed.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.calls.create({
    agent_id: "agent_id",
    to_number: "to_number"
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `AgentlineApi.CallRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `CallsClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.calls.<a href="/src/api/resources/calls/client/Client.ts">get</a>({ ...params }) -> unknown</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Get full details of a specific voice call.

Returns the call's metadata including direction, phone numbers,
status, duration, AI agent configuration used, and the full
conversation transcript between the AI agent and the caller.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.calls.get({
    call_id: "call_id"
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `AgentlineApi.GetCallsRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `CallsClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.calls.<a href="/src/api/resources/calls/client/Client.ts">pushContext</a>({ ...params }) -> unknown</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Push context into a LIVE relay-mode call (mid-call context injection).

A call.utterance or call.task.open event means a live caller is waiting.
Do the work, then push the facts; they reach the call immediately. The
hosted voice phrases them in its own words (it never reads your text
aloud) and keeps them for the rest of the call.

Body fields (send as arguments next to call_id):
  - context: the facts, e.g. "John emailed yesterday about an invoice."
    Aliases: summary, answer, response, reply, text, result, message.
  - disposition: partial (one real fact so far; spoken now, task stays
    open), progress (a note, not spoken, task stays open), done (default),
    failed or noop (settle the task; noop needs no context), or facts
    (call facts at any time without turn_id, e.g. a call-start briefing).
  - turn_id, push_token: as the parameters below.

Auth: pass the event's push_token as token. An AgentLine API key as
Authorization: Bearer also works; OAuth tokens do not.

Returns {"delivered": true, "status", "call_id", "turn_id"}; status
"duplicate" means an identical retry was already accepted. HTTP 409: the
turn is stale or cancelled, so do not reuse this context. HTTP 410: the
call ended; stop working on this request.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.calls.pushContext({
    call_id: "call_id",
    body: {
        "key": "value"
    }
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `AgentlineApi.PushContextCallsRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `CallsClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.calls.<a href="/src/api/resources/calls/client/Client.ts">hangup</a>({ ...params }) -> unknown</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Hang up an active phone call.

Programmatically terminates an in-progress voice call. Use this
when the AI agent needs to end the conversation, or to force-stop
a call that is no longer needed. The call's final transcript and
billing are processed automatically after hangup.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.calls.hangup({
    call_id: "call_id"
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `AgentlineApi.HangupCallsRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `CallsClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.calls.<a href="/src/api/resources/calls/client/Client.ts">getTranscript</a>({ ...params }) -> unknown</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Get the full conversation transcript for a call.

Returns the complete speech-to-text transcript of the phone call,
with each turn labeled by role ("human" for the caller, "assistant"
for the AI agent). Useful for reviewing what was said on the call,
extracting information, or auditing AI agent behavior.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.calls.getTranscript({
    call_id: "call_id"
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `AgentlineApi.GetTranscriptCallsRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `CallsClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## Events
<details><summary><code>client.events.<a href="/src/api/resources/events/client/Client.ts">poll</a>({ ...params }) -> unknown</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Poll for telephony events from your AI agents.

Returns pending events such as call completions, transcripts, and
failures. Events are consumed on retrieval (one-time read) — once
polled, they are automatically deleted from the mailbox, so process or
store them. Use peek_events to look without consuming.

Returns {"events": [...], "count"}: each event has event_id, agent_id,
event_type, payload and created_at, oldest first. An empty list means
nothing is pending. Agents with a webhook receive events there instead.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.events.poll();

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `AgentlineApi.PollEventsRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `EventsClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.events.<a href="/src/api/resources/events/client/Client.ts">peek</a>({ ...params }) -> unknown</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Peek at pending telephony events without consuming them.

Returns a preview of queued events (call completions, transcripts)
without removing them from the mailbox. Useful for checking if
there are events to process before committing to retrieve them.

Returns {"pending_count", "events"}: pending_count counts every queued
event for the account (or agent_id); events lists event_id, agent_id,
event_type and created_at, without payloads. Call poll_events to get the
payloads.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.events.peek();

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `AgentlineApi.PeekEventsRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `EventsClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## Messages
<details><summary><code>client.messages.<a href="/src/api/resources/messages/client/Client.ts">list</a>({ ...params }) -> unknown</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

List SMS messages sent and received by your AI agents.

Returns message history with optional filters by AI agent or
conversation. Each entry includes direction (inbound/outbound),
phone numbers, message body, and delivery status.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.messages.list();

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `AgentlineApi.ListMessagesRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `MessagesClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.messages.<a href="/src/api/resources/messages/client/Client.ts">send</a>({ ...params }) -> unknown</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Send an outbound SMS message from an AI agent's phone number.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.messages.send({
    agent_id: "agent_id",
    to_number: "to_number",
    body: "body"
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `AgentlineApi.MessageSend` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `MessagesClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.messages.<a href="/src/api/resources/messages/client/Client.ts">listConversations</a>({ ...params }) -> unknown</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

List all SMS conversations for your AI agents.

Returns conversation threads, optionally filtered by AI agent.
Each conversation represents an ongoing SMS exchange between
an AI agent's phone number and an external contact.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.messages.listConversations();

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `AgentlineApi.ListConversationsMessagesRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `MessagesClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## Numbers
<details><summary><code>client.numbers.<a href="/src/api/resources/numbers/client/Client.ts">list</a>() -> unknown</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

List all phone numbers provisioned on your account.

Returns every phone number you've bought for your AI agents,
including which agent each number is assigned to, the number's
status (active/released), and country.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.numbers.list();

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**requestOptions:** `NumbersClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.numbers.<a href="/src/api/resources/numbers/client/Client.ts">buy</a>({ ...params }) -> unknown</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Buy a US or Canada phone number for your AI agent.

Buys a real +1 number from the carrier, attaches it to the agent and
charges $2.00 to the account balance. Once attached, the agent can make
outbound calls and answers inbound calls on this number. Not idempotent:
every successful call buys and charges for another number.

Prerequisites: an agent from create_agent with no active number (each
agent has at most one; a second purchase returns HTTP 409) and at least
$2.00 of balance (HTTP 402 otherwise; see get_account_balance).

Returns the number's id (num_..., used by release_phone_number and as
from_number_id), phone_number, country, number_type, status, cost,
balance_remaining and a private number card link (card_url,
card_image_url, card_url_expires_at). If the account has an owner email,
the card link is also emailed there.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.numbers.buy({
    agent_id: "agent_id"
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `AgentlineApi.NumberProvision` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `NumbersClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.numbers.<a href="/src/api/resources/numbers/client/Client.ts">attach</a>({ ...params }) -> unknown</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Manually attach a number that was bought outside this account.
Each agent can only have ONE active number.

Query params:
  - phone_number: E.164 format (e.g. "+12125551234")
  - agent_id: agent to attach to
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.numbers.attach({
    phone_number: "phone_number",
    agent_id: "agent_id"
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `AgentlineApi.AttachNumbersRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `NumbersClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.numbers.<a href="/src/api/resources/numbers/client/Client.ts">get</a>({ ...params }) -> unknown</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Get details of a specific phone number.

Returns the phone number, its assigned AI agent, country, and current status.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.numbers.get({
    number_id: "number_id"
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `AgentlineApi.GetNumbersRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `NumbersClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.numbers.<a href="/src/api/resources/numbers/client/Client.ts">reassign</a>({ ...params }) -> unknown</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Reassign a phone number to a different AI agent.

Moves an existing phone number from one AI agent to another.
The target agent must not already have an active number assigned.
The phone number remains active — only the agent ownership changes.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.numbers.reassign({
    number_id: "number_id",
    agent_id: "agent_id"
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `AgentlineApi.ReassignNumbersRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `NumbersClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## Webhooks
<details><summary><code>client.webhooks.<a href="/src/api/resources/webhooks/client/Client.ts">list</a>({ ...params }) -> unknown</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

List the account's per-agent webhook configuration(s).

Secrets are **masked**. Pass `agent_id` to inspect a single agent's webhook.
The full secret is only ever shown once, by set_webhook.

Returns {"webhooks": [...], "count"}: each has agent_id, url, masked
secret, signature_header, protocol, capabilities and created_at. An empty
list means no webhook is set, so events wait for poll_events. HTTP 404 if
agent_id is not an agent on this account.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.webhooks.list();

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `AgentlineApi.ListWebhooksRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `WebhooksClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.webhooks.<a href="/src/api/resources/webhooks/client/Client.ts">set</a>({ ...params }) -> AgentlineApi.WebhookCreated</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Create or replace an agent's webhook.

The configured URL receives ALL of that agent's event types — call lifecycle
(`call.received`, `call.completed`, `call.failed`), SMS (`sms.received`),
and future events — as signed JSON POSTs. Each agent may have at most one
webhook; setting it again replaces the URL. Omitted secret,
signature_header, protocol and capabilities keep their current values.

Returns agent_id, url, the full secret (shown only here; get_webhook
masks it), signature_header, protocol, capabilities and created_at.
Store the secret to verify the signature header on deliveries.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.webhooks.set({
    url: "url",
    agent_id: "agent_id"
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `AgentlineApi.WebhookConfig` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `WebhooksClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.webhooks.<a href="/src/api/resources/webhooks/client/Client.ts">delete</a>({ ...params }) -> unknown</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Remove an agent's webhook. No events for that agent will be delivered via
HTTP afterwards; they remain available via GET /v1/events (the mailbox).
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.webhooks.delete({
    agent_id: "agent_id"
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `AgentlineApi.DeleteWebhooksRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `WebhooksClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.webhooks.<a href="/src/api/resources/webhooks/client/Client.ts">test</a>({ ...params }) -> unknown</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Fire a signed `webhook.test` event to the agent's webhook.

Uses the exact same event bus (publish_event) that real telephony events use,
so a successful delivery confirms the entire pipeline is wired correctly.
Returns 404 if no webhook is configured for the agent.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.webhooks.test({
    agent_id: "agent_id"
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `AgentlineApi.TestWebhooksRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `WebhooksClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

