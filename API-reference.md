⭐ 1. Overview

Titan-X is a stateless, privacy-first adaptive intelligence engine that transforms real-time behavioural signals into clear, explainable decisions — without storing any data whatsoever.

This public preview API gives developers a simple, universal interface:

POST → /v1/evaluate

Send live signals and immediately receive an adaptation decision.

Titan-X:

stores nothing

logs nothing

processes signals in <50ms

returns fully explainable results

is safe for any industry (education, fintech, health, gaming, enterprise, etc.)

⭐ 2. Authentication

For preview, Titan-X uses a simple API key system.

Include your key in the request header:

Authorization: Bearer YOUR_API_KEY


Keys will rotate automatically when the full platform launches.

⭐ 3. Submit Evaluation Request
Endpoint
POST /v1/evaluate
Content-Type: application/json

Request Body
{
  "signals": {
    "accuracy_pct": 82,
    "time_on_task": 12400,
    "hesitation_events": 2,
    "cursor_velocity": 0.44,
    "error_count": 1
  },
  "metadata": {
    "session_id": "abc123",
    "task_id": "lesson-12",
    "client_version": "1.0"
  }
}

Notes

signals = the real-time behavioural indicators your app collects

metadata = optional context; Titan-X does not store this

No personal identifiers allowed

⭐ 4. Example Successful Response

Titan-X evaluates signals, applies the rules engine, and returns:

{
  "decision": "surface_hint",
  "reason": "low performance and hesitation",
  "signals_used": ["accuracy_pct", "hesitation_events"],
  "rule_trace": [
    {"rule_id": "accuracy_low", "matched": true},
    {"rule_id": "hesitation_high", "matched": true},
    {"rule_id": "pace_good", "matched": false}
  ],
  "confidence_score": 0.82,
  "engine_version": "preview-v1",
  "timestamp": 1700059120
}

Every response contains:

decision – the recommended adaptation

reason – plain-language explanation

signals_used – which inputs mattered

rule_trace – transparency for auditing & compliance

confidence_score – weighted evaluation result

Titan-X stores none of this.
Once sent, the event is discarded immediately.

⭐ 5. Error Handling
5.1 Missing Signals
{
  "error": "missing_signals",
  "message": "Request must include a signals object."
}

5.2 Invalid Signal Format
{
  "error": "invalid_signal_type",
  "message": "Signal 'accuracy_pct' must be numeric."
}

5.3 No API Key Provided
{
  "error": "unauthorized",
  "message": "API key missing or invalid."
}

⭐ 6. Supported Signals (Preview)

Titan-X is signal-agnostic, but these are the core supported inputs:

Signal	Description
accuracy_pct	% of correct responses
time_on_task	Time spent on the task
hesitation_events	Pauses or stalls in behaviour
cursor_velocity	Speed of cursor movement
error_count	Number of mistakes
retry_count	Number of attempts
completion_pct	Progress through task

More signals unlock at full release.

⭐ 7. Decisions Titan-X Can Return
Decision	Meaning
increase_difficulty	User performing strongly
decrease_difficulty	User struggling; reduce challenge
surface_hint	Provide small contextual help
increase_support	Larger assist; possibly multimodal
flag_friction	User experiencing difficulty or confusion
risk_alert	Behaviour resembles harmful or risky pattern
continue	No change needed

Return set expands with enterprise rulesets.

⭐ 8. Latency Targets
Stage	Time
Signal parsing	< 5ms
Rule evaluation	< 20ms
Fusion + scoring	< 10ms
Response generation	< 10ms

Total target: < 50ms p95.

⭐ 9. Rate Limits (Preview)
Tier	Requests / minute	Purpose
Free Preview	60	Testing only
Early Access	600	Small apps
Enterprise	Custom	Production load
⭐ 10. SDK Status

SDKs available at full launch:

JavaScript / TypeScript

Python

Swift (iOS)

Kotlin (Android)

Bubble Plugin

Zapier / n8n connectors

Preview includes only raw API usage.

⭐ 11. Example Client Integration
JavaScript
const response = await fetch("https://api.titanx.ai/v1/evaluate", {
  method: "POST",
  headers: {
    "Content-Type": "application/json",
    "Authorization": "Bearer YOUR_KEY"
  },
  body: JSON.stringify({
    signals: {
      accuracy_pct: 55,
      hesitation_events: 3
    }
  })
});

const data = await response.json();
console.log(data.decision, data.reason);

⭐ 12. Compliance Notes

Titan-X is designed to be fully compliant with:

UK & EU AI Act

US AI Safety directives (NIST)

GDPR

ISO 42001 (AI management)

Key features:

Zero data storage

Full explainability

No identity reconstruction

No profiling or tracking
