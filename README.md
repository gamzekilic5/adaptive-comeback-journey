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

### ⚡ Quick Comeback — Casual Players

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
