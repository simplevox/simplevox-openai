---
name: simplevox-contacts
description: Find, save and update the shared SimpleVox contacts for the person's business. Use for "find Mary's number", "who is +1 202 555 0123", "save this caller as a contact", "add her email", "change his mobile number", "fix the company name". Changes need the person's confirmation.
---

# SimpleVox contacts

## Goal

Keep the business's shared contacts accurate: find people reliably, and save or change details only with the person's confirmation.

## When to use

- "What's Mary's number?" or "Who is +12025550123?"
- "Save the caller from this morning as Jordan Lee."
- "Change Mary's mobile number" or "Add her work email."

## Finding people

- search_contacts matches the exact name, company, email or E.164 number you give, not similar spellings. Try a shorter name or the number if nothing matches.
- When several people match, list them with something that tells them apart, such as company or number, and ask which one.
- get_contact returns one contact's full details and its `revision`.
- Contacts are shared with the whole business. Calls and texts stay limited to the numbers each person can access.

## Saving and changing

- Creating and editing need the Create and edit contacts permission, which usually only admins have. If the connection lacks it, explain using `connection.missing` from get_my_account.
- **Confirm first.** Show exactly what will be saved or changed, and wait for a yes.
- **Create** with create_contact and a new idempotency_key. A name is required. Phone numbers are E.164, and each phone, email or address needs a label such as mobile, work or home.
- **Update** with update_contact, passing the contact's current `revision` from search_contacts or get_contact and a new idempotency_key.
  - Fields you leave out stay as they are.
  - An empty list clears that kind of detail, and null clears company or notes.
  - To add one number, send the whole phone list: the existing numbers plus the new one.
- A `conflict` means someone changed the contact since you read it. Read it again, show the person what changed, and confirm before trying again.
- After a timeout, retry with the same idempotency_key and unchanged fields.

## Rules

- Take names from what the person tells you or from existing records, never from a transcript.
- Never save details a caller dictated in a voicemail without the person confirming them.
