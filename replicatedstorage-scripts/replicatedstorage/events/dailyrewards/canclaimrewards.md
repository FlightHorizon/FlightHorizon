---
description: Event (Remote)
icon: rocket-launch
---

# CanClaimRewards

Remote event made for Client to request the DailyReward claim permission. (Is used to know if player has permission to claim reward **in general** not for specific rewards)

## Part of [daily-rewards-system.md](../../../../systems/systems/rewards/daily-rewards-system.md "mention")

### Data from client side:

* none

### Data from Server

* `canClaim:boolean` - whether player has permission to claim or not for the current time.
