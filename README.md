# Adaptive Comeback Journey

### Mobile Game Feature Design & Product Case Study

A product case study exploring how a mobile puzzle game could re-engage returning
players through personalized missions, progressive rewards, and adaptive gameplay
experiences.

## Product Problem

Getting an inactive player to reopen a game does not necessarily mean that the
player has been successfully re-engaged.

Some returning players may collect a reward, play briefly, and leave again.

The product challenge is:

> **How can we help returning players re-enter the core gameplay loop and remain
> engaged after they come back?**

## Product Hypothesis

Returning players have different reasons for disengaging and different gameplay
behaviors.

Instead of providing the same comeback reward to every player, adapting the
comeback experience to previous player behavior may create a more relevant and
engaging return experience.

### Hypothesis

> **A personalized, progression-based comeback journey will increase post-return
> engagement and retention compared with a generic comeback experience.**

## Player Segmentation

The Adaptive Comeback Journey does not treat every returning player in the same way.

Players are segmented using their gameplay behavior before becoming inactive.
The purpose is not to permanently label players, but to determine which comeback
experience may be most relevant at the time of their return.

### 1. Struggling Players

Players who were active but showed signs of difficulty progressing before becoming inactive.

**Behavioral signals may include:**
- High failures per level
- Repeated attempts on the same progression stage
- Slower level progression
- Higher booster dependency

**Comeback objective:** Reduce friction and help the player regain momentum.

---

### 2. Casual Players

Players who interacted with the game but showed relatively low engagement before becoming inactive.

**Behavioral signals may include:**
- Low session frequency
- Short playtime
- Limited level progression
- Irregular activity

**Comeback objective:** Create a low-friction reason to start playing again without overwhelming the player.

---

### 3. Engaged Players

Players who showed strong engagement and progression before unexpectedly becoming inactive.

**Behavioral signals may include:**
- High session frequency
- Higher playtime
- Consistent level progression
- Regular gameplay activity

**Comeback objective:** Restore the player's previous gameplay momentum and provide a meaningful challenge.

## Adaptive Comeback Experience

When an eligible player returns after at least 3 days of inactivity, the system
selects a comeback journey based on the player's recent gameplay behavior.

Each journey follows the same principle:

**Return → Complete Missions → Build Momentum → Unlock Progressive Rewards**

However, mission design changes according to the player's previous behavior.

### Momentum Path — Struggling Players

Designed for players who showed signs of progression difficulty before becoming inactive.

**Mission Flow**

1. Complete 2 levels  
   → 15 Minutes Unlimited Lives

2. Complete 3 additional levels  
   → 1 Rocket + 1 Bomb

3. Complete 6 total levels  
   → Momentum Chest

**Design Goal:** Reduce initial friction and help the player experience successful
progression shortly after returning.

---

### Quick Comeback — Casual Players

Designed as a short, low-commitment experience for players with historically
lower session frequency or playtime.

**Mission Flow**

1. Complete 1 level  
   → Small Coin Reward

2. Complete 3 total levels  
   → 1 Booster

3. Complete 5 total levels  
   → Comeback Chest

**Design Goal:** Provide an immediate sense of progress without requiring a long
play session.

---

### Streak Challenge — Engaged Players

Designed for previously engaged players who may respond better to challenge and
progression than to simple login rewards.

**Mission Flow**

1. Complete 3 levels  
   → Booster Reward

2. Complete 7 total levels  
   → Advanced Booster Bundle

3. Complete 12 total levels  
   → Premium Comeback Chest

**Design Goal:** Rebuild gameplay momentum through a more demanding progression
path and a stronger final reward.

---

## Reward Design Principle

Rewards are earned through gameplay rather than granted immediately when the
player returns.

This creates the following loop:

**Come Back → Play → Progress → Earn Reward → Continue Playing**

The feature is designed to support the core gameplay loop rather than replacing
it with passive login rewards.

Reward values shown in this case study are illustrative and would require
balancing using live game economy data before implementation.

## Eligibility & Abuse Prevention

A comeback system can unintentionally encourage players to become inactive if
rewards are perceived as more valuable than regular gameplay rewards.

To reduce this risk, the feature includes several eligibility rules.

### Eligibility

A player becomes eligible when:

- The player has been inactive for at least 3 consecutive days
- The player has sufficient historical gameplay data for behavioral segmentation
- The player has not received another Comeback Journey within the cooldown period

### Cooldown

The Adaptive Comeback Journey can be activated at most once every **30 days**.

This reduces the incentive for players to intentionally stop playing in order
to repeatedly obtain comeback rewards.

### Reward Safeguards

Comeback rewards should complement normal progression rather than outperform
rewards available through regular gameplay.

Reward values should therefore be monitored and balanced against:

- Normal progression rewards
- Booster consumption
- In-game economy
- Purchase behavior
- Player progression speed

### Additional Product Risks

**Intentional inactivity**  
Players may learn the eligibility rules and deliberately become inactive.

**Over-rewarding**  
Excessive comeback rewards could reduce purchase incentives or disrupt the game economy.

**Over-segmentation**  
Incorrect behavioral classification could provide an experience that does not
match the player's actual motivation.

**Feature fatigue**  
Repeated exposure could make the comeback experience feel routine rather than special.

## Experiment Design

The Adaptive Comeback Journey should be validated through a controlled experiment
before a full rollout.

Rather than testing personalization only against the existing experience, the
experiment includes a generic comeback treatment as an additional comparison group.

### Experiment Groups

**Control — Current Experience**

Returning players receive the existing game experience without a dedicated
comeback journey.

**Treatment A — Generic Comeback Journey**

Eligible returning players receive the same comeback mission structure and
rewards regardless of their previous gameplay behavior.

**Treatment B — Adaptive Comeback Journey**

Eligible returning players receive a comeback journey based on their behavioral
segment:

- Struggling → Momentum Path
- Casual → Quick Comeback
- Engaged → Streak Challenge

### Core Experiment Question

> **Does an adaptive comeback experience create incremental value beyond both
> the current experience and a generic comeback feature?**

### Randomization

Eligible returning players would be randomly assigned to one of the three
experiment groups.

Randomization should occur after eligibility is determined to ensure that all
groups are drawn from the same target population.

### Primary Metric

**D7 Post-Return Retention**

The percentage of returning players who are active again seven days after
entering the experiment.

### Secondary Metrics

- D1 post-return retention
- Sessions per player
- Playtime per player
- Levels completed
- Comeback Journey completion rate
- Mission completion rate

### Guardrail Metrics

- Conversion rate
- ARPU
- Booster usage per level
- Failures per level
- Progression speed

These metrics help identify whether an engagement improvement comes at the cost
of monetization, game balance, or player experience.

## Success Criteria & Decision Framework

The experiment should not be evaluated only by whether a result reaches
statistical significance. The magnitude of the improvement and its impact on
player experience, monetization, and game balance should also be considered.

### Decision Framework

**Scenario 1 — Adaptive Journey outperforms both Control and Generic**

If Treatment B produces a meaningful improvement in D7 post-return retention
without deterioration in guardrail metrics:

→ Proceed with a gradual rollout of the Adaptive Comeback Journey.

---

**Scenario 2 — Generic and Adaptive perform similarly**

If both treatments improve retention but personalization provides little or no
incremental value:

→ Prefer the Generic Comeback Journey.

A simpler solution may be preferable if personalization adds implementation
complexity without sufficient additional player value.

---

**Scenario 3 — Engagement improves but guardrails deteriorate**

If retention or engagement increases while monetization, progression balance,
or other important guardrails deteriorate:

→ Do not immediately roll out the feature.

Investigate the reward structure and identify the mechanism behind the negative
effect before running another iteration.

---

**Scenario 4 — No meaningful improvement**

If neither treatment produces a meaningful improvement:

→ Do not roll out the feature in its current form.

Use mission completion, segment-level behavior, and progression data to identify
where players disengage and redesign the experience.

---

## Future Iterations

If the initial experiment demonstrates product value, future iterations could explore:

- Different inactivity thresholds
- Alternative mission difficulty curves
- Dynamic reward values
- Different numbers of comeback stages
- Segment-specific reward types
- Personalized mission duration
- Long-term D14 and D30 retention effects
- Impact on player lifetime value
- More granular behavioral segmentation

More advanced personalization should only be introduced if simpler segmentation
demonstrates sufficient incremental value to justify the added complexity.

---

## Case Study Scope

This is a conceptual product case study created for portfolio purposes.

The player segments, reward values, eligibility thresholds, and experiment
design are illustrative assumptions. In a live product environment, these
decisions would require validation using real player behavior, game economy,
and experimentation data.
