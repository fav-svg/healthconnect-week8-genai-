# Known Limitations — GenAI Track (Week 8)

## 1. Ambiguous requests are not distinguished from unsupported requests

Genuinely vague queries (e.g. "Can you help me with something?") currently receive the exact same generic fallback as clearly off-topic queries (e.g. "What is the weather like today?"):

> "I don't have information on that. I'd recommend contacting clinic reception directly."

**Why this matters:** An ambiguous request means the user might have a valid, in-scope question but phrased it too vaguely for `retrieve()` to match. Ideal behavior would ask a clarifying question (e.g. "Could you tell me more about what you need help with — appointments, services, or reminders?") rather than turning the user away as if the topic itself were unsupported. This is a real gap between "ambiguous" and "unsupported" that the current design collapses into one response path.

## 2. No live/dynamic data access

The assistant is grounded entirely in the static HealthConnect Knowledge Base. It cannot confirm real-time information (e.g. actual appointment availability, live wait times) — only general policy/process information. Queries like "Do you have walk-in appointments?" are correctly flagged as unconfirmed rather than guessed, but this also means the assistant can never give a definitive yes/no on anything requiring live data.

## 3. No true booking/transaction capability

By design, the assistant only informs — it cannot book, confirm, reschedule, or cancel appointments. This is enforced correctly (see Fix 1 in `final_test_results.md`), but every actual transaction still requires a human handoff to reception, which limits how much administrative burden the assistant can genuinely offload.

## 4. Reminder-channel guidance is advisory only

The `REMINDER_TIP` (SMS reminders had a 45.8% no-show rate vs. 51.4% with no reminder) is informational — the assistant cannot actually set or change a patient's reminder preference; it can only suggest.
