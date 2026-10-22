# Run My Day

The one orchestration prompt for TKG Group procurement and logistics. Paste the body below into Claude when you want to work through today's email, source new requests, add freight, build estimates, and dispatch anything the customer has approved. Nothing sends or books without your explicit go.

## How to use

1. Open a new Claude conversation (web app or desktop).
2. Make sure the Outlook (Microsoft 365), Square, and your custom skills (procurement agent, estimator agent 2, invoice collector, books agent, logistics agent) are available.
3. Paste the whole "Prompt" block below.
4. Answer the clarifying questions it raises. Give the gos it asks for.
5. Run it again later in the day if more customer approvals or supplier replies land.

## Prompt

Run my day for TKG Group procurement and logistics.

This is the one prompt that chains my email agent (procurement agent for new email, invoice collector for supplier invoices and receipts), procurement agent for sourcing both local and online suppliers, logistics agent for freight, estimator agent for pricing and Square estimates, and books agent for the General Ledger and draft invoices.

What this run does, in plain language.

1. Scout my inbox for new customer supply requests.
2. If a request is missing information I need to source it (quantity, spec, destination community, needed by date, delivery address), draft a clarifying email to the customer in Outlook drafts and park the request. Do not guess.
3. Source complete requests from my existing suppliers first, then online if nothing fits. Add freight for the destination.
4. Build a draft estimate in Square and a draft reply email in Outlook drafts for every complete request.
5. When a customer accepts an estimate, convert it to a draft invoice in Square, draft the supplier PO, book the freight, and draft a shipment notification.

Nothing gets sent and nothing gets booked without my explicit go. All reply drafts land in Outlook drafts. All estimates and invoices land in Square as drafts. All supplier POs land in Outlook drafts.

### Step 1. Triage email since the last run.

Classify every new message in my inbox since the last run.

a. New supply request from a customer. Route to step 2.
b. Supplier quote reply (we asked for pricing). Attach the quote to the open sourcing task.
c. Supplier invoice or shipping confirmation. Route to the invoice collector so the PDF gets filed in the correct year folder on my desktop.
d. Customer answer on an estimate we sent. If accepted, route to step 5. If a question, draft a reply in Outlook drafts and stop there for that thread.
e. Carrier invoice or waybill. Pass to invoice collector for filing, and match to the open booking (logistics agent).
f. Noise. Skip.

### Step 2. Scout and source new supply requests.

For each new supply request, first check it has what we need to source it: item description or part number, quantity, destination community, delivery address, needed by date, any specs or substitutions allowed.

If anything critical is missing, draft a clarifying reply in Outlook drafts asking for exactly the missing fields in a short bulleted list. Park the request. Do not source. Move on to the next message.

For complete requests, call the procurement agent.
It identifies items and quantities. It checks my existing suppliers first (local or regional accounts I already have). If no existing supplier carries the item, it searches online suppliers. It comes back with vendor, unit cost, lead time, and pickup location per line.

If two suppliers are candidates, pick one and explain the choice in one sentence (lowest landed, fastest lane, or best past reliability).

### Step 3. Quote the freight.

For each sourced line, call the logistics agent in quote mode with: vendor pickup location, item weight and dimensions, destination community, needed by date, and any special handling (freezable, hazmat, oversize).

It returns a freight estimate (CAD), the proposed lane (truck to Pickle Lake, air cargo north, winter road if open for that community), and the proposed carrier.

If the destination is fly in only right now and the item is restricted on aircraft, flag it. Do not quote a lane that will not fly.

### Step 4. Build the estimate.

Call the estimator agent with the landed cost per line (supplier cost plus freight) and the destination.

It applies TKG margin: 75 percent markup if landed cost per unit is under $10, 30 percent otherwise.
It copies the MASTER SHEET tab in my master budget workbook into a new tab for this estimate and fills it in.
It creates a draft estimate in Square against the correct customer. If the customer is new or ambiguous, it stops and asks me rather than creating a duplicate.
It drafts a reply email in Outlook drafts linking the Square estimate and listing what was sourced, from whom, and expected delivery window.

### Step 5. Dispatch approved estimates and build the draft invoice.

For every Square estimate that moved to accepted since the last run, do this:

a. Convert the accepted estimate to a draft invoice in Square. Do not send. Carry over all lines, taxes, and the customer record. Confirm the HST line is right (Ontario, 13 percent, unless the customer is exempt and on file as such).
b. Draft the supplier PO in Outlook drafts (if the supplier takes email) or prepare the portal order and wait for my go.
c. Call the logistics agent in dispatch mode on the quoted lane and carrier. It books pickup and returns waybill plus ETA.
d. Call the books agent to log the booking against the draft invoice in the General Ledger tab of my master budget workbook: carrier, waybill, freight cost actual, pickup date, ETA, linked invoice number.
e. Draft a shipment notification to the customer in Outlook drafts with carrier, waybill, pickup date, and ETA.
f. Leave the invoice in draft until I send it. Flag anything blocking a send (missing customer PO reference, pricing variance, backorder).

### Step 6. End of run summary.

Give me a report in this shape.

a. New supply requests scouted. Table: sender, customer, items asked for, status (complete and sourced, or parked waiting on info, or clarifying reply drafted).
b. New estimates drafted today. Table: customer, lines, draft estimate URL, destination, total.
c. Draft invoices created from accepted estimates. Table: customer, invoice number, lines, total, HST handling.
d. Shipments dispatched today. Table: customer, carrier, waybill, ETA.
e. Blocked items and why. One line each (missing info from customer, no supplier found online or local, air restricted, winter road closed, carrier capacity, customer not matched, supplier price jump over 15 percent).
f. Decisions I need to make. One line per decision with a recommended answer.
g. AR nudges due today (from the books agent).

### Rules.

- Nothing sends from Outlook without my go.
- No supplier orders submit without my go.
- No carrier bookings without my go. Dispatch mode of logistics agent returns a proposed booking. I approve. Then book.
- No new Square customer without my go if there is any close name match.
- All drafts carry my signature block. Plain language. No sales speak.
- All numbers in CAD unless the supplier quoted USD, in which case show both and the FX used.
- No dashes in prose in anything you draft for me. Commas, periods, parentheses, or line breaks instead.
