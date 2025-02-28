---
icon: gear-code
description: Configuration
---

# DailyRewardsConfiguration

Configuration for DailyRewards. Stores reward types,  display names, etc.

## Part of [daily-rewards-system.md](../../../../systems/systems/rewards/daily-rewards-system.md "mention")

## Configuration Description:

Stores information about 7 rewards (for each day) that includes reward type, display name and amount/item id. Each reward can be represented by this format:

```lua
[dayID:number] = {
		RewardText = text:string,
		RewardType = text:string, --type*
		RewardAmount or RewardItemID = n:number
},
```

**RewardText** - display name of reward, text that is displayed on GUI reward title

**RewardType** - type of the reward. Can be: "**Currency**" or "**Item**". New types may be added in the future.

**RewardAmount/RewardItemID** - the key depends on **RewardType**. If _**Currency**_ use **RewardAmount** if _**Item**_ use **RewardItemID**. Both are numbers where **RewardAmount** represents quantity of currency gained and **RewardItemID** the id of the item.
