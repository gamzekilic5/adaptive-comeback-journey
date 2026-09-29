# Adaptive Comeback Journey — Analytics Tracking Plan

## 1. Purpose

This tracking plan defines the events and properties required to measure the
Adaptive Comeback Journey.

The goal is to understand:

- How many returning players become eligible
- Which comeback experiences players receive
- Whether players engage with the feature
- Where players drop off during the journey
- Whether players complete missions and claim rewards
- Whether the feature improves post-return retention and engagement
- Whether personalization creates incremental value over a generic comeback experience

The tracking design should support both product analysis and the proposed
Control vs Generic vs Adaptive experiment.

---

## 2. Core Experiment Properties

The following properties should be attached to relevant experiment events.

| Property | Description | Example |
|---|---|---|
| player_id | Unique player identifier | 847291 |
| experiment_group | Assigned experiment group | treatment_b |
| player_segment | Behavioral segment | struggling |
| journey_type | Assigned comeback journey | momentum_path |
| inactivity_days | Days inactive before return | 5 |
| journey_id | Unique journey instance | CJ_847291_01 |
| platform | Player platform | iOS |
| country | Player country | Turkey |
| timestamp | Event timestamp | 2026-09-29T18:30:00Z |

For Control players, `journey_type` and `player_segment` may be null where appropriate.

---

## 3. Event Taxonomy

### Event 1 — `comeback_eligible`

Triggered when the system determines that a returning player meets the
eligibility requirements.

**Important properties:**

- player_id
- experiment_group
- inactivity_days
- platform
- country
- timestamp

**Product question:**

How many returning players qualify for the comeback experience?

---

### Event 2 — `comeback_exposed`

Triggered when the Comeback Journey interface is shown to the player.

**Important properties:**

- player_id
- experiment_group
- player_segment
- journey_type
- journey_id
- inactivity_days
- timestamp

**Product question:**

How many eligible players are actually exposed to the feature?

---

### Event 3 — `comeback_started`

Triggered when the player begins interacting with the assigned Comeback Journey.

**Important properties:**

- player_id
- experiment_group
- player_segment
- journey_type
- journey_id
- timestamp

**Product question:**

What percentage of exposed players start the comeback experience?

---

### Event 4 — `mission_started`

Triggered when a player begins progress toward a comeback mission.

**Important properties:**

- player_id
- journey_id
- player_segment
- journey_type
- mission_id
- mission_stage
- mission_target
- timestamp

**Example:**

```text
mission_id: momentum_01
mission_stage: 1
mission_target: complete_2_levels
```

---

### Event 5 — `mission_completed`

Triggered when the player satisfies the requirement of a mission.

**Important properties:**

- player_id
- journey_id
- player_segment
- journey_type
- mission_id
- mission_stage
- completion_time
- timestamp

**Product question:**

At which mission stage do players most frequently drop off?

---

### Event 6 — `reward_claimed`

Triggered when the player claims an unlocked mission reward.

**Important properties:**

- player_id
- journey_id
- player_segment
- journey_type
- mission_id
- reward_type
- reward_amount
- timestamp

**Product question:**

Do players claim the rewards they unlock, and which reward types generate the
strongest continuation behavior?

---

### Event 7 — `comeback_completed`

Triggered when the player completes the final mission of the Comeback Journey.

**Important properties:**

- player_id
- journey_id
- player_segment
- journey_type
- total_missions_completed
- journey_completion_time
- timestamp

**Product question:**

What percentage of players complete the full comeback experience?

---

### Event 8 — `comeback_expired`

Triggered when the Comeback Journey reaches its expiration time without being
completed.

**Important properties:**

- player_id
- journey_id
- player_segment
- journey_type
- last_completed_mission
- timestamp

**Product question:**

Where were players when their journey expired?

---

## 4. Core Funnel

The main feature funnel is:

```text
COMEBACK ELIGIBLE
        |
        v
COMEBACK EXPOSED
        |
        v
COMEBACK STARTED
        |
        v
MISSION 1 COMPLETED
        |
        v
MISSION 2 COMPLETED
        |
        v
MISSION 3 COMPLETED
        |
        v
COMEBACK COMPLETED
```

This funnel should be analyzed overall and separately by:

- Experiment group
- Player segment
- Journey type
- Platform
- Country
- Inactivity duration

---

## 5. Funnel Metrics

### Feature Start Rate

```text
Players who started the journey
--------------------------------
Players exposed to the journey
```

Measures whether the feature successfully motivates returning players to engage.

---

### Mission Completion Rate

```text
Players completing a mission
-----------------------------
Players who started that mission
```

Should be calculated separately for each mission stage.

This helps identify excessive difficulty or weak motivation within the journey.

---

### Journey Completion Rate

```text
Players completing the final mission
-------------------------------------
Players who started the journey
```

Measures whether the complete mission structure is achievable and engaging.

---

### Reward Claim Rate

```text
Players claiming an unlocked reward
------------------------------------
Players who unlocked that reward
```

A low claim rate may indicate UX friction, unclear communication, or low perceived reward value.

---

## 6. Experiment Success Metrics

### Primary KPI — D7 Post-Return Retention

```text
Players active on Day 7 after experiment entry
-----------------------------------------------
Players entering the experiment
```

This is the primary measure of whether the comeback experience creates
sustained re-engagement rather than only short-term activity.

---

### Secondary KPIs

#### D1 Post-Return Retention

Measures immediate re-engagement after returning.

#### Sessions per Player

Measures whether the feature increases gameplay frequency.

#### Playtime per Player

Measures overall engagement depth.

#### Levels Completed

Measures progression activity after returning.

#### Journey Completion Rate

Measures direct engagement with the comeback feature.

#### Mission Completion Rate

Identifies friction within individual stages.

---

## 7. Guardrail Metrics

Improved retention should not automatically be considered successful if it
creates negative effects elsewhere in the product.

The experiment should therefore monitor:

### Conversion Rate

Percentage of players making at least one purchase.

### ARPU

Average Revenue per User.

### Booster Usage per Level

Helps detect whether players require more resources to progress.

### Failures per Level

Helps detect unintended difficulty changes.

### Progression Speed

Helps identify whether rewards accelerate progression beyond intended levels.

---

## 8. Key Analysis Cuts

Experiment results should be evaluated at the overall level first.

Secondary analysis can then explore:

### By Player Segment

- Struggling
- Casual
- Engaged

Question:

> Does personalization provide similar value across behavioral segments?

### By Platform

- iOS
- Android

Question:

> Does the feature behave differently across platforms?

### By Inactivity Duration

Example groups:

- 3–5 days
- 6–10 days
- 11+ days

Question:

> Does comeback effectiveness change depending on how long the player was inactive?

### By Journey Stage

Analyze completion rates from Mission 1 through the final mission.

Question:

> Where does the largest player drop-off occur?

---

## 9. Example Product Dashboard

A product dashboard for the feature could contain:

### Experiment Overview

- Eligible Players
- Exposed Players
- Journey Starts
- Journey Completions
- D1 Retention
- D7 Retention

### Funnel

```text
Eligible
   ↓
Exposed
   ↓
Started
   ↓
Mission 1
   ↓
Mission 2
   ↓
Mission 3
   ↓
Completed
```

### Experiment Comparison

| Metric | Control | Generic | Adaptive |
|---|---:|---:|---:|
| D1 Retention | — | — | — |
| D7 Retention | — | — | — |
| Sessions / Player | — | — | — |
| Levels Completed | — | — | — |
| Conversion Rate | — | — | — |
| ARPU | — | — | — |

Values are intentionally left blank because this case study does not use
fabricated experiment results.

---

## 10. Example Product Questions

The tracking system should allow the product team to answer questions such as:

- Does Adaptive Comeback improve D7 retention compared with Control?
- Does personalization outperform the Generic Comeback Journey?
- Which behavioral segment benefits most from the feature?
- At which mission stage do players drop off?
- Do players who complete the journey remain more engaged afterward?
- Does reward claiming influence continued gameplay?
- Does the feature negatively affect conversion or ARPU?
- Does the feature increase booster dependency?
- Are longer-inactive players harder to re-engage?
- Is the additional complexity of personalization justified by incremental player value?

---

## 11. Tracking Quality Considerations

### Stable Experiment Assignment

A player should remain in the same experiment group throughout the experiment.

### Unique Journey Identification

Each Comeback Journey should have a unique `journey_id` so repeated experiences
can be analyzed separately.

### Event Deduplication

Events such as reward claiming and journey completion should not be recorded
multiple times because of retries or connection problems.

### Server-Side Validation

Critical events such as reward claims should be validated server-side where
possible.

### Consistent Timestamps

Event timestamps should use a consistent timezone and format.

### Missing Data Monitoring

The analytics pipeline should monitor unexpected missing values for important
properties such as:

- experiment_group
- player_segment
- journey_type
- mission_id

---

## 12. Scope Note

This tracking plan is a conceptual analytics specification created for a
portfolio product case study.

Event names, properties, segmentation logic, and metrics are illustrative.

In a production environment, the final tracking implementation would require
collaboration between Product, Game Design, Engineering, Data, and Analytics
teams and validation against the game's existing analytics architecture.
