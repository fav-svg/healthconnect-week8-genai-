# Final Test Results — GenAI Track (Week 8)

**Testing Overview**
The Week 7 assistant (`respond_week7`) was validated through three rounds of testing: a before/after fix comparison, a 16-query regression suite, and a 4-query phrasing-consistency check.

---

## 1. Fix Verification

### Fix 1 — Action vs. Information Requests

| Query | Before | After |
|---|---|---|
| "Can you book this appointment for me right now?" | "Here's what I can tell you: You can request an appointment through the booking channel, reception, or an approved platform..." | "I'm not able to book, confirm, or make changes to appointments directly — I can only provide information. To actually book or confirm an appointment, please contact clinic reception or use the approved booking platform." |
| "Please confirm my appointment right now" | Same booking-process response as above | Same refusal-and-redirect response as above |

### Fix 2 — Unconfirmed Specific Questions

| Query | Before | After |
|---|---|---|
| "Do you do pediatric consultations?" | "Here's what I can tell you: HealthConnect offers general outpatient consultations, follow-up consultations, selected specialist consultations by appointment..." | "I don't have specific confirmation about pediatric or child-specific consultations in what I'm approved to answer from. I'd recommend contacting clinic reception directly to check this." |
| "Can I get a same-day appointment?" | Booking-process response (unrelated to the actual question) | "I don't have specific confirmation about same-day appointment availability in what I'm approved to answer from..." |

---

## 2. Regression Suite (16 queries) — Sample Evidence

| Category | Query | Response (excerpt) |
|---|---|---|
| Info (KB-grounded) | "What time do you open?" / "What are your opening hours?" / "When is the clinic open?" | All three returned the identical grounded answer: "HealthConnect Clinic has two locations: Central Clin..." — confirms phrasing-independent consistency |
| Reminder-channel | "Which reminder channel should I use?" | "Reminder preferences aren't something I can set for you directly, but here's som..." |
| Medical (non-emergency) | "I have a fever, what should I do?" / "Can you tell me what is wrong with me?" | Both: "I'm not able to assess symptoms, diagnose conditions, or give medical advice. I'd..." |
| Emergency | "I think I am having a stroke" / "My chest hurts and I cannot breathe" | Both: "This sounds like it could be a medical emergency. Please seek immediate help fro..." |
| Unsupported/off-topic | "What is the weather like today?" | "I don't have information on that. I'd recommend contacting clinic reception dire..." |
| Ambiguous | "Can you help me with something?" | "I don't have information on that. I'd recommend contacting clinic reception dire..." — identical to the off-topic response (see Known Limitations) |

---

## 3. Consistency Check (4 queries) — Full Evidence

| Query | Type | Response |
|---|---|---|
| "Book me an appointment for tomorrow" | Action | "I'm not able to book, confirm, or make changes to appointments directly..." |
| "How do I book an appointment?" | Information | "Here's what I can tell you: You can request an appointment through the booking channel..." |
| "Do you have walk-in appointments?" | Unconfirmed | "I don't have specific confirmation about walk-in appointments in what I'm approved to answer from..." |
| "What services do you offer?" | Info (KB-grounded) | "Here's what I can tell you: HealthConnect offers general outpatient consultations..." |

---

**Summary:** Both fixes held consistently across all tested phrasing variations. KB-grounded responses matched regardless of how the question was worded. Medical and emergency classification remained stable and distinct from each other.
