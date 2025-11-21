Signals & Events — Titan-X Developer Documentation

Signals and events are the foundation of Titan-X.
Everything Titan-X does — every adaptation, decision, and explanation — is generated from real-time signal flows rather than stored data or historical profiles.

This document explains what signals are, how events are constructed, and how Titan-X processes them without retaining any user data.

⭐ 1. What Is a Signal?

A signal is a tiny, real-time behavioural datapoint.

Signals are:

anonymous

transient

descriptive of behaviour, not identity

processed instantly and then discarded

Examples:

keypress_interval_ms

cursor_velocity

navigation_depth

completion_time_sec

gesture_accuracy_pct

latency_score

Signals describe what happened, not who, where, or why.

⭐ 2. What Is an Event?

An event is a grouped packet of signals sent to Titan-X.

Example structure:

{
  "session_id": "anon_7fa2",
  "timestamp": 1700002219,
  "event_type": "task_completed",
  "signals": {
    "accuracy_pct": 92,
    "time_to_complete": 3200,
    "keypress_interval_ms": 87,
    "cursor_velocity": 0.44
  }
}

Titan-X never stores:

session IDs

timestamps

behavioural histories

navigation journeys

They exist only long enough for Titan-X to compute a decision.

⭐ 3. Real-Time Signal Windowing

Titan-X does not use large datasets or histories.
Instead it analyses sliding windows of live signals.

Window example:

Window size: 10 seconds

Signals processed: ~400

Retention time: 0ms after decision

This approach:

meets EU AI 2026 transparency requirements

avoids behavioural profiling

gives predictable, explainable outputs

⭐ 4. Why Signals Matter (vs ML Models)

Most AI systems rely on:

stored data

user profiles

behavioural tracking

opaque models

Titan-X does not.
Titan-X uses deterministic rules that are:

transparent

explainable

traceable

debuggable

compliant

Rules process signals to produce decisions.

⭐ 5. Signal Categories Titan-X Supports
1. Performance Signals

accuracy

completion time

consistency

pace variance

error frequency

2. Interaction Signals

cursor/gesture movement

click density

scroll velocity

UI navigation

3. Cognitive Effort Signals

hesitation

correction behaviour

retry behaviour

pace drop-offs

4. Environment Signals (optional)

latency

viewport resize events

device input type

None of these signals identify a user.

⭐ 6. Creating an Event Payload

When integrating with Titan-X, events are typically sent like:

POST /ingest
{
  "event_type": "exercise_progress",
  "signals": {
    "accuracy_pct": 88,
    "time_to_complete": 4500,
    "cursor_velocity": 0.52
  }
}

Titan-X returns a decision:

{
  "decision": "increase_difficulty",
  "reason": "high accuracy and consistent performance",
  "signals_used": ["accuracy_pct", "time_to_complete"]
}

No logs stored.
No database entry.
The payload is immediately discarded.

⭐ 7. Best Practices for Developers
✔ Keep signals simple

Titan-X is designed for high-volume, simple behavioural datapoints.

✔ Don’t send identity

Never include email, names, IPs, IDs, tokens, or session identifiers.

✔ Use consistent naming

Use snake_case keys for clarity.

✔ Avoid overloading events

Small, frequent events > huge bulky events.

✔ Always verify the decision

Responses include structured reasons you can use in UI logic.

⭐ 8. What’s Coming Next

Titan-X will ship with:

Signal validator schemas

Example payloads for multiple industries

Real-time debugging UI (explainability mode)

Auto-generated “decision traces” for auditors
