---
description: Event (Remote)
icon: rocket-launch
---

# GetRewardStatus

Event made for client to request server the data about specific reward's status.

## Part of [daily-rewards-system.md](../../../../systems/systems/rewards/daily-rewards-system.md "mention")

### Data from Client:

* `rewardID:number` - id of the reward. (It is ID of day assigned for the reward. From 1 to 7)

### Data from server:

* `rewardStatus:boolean` - represents the reward status. True = Claimed, False = Not claimed.
