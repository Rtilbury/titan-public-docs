⭐ 1. Overview

Titan-X is built on a strict event-driven architecture.

Every interaction sent to Titan-X (signals, metadata, task identifiers) is processed as an event, and every adaptive output (recommendation, insight, explanation) is also an event.

This event-level transparency is what makes Titan-X align with the 2026+ global AI regulations:

Explainable AI

Traceability

Behaviour-based safety

Audit readiness

Data minimisation

Titan-X stores no identifying data and no long-term logs.
Events are processed, derived, audited, and immediately anonymised.

⭐ 2. What Is an “Event”?

An event is any discrete action or signal that occurs within a user session.

Titan-X classifies events into four categories:

Input Events – signals sent by the client

Derived Events – signals generated internally

Decision Events – internal reasoning steps

Output Events – what Titan returns to the client

Example sequence:

1. INPUT: user submitted signals → event created  
2. DERIVED: Titan generates confidence_delta  
3. DECISION: Titan selects an adaptation rule  
4. OUTPUT: Titan returns difficulty_adjustment + explanation


This structure keeps every outcome audit-ready while remaining privacy-safe.

⭐ 3. Event Schema (Public API)
{
  "event_id": "uuid",
  "timestamp": "2025-01-01T12:00:00Z",
  "event_type": "input | derived | decision | output",
  "session_id": "client-session-uuid",
  "task_id": "optional",
  "payload": {}
}


Titan-X guarantees:

All timestamps are ISO-8601

All event IDs are UUIDv4

No personal data is stored

Events are purged after processing unless the partner opts into rolling audit logs

⭐ 4. Input Event Logging (What You Send)

Input events represent raw behavioural signals.

Example:

{
  "event_type": "input",
  "payload": {
    "signals": {
      "accuracy_pct": 80,
      "time_on_task": 9200,
      "hesitation_events": 2
    }
  }
}


Titan stores these only long enough to:

validate them

derive additional signals

compute adaptive output

produce an explainability chain

After that, signals are discarded permanently.

⭐ 5. Derived Event Logging (What Titan Computes)

These are system-generated, non-identifying insights.

Examples:

Derived Signal	Inputs	Purpose
confidence_delta	accuracy + hesitation	How confident the user is
fatigue_estimate	time + errors	Cognitive overload indicator
risk_trend	impulsivity + escalation	Safer-betting compliance
pace_stability	timing + consistency	Flow of behaviour

Example logged event:

{
  "event_type": "derived",
  "payload": {
    "derived_signals": {
      "confidence_delta": -0.12,
      "fatigue_estimate": 0.22
    }
  }
}

⭐ 6. Decision Event Logging (How Titan Thinks)

This is the core of explainable AI.

A decision event shows:

which rule fired

what triggered it

what thresholds were breached

which signals contributed

how the final score or recommendation was chosen

Example:

{
  "event_type": "decision",
  "payload": {
    "rule_fired": "pace_slow_adaptation_v3",
    "trigger_signals": {
      "time_on_task": 18200,
      "hesitation_events": 3
    },
    "decision_reasoning": "User is performing below expected pace baseline for this task type."
  }
}


These events make Titan-X fully auditable, transparent, and regulator-ready.

⭐ 7. Output Event Logging (What Titan Returns)

Output events are simply what your client API receives.

Example:

{
  "event_type": "output",
  "payload": {
    "recommendation": "reduce_difficulty",
    "explanation": "User pace slowed by 38% and hesitation increased."
  }
}


Titan ONLY returns non-sensitive information.

⭐ 8. Explainability Chain (End-to-End Flow)

Titan-X provides a 3–7 step explanation chain that partners can expose in UI or store for compliance.

Sample end-to-end explainability chain:

Input: User sent 9 signals

Derived: Titan generated fatigue_estimate = 0.27

Rule Triggered: difficulty_reduce_rule_v2

Contributing Factors:

High hesitation

Increase in error rate

Reduced navigation speed

Safety Context: Beginner-level skill band

Output: Suggest easier content

Explanation (inline):

“Your pace slowed and accuracy dropped, so we’re adjusting the challenge level.”

This meets the future legal requirement of:

“Meaningful information about the logic involved.”

⭐ 9. Audit Logs (Enterprise Optional)

Some partners (e.g. fintech, racing integrity teams) may opt into rolling audit logs.

Titan supports:

Retention	Who It’s For	Notes
0 days (default)	privacy-first environments	No data stored
1–7 days	internal analysts	Events remain anonymised
30–90 days	compliance-heavy sectors	Requires partner consent

No personal identifiers are ever included.

⭐ 10. Compliance Notes (Aligns with 2026 AI Regulations)

Titan-X automatically satisfies:

✔ Explainability Requirements

Through decision logs + reasoning strings

✔ Behaviour-Based Safety Controls

Through risk, fatigue, trend, and pattern signals

✔ Traceable AI

Via full event chain architecture

✔ Data Minimisation

No personal data ingested
No long-term storage by default

⭐ 11. Example Full Session Log (Human-Readable)
Session Start → Event 1: Input Received
Event 2: Derived Confidence Delta
Event 3: Derived Fatigue Score
Event 4: Decision Triggered (Rule: beginner_safe_lane)
Event 5: Output Returned (Next Step: easier content)
Session Purged


Partners can convert this into UI components like:

“See why this recommendation was made”

“Your skill pattern trend this week”

“Your fatigue score is improving”

⭐ 12. Security & Privacy Guarantees

Titan-X guarantees:

No cookies

No cross-session tracking

No user identifiers

No sensitive data

No long-term profiling

No model training on individual data

Titan is a real-time adaptation engine, not an identity engine.

⭐ 13. Change Log
Version	Changes
Preview-v1	Initial release
