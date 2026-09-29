# Adaptive Comeback Journey — Product Specification

## 1. Objective

Design a personalized re-engagement experience for mobile puzzle game players returning after a period of inactivity.

The feature should help returning players re-enter the core gameplay loop while avoiding unnecessary disruption to monetization, progression, and game economy.

The first version intentionally uses simple and explainable behavioral segmentation rather than complex personalization models.

---

## 2. Target User

The feature targets players returning after at least **3 consecutive days of inactivity**.

A player must also:

- Have sufficient historical gameplay data for segmentation
- Not have received another Comeback Journey within the previous 30 days
- Be eligible for the active experiment population

Players without sufficient behavioral history should fall back to the **Generic Comeback Journey** rather than being assigned to an unreliable behavioral segment.

---

## 3. Functional Requirements

### FR-01 — Eligibility Check

When a player launches the game, the system should determine whether the player meets the inactivity and cooldown requirements.

If the player is not eligible, the normal game experience should continue without displaying the Comeback Journey.

### FR-02 — Behavioral Classification

For eligible players, recent gameplay behavior should be evaluated using signals such as:

- Session frequency
- Total playtime
- Level progression
- Failures per level
- Booster usage per level
- Recent activity consistency

The player should then be assigned to one of three behavioral paths:

- **Momentum Path** — Struggling Players
- **Quick Comeback** — Casual Players
- **Streak Challenge** — Engaged Players

Exact classification thresholds would need to be calibrated using real player distributions.

### FR-03 — Journey Assignment

The assigned journey should remain fixed for the duration of the active Comeback Journey.

A player should not move between behavioral segments while a journey is already active.

### FR-04 — Mission Progress

Mission progress should update automatically through normal gameplay.

The player should not need to enter a separate game mode to complete comeback missions.

### FR-05 — Progressive Rewards

Rewards should unlock only after the corresponding mission requirement has been completed.

Rewards should not be granted simply because the player returned to the game.

The intended loop is:

**Return → Play → Progress → Earn Reward → Continue Playing**

### FR-06 — Reward Claiming

When a mission is completed, its reward becomes claimable.

Claimed rewards should be delivered immediately and the claim status should be stored at the player-account level.

### FR-07 — Journey Completion

The journey should be marked as completed when the player finishes the final mission and becomes eligible to claim the final reward.

Journey completion should be tracked separately from individual mission completion.

### FR-08 — Expiration

A Comeback Journey should remain available for a limited period.

For this case study, the proposed duration is **7 days after activation**.

Unclaimed rewards should expire when the journey expires.

### FR-09 — Cooldown

After receiving a Comeback Journey, the player should not become eligible for another one for **30 days**.

This rule is intended to reduce repeated reward exploitation and intentional inactivity.

---

## 4. Journey Configuration

| Player Segment | Assigned Journey | Primary Design Goal |
|---|---|---|
| Struggling | Momentum Path | Reduce progression friction and rebuild confidence |
| Casual | Quick Comeback | Encourage low-friction re-entry |
| Engaged | Streak Challenge | Restore gameplay momentum through challenge |

Mission requirements and reward values should be configurable without requiring changes to the underlying feature logic.

---

## 5. Journey Mechanics

### Momentum Path

Designed for players who showed signs of progression difficulty before becoming inactive.

**Example mission structure:**

1. Complete 2 levels  
   → 15 Minutes Unlimited Lives

2. Complete 3 additional levels  
   → 1 Rocket + 1 Bomb

3. Complete 6 total levels  
   → Momentum Chest

**Design intention:** Help the player regain progression momentum without simply granting a large login reward.

---

### Quick Comeback

Designed for players with relatively low historical session frequency or playtime.

**Example mission structure:**

1. Complete 1 level  
   → Small Coin Reward

2. Complete 3 total levels  
   → 1 Booster

3. Complete 5 total levels  
   → Comeback Chest

**Design intention:** Create an immediate sense of progress while keeping the commitment requirement low.

---

### Streak Challenge

Designed for previously engaged players who showed consistent gameplay before becoming inactive.

**Example mission structure:**

1. Complete 3 levels  
   → Booster Reward

2. Complete 7 total levels  
   → Advanced Booster Bundle

3. Complete 12 total levels  
   → Premium Comeback Chest

**Design intention:** Restore gameplay momentum through a more challenging progression path.

> Reward quantities in this case study are illustrative. Production values would require balancing against real game economy, progression, and monetization data.

---

## 6. Core System Logic

```text
PLAYER OPENS GAME
        |
        v
Inactive for 3+ days?
     /       \
   NO         YES
   |           |
Normal      Cooldown passed?
Game          /       \
             NO       YES
             |          |
          Normal     Enough behavioral data?
           Game        /             \
                      NO             YES
                      |               |
                   Generic       Classify Player
                   Journey       /      |       \
                           Struggling  Casual  Engaged
                               |         |        |
                           Momentum    Quick    Streak
                             Path     Comeback  Challenge
                               \         |        /
                                \        |       /
                                 v       v      v
                                   GAMEPLAY
                                      |
                                      v
                               Mission Progress
                                      |
                                      v
                              Progressive Rewards
                                      |
                                      v
                              Journey Completed
```

---

## 7. Experiment Behavior

The feature should support three experiment experiences:

### Control

The player receives the existing returning-player experience without a dedicated Comeback Journey.

### Treatment A — Generic Comeback

All eligible players receive the same Comeback Journey regardless of historical behavior.

### Treatment B — Adaptive Comeback

Eligible players receive a journey based on their behavioral segment.

Experiment assignment should be persistent for the experiment period.

A player's experiment group should not change between sessions.

---

## 8. Edge Cases

### Player becomes inactive during an active journey

The existing journey remains active until its expiration date.

A new journey should not be generated.

### Player returns but has insufficient historical data

Assign the **Generic Comeback Journey** rather than forcing an unreliable behavioral classification.

### Player qualifies for multiple behavioral segments

A predefined classification priority or scoring rule should resolve overlapping signals.

The final production rule would require validation using real player data.

### Player completes a mission but closes the game before claiming the reward

Mission completion should be persisted.

The reward should remain claimable until the journey expires.

### Player closes the game during mission progress

Progress should be saved and restored during the player's next session.

### Player changes device

Journey state, experiment assignment, mission progress, and claimed rewards should be stored at the player-account level rather than only on the local device.

### Player loses connection while claiming a reward

Reward delivery should be idempotent so that reconnecting does not create duplicate rewards.

### Player completes the final mission

The journey should be marked as completed, but the final reward should remain claimable until expiration if it has not yet been collected.

### Experiment assignment changes

Experiment assignment should remain stable for the full experiment period to avoid contamination between Control and Treatment experiences.

---

## 9. Product Safeguards

### Intentional Inactivity

Players may discover that inactivity makes them eligible for comeback rewards.

The 30-day cooldown and controlled reward values are intended to reduce this incentive.

### Over-Rewarding

Comeback rewards should complement normal progression rather than outperform rewards available through regular gameplay.

Reward balancing should consider:

- Normal progression rewards
- Booster consumption
- Purchase behavior
- Player progression speed
- Game economy inflation

### Incorrect Segmentation

A player may be assigned to an experience that does not match their actual motivation.

Segment-level mission completion and retention should therefore be monitored during experimentation.

### Feature Fatigue

Repeated exposure could reduce the perceived value of the feature.

Eligibility frequency and repeat-player behavior should be monitored before expanding the feature.

---

## 10. Non-Goals

The first version does not attempt to:

- Predict individual churn probability using machine learning
- Generate missions dynamically with AI
- Personalize every reward at an individual-player level
- Replace the game's existing progression system
- Optimize the entire game economy
- Create a separate gameplay mode
- Determine why an individual player originally stopped playing

The first version intentionally uses explainable behavioral segmentation to test whether personalization creates enough incremental value before introducing additional complexity.

---

## 11. Product Success Requirements

The feature should ultimately be evaluated using the experiment framework defined in the main case study.

The primary success metric is:

**D7 Post-Return Retention**

Supporting engagement metrics include:

- D1 post-return retention
- Sessions per player
- Playtime per player
- Levels completed
- Mission completion rate
- Journey completion rate

Guardrails include:

- Conversion rate
- ARPU
- Booster usage per level
- Failures per level
- Progression speed

A successful result should demonstrate meaningful retention or engagement improvement without unacceptable deterioration in monetization, progression, or game balance.

---

## 12. Open Questions

Before production implementation, the team would need to determine:

- What inactivity threshold best identifies meaningful returning players?
- How should behavioral segmentation thresholds be calibrated?
- Which historical time window should be used for player classification?
- What reward values are sustainable within the live game economy?
- Is a 7-day journey duration appropriate?
- Is a 30-day cooldown sufficient to prevent undesirable behavior?
- How should overlapping behavioral signals be prioritized?
- How should players with very limited historical data be handled?
- Does personalization provide enough incremental value over a generic comeback system to justify its technical and operational complexity?

---

## 13. Scope Note

This specification is part of a conceptual mobile game product case study.

The segmentation rules, mission requirements, reward values, inactivity threshold, cooldown period, and expiration rules are illustrative product assumptions.

In a live game environment, these parameters would require validation using real player behavior, game economy data, technical constraints, and controlled experimentation.
