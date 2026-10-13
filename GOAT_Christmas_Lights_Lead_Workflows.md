# GOAT Christmas Lights: Inbound Lead Workflows

Built in Flyra (GOAT Window Cleaning & Christmas Lights account), October 2026.

## 1. What's in Flyra

### Pipelines (all three have the same stages)

| Pipeline | Lead source that routes into it |
|---|---|
| **GOAT Lights — Meta / Facebook** | `Facebook - Christmas Lights` |
| **GOAT Lights — Yard Signs (Branded)** | `Yard Sign - Branded (Lights)` |
| **GOAT Lights — Yard Signs (Non-Branded)** | `Yard Sign - Non-Branded (Lights)` |

Stages:

1. **New Lead**: automated texts run only while the lead sits here
2. **Contacted (Talked To)**: you reached them by phone
3. **Qualified ($650 / $1K Explained)**: they heard the price and are still in
4. **Appointment Booked**: sends the confirmation text automatically
5. **Appointment Held**: you sat down with both decision makers
6. **Won**
7. **Follow Up Later**: "call me in November", etc.
8. **No Response**: the automation moves leads here after the last text
9. **Not Qualified**: outside the area, a renter, under budget
10. **Lost**

> **The one rule:** as soon as you talk to a lead, move them out of **New Lead**. That stops the follow-up texts.

### Automations

| Automation | Trigger | Status |
|---|---|---|
| GOAT Lights — New Lead (Meta / Facebook) | New lead in Meta pipeline | ON |
| GOAT Lights — New Lead (Yard Sign Branded) | New lead in Branded pipeline | ON |
| GOAT Lights — New Lead (Yard Sign Non-Branded) | New lead in Non-Branded pipeline | ON |
| GOAT Lights — Appt Booked Confirmation (×3, one per pipeline) | Lead moved to Appointment Booked | ON |
| Missed Call Text-Back (existing) | Missed call | ON (wording updated) |

The existing window-cleaning automation "New Lead — META" only fires for the *Digiwerks Meta Leads* pipeline, so it won't double-text Christmas lights leads.

## 2. New-lead follow-up sequence

Every new lead gets this sequence. Each follow-up only sends if the lead is **still in New Lead**. If they text back, the sequence stops and you get a text saying "they replied, call now".

| When | What happens |
|---|---|
| Instantly | You get a text alert: "NEW lights lead: name, phone, call now" |
| +1 min | **Text 1:** instant reply (wording differs by source, see below) |
| +3 hrs | **Text 2:** "Tried to catch you, what time works for a quick call?" |
| +1 day | **Text 3:** price anchor: starts at $650, most homes around $1,000, I bring the lights to show you |
| +3 days | **Text 4:** urgency: calendar fills up once November hits |
| +6 days | **Text 5:** breakup text, then the lead moves to **No Response** |

### Text 1 by source

- **Meta / Facebook:** "Hey {first_name}! It's Mateo with GOAT Christmas Lights 🎄 Thanks for reaching out about getting your home lit up this season. I'll give you a quick call shortly to hear about your house. Is now a good time, or is there a better time today?"
- **Yard sign, branded** (sign is on a customer's home): "…Thanks for reaching out, glad you spotted one of our homes in the neighbourhood! …" Texts 2 and 4 also lean on "we're already lighting up homes on your street".
- **Yard sign, non-branded:** "…Thanks for reaching out from our sign! We design and install Christmas lights so you never have to touch a ladder. …"

### Text 3: price anchor (all sources)

> Hi {first_name}! So there are no surprises: our Christmas light installs start at $650 and most homes land around $1,000. I bring the actual lights to your door so you can see them in person, and I give you an exact price for your house on the spot. Want me to save you an appointment this week?

### Appointment Booked confirmation (all sources)

> You're all set {first_name}! 🎄 Looking forward to our Christmas lights appointment. I'll bring the actual lights so you can see them in person, and I'll show you exactly what your home would look like and what it would cost. Since it's a decision for the household, please make sure everyone who'd be deciding can be there. See you soon! Mateo, GOAT Christmas Lights

### Missed call text-back

> Hey, it's Mateo with GOAT 🎄 Sorry I missed your call, I'm with a customer right now. Are you calling about Christmas lights or window cleaning? Text me back here with your name and address and I'll call you right back!

This number is shared with window cleaning, so the text asks which service they're calling about.

## 3. Phone script (the appointment model)

**1. Open and qualify (2–3 min)**
- "Hey {name}, it's Mateo with GOAT Christmas Lights, you reached out about getting your house lit up. Got a couple minutes?"
- Do you own the home? (Renters → Not Qualified unless the landlord approves)
- What's the address? (Check it's in your service area)
- What are you picturing: roofline only, or roofline plus trees, bushes and windows?
- Have you had lights professionally installed before?
- Who else would be part of the decision? (Spouse or partner → they must be at the appointment)

**2. Anchor the price**
- "Just so you know where we land: our installs start at $650, and the average home ends up around $1,000 depending on what you want lit up. Does that fit what you were thinking?"
- Yes → move to **Qualified**. Hard no → **Not Qualified** or **Follow Up Later**.

**3. Book the in-person appointment**
- "The best way to do this is for me to come by, show you the actual lights in person, and show you exactly what your house would look like and cost. It's quick. I need you and {spouse} both there, since it's a decision you'll make together. Does {day} at {time} or {day} at {time} work better?"
- Book it → move to **Appointment Booked** (the confirmation text goes out automatically).

**4. The sit-down**
- Both decision makers at the table. Show the lights and the design for their home, then the price.
- Close → **Won** (use Convert in Flyra to create the customer and job). Not yet → **Follow Up Later**.

## 4. Getting leads into Flyra (and keeping costs down)

**Recommendation: run all automated texting from Flyra, not from a separate tool.** You already pay for Flyra and it already sends texts, so the sequences above add no new software. A tool like GoHighLevel, or a Zapier sequence, would be an extra monthly bill doing the same job.

How each source gets into the right pipeline:

- **Facebook / Meta:** Your Facebook page is already connected to Flyra. Once you build the Christmas lights instant form in Meta Ads Manager, its leads have to be pointed at **GOAT Lights — Meta / Facebook**. Do this in Flyra under *Leads → Integrations → Form routing*, or ask Claude to do it. **Right now no lights form exists**, and unrouted forms land in "Digiwerks Meta Leads", which runs the window-cleaning sequence.
- **Yard signs (calls/texts that come into Quo):** Quo doesn't push leads into Flyra on its own. Options, cheapest first:
  1. **Free and manual (start here):** when a yard sign call or text comes in on Quo, add the lead in the Flyra app with source *Yard Sign - Branded (Lights)* or *Yard Sign - Non-Branded (Lights)*. It routes to the right pipeline, and the sequence starts if you add them on the New Lead stage. About 20 seconds per lead.
  2. **Use your Flyra number on the yard signs** instead of the Quo number. Calls and texts then land straight in Flyra, and the missed-call text-back fires automatically. Using a different number for branded and non-branded signs lets you tell the two apart.
  3. **Automatic Quo → Flyra:** a Quo webhook (call or message received) feeds a Flyra *Inbound webhook* automation that creates the lead in the right pipeline. No monthly cost, but you need a separate Quo number per sign type to tell them apart, and the webhook URL has to be set up in Flyra and Quo. Check that your Quo plan includes webhooks/API.

### Setting up option 3 (Quo → Flyra webhook)

Two automations are already built in Flyra, both **ON** (they do nothing until Quo sends to them):
- *Quo → Flyra: Yard Sign Branded leads*: creates the lead in the Branded pipeline
- *Quo → Flyra: Yard Sign Non-Branded leads*: creates the lead in the Non-Branded pipeline

Steps:
1. **Get one Quo number per sign type.** Print number A on branded signs and number B on non-branded signs. This is how Flyra tells the two apart.
2. **Copy the webhook URL from Flyra.** Open each Quo → Flyra automation in the Flyra web app (*Automations*), click the trigger step, and copy its webhook URL.
3. **Create the webhooks in Quo.** You need to be an Owner or Admin. In the Quo web or desktop app go to *Settings → Integrations → Webhooks*, and for each sign number create a webhook:
   - URL: the matching Flyra webhook URL
   - Events: `message.received` and `call.completed` (a completed call includes missed calls and voicemails)
   - Phone number: only that sign's number
4. **Test before trusting it.** Turn on the Quo → Flyra automation and text and call the sign number from your cell. Check that:
   - one lead appears in the right pipeline, with the caller's phone number filled in
   - texting a second time doesn't create a duplicate lead
   - the New Lead text sequence starts
5. If the phone number comes through blank, or every text creates a new lead, the payload isn't mapping cleanly. Use the fallback below.

**Fallback:** use [Make.com](https://www.make.com) (free tier). Its scenario is *Quo webhook → search Flyra for the phone number → if not found, create the lead in the right pipeline* through the Flyra REST API. Create the API key at app.flyra.io/developer.

> Note: Flyra's missed-call text-back only fires for calls to your **Flyra** number. Missed calls on Quo need Quo's own missed-call auto-reply. Paste the same missed-call text from section 2 into Quo so both numbers say the same thing.

## 5. Before turning it on

1. Read the texts above and tell Claude (or edit in Flyra) anything you'd word differently.
2. Turn on the 3 **New Lead** automations and the 3 **Appt Booked** automations in Flyra (*Automations*).
3. Test: add yourself as a lead in each pipeline and confirm you get the alert and Text 1.
4. Once the Facebook lights form is live, route it to **GOAT Lights — Meta / Facebook**.
