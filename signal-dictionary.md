⭐ 1. Overview

Signals are the core behavioural inputs Titan-X uses to:

interpret user behaviour

evaluate real-time friction

assess confidence, risk, skill and pace

generate safe, explainable adaptation decisions

Signals are stateless, ephemeral, and non-identifying.
Titan-X never stores or links signals to any user.

This dictionary describes every signal supported in the Preview API, plus extended signals that unlock in the Enterprise tier.

⭐ 2. Signal Categories

Titan-X recognises several classes of behavioural signals:

Performance Signals – how well tasks are being completed

Tempo & Pace Signals – how smoothly behaviour is flowing

Cognitive-Load Signals – indicators of hesitation, friction, overload

Risk & Stability Signals – markers of unsafe behaviour patterns

Progression Signals – indicators of advancement or regression

Environmental Signals – optional context from the client device

Content Signals – metadata about what is being attempted

Each category is modular: developers can send as few or as many as they wish.

⭐ 3. Supported Signals (Preview Tier)

These signals are available immediately with the public API.

3.1 Performance Signals
Signal	Type	Description	Typical Range
accuracy_pct	number	Percent correct	0–100
error_count	number	Total mistakes within task	0–10
retry_count	number	Attempts to complete task	0–10
score_raw	number	Raw numeric score	any
score_normalised	number	0–1 normalised score	0–1
3.2 Tempo & Pace Signals
Signal	Type	Description	Range
time_on_task	number	ms spent on activity	0–∞
completion_time	number	ms to finish	0–∞
cursor_velocity	number	px/ms (movement speed)	0–5
scroll_velocity	number	scroll speed	0–5
navigation_speed	number	time between screen changes	0–∞
3.3 Cognitive Load / Friction Signals
Signal	Type	Description
hesitation_events	number	Count of pauses, stalls, indecision
undo_actions	number	Reversal of actions, indicates uncertainty
long_dwell	boolean/number	Extended hover or pause on specific UI elements
rapid_backtrack	number	Quick returns to previous screens (confusion indicator)
3.4 Risk & Safety Signals
Signal	Type	Description
risk_escalation_rate	number	Pace at which behaviour becomes risky (context-dependent)
unstable_sequence_count	number	Repeated shifts between high and low control
impulsive_action_count	number	Rapid interactions without processing
dropout_probability	number	0–1 predicted chance the user abandons
3.5 Progression & Mastery Signals
Signal	Type	Description
completion_pct	number	Progress through task (0–100)
mastery_score	number	ML-backed mastery estimate (0–1)
stability_score	number	Smoothness vs volatility of behaviour (0–1)
3.6 Environmental Signals (Optional)

These are stripped immediately after processing.

Signal	Type	Description
device_type	string	"mobile", "tablet", "desktop"
connection_quality	number	ms latency / quality multiplier
screen_size	string	e.g. "1920x1080"
⭐ 4. Extended Signals (Enterprise Tier)

These unlock with higher-tier deployments and industry-specific implementations.

4.1 Multi-Modal Input Signals
Signal	Description
gaze_stability	Uses optional eye-tracking SDK
voice_sentiment	Real-time sentiment analysis of spoken audio
gesture_precision	AR/VR or 3D environments
4.2 Collaboration / Social Signals
Signal	Description
group_sync_level	Smoothness of multi-user collaboration
turn_taking_equity	Balanced participation in group tasks
4.3 Domain-Specific Signals

Titan-X can ingest external signals — examples:

Education

reading pace

decoding difficulty

distractibility patterns

Fintech / Trading

order-change volatility

risk-absorption curve

chase behaviour probability

Gaming

APM (actions per minute)

reaction-time deltas

micro-error patterns

Racing & Sports

decision-timing

pace vs expectation

positional stability

These are modular and optional.

⭐ 5. Signals Titan-X Automatically Derives

Titan-X also generates secondary signals by fusing multiple inputs:

Derived Signal	Inputs	Meaning
confidence_delta	accuracy + pace + stability	Strength of user intent
fatigue_estimate	error_count + hesitation	Likely cognitive fatigue
focus_stability	dwell + cursor patterns	Consistency of attention
risk_trend	escalation_rate + impulsive_actions	Worsening risk profile

These derived signals never leave the engine unless requested.

⭐ 6. Minimum Recommended Signals

You may send any number of signals, but Titan-X performs best with a minimum of:

accuracy_pct
time_on_task
hesitation_events
error_count
completion_pct


Lightweight apps can send fewer.

Enterprise models perform best with 10–20 signals.

⭐ 7. Deprecated / Not Supported Signals

Titan will never accept:

biometric identifiers

personal identity data

location

IP address

cookies

facial recognition signals

The engine is privacy-first by design.

⭐ 8. Example Comprehensive Payload
{
  "signals": {
    "accuracy_pct": 72,
    "time_on_task": 18200,
    "hesitation_events": 3,
    "cursor_velocity": 0.34,
    "retry_count": 1,
    "completion_pct": 55,
    "risk_escalation_rate": 0.12,
    "unstable_sequence_count": 2
  },
  "metadata": {
    "session_id": "abc-123",
    "task_id": "lesson-01"
  }
}

⭐ 9. Change Log
Version	Changes
Preview-v1	Initial public dictionary
