---
icon: scroll
description: Script (Local)
---

# RewardInfoUpdater

Manages [.](./ "mention") GUI.

## Part of [daily-rewards-system.md](../../../systems/systems/rewards/daily-rewards-system.md "mention")

## Services and Dependencies

* [dailyrewardsconfiguration.md](../../../replicatedstorage-scripts/replicatedstorage/scripts/configuration/dailyrewardsconfiguration.md "mention")
* [canclaimrewards.md](../../../replicatedstorage-scripts/replicatedstorage/events/dailyrewards/canclaimrewards.md "mention") (event)
* [claim.md](../../../replicatedstorage-scripts/replicatedstorage/events/dailyrewards/claim.md "mention") (event)
* [getrewardstatus.md](../../../replicatedstorage-scripts/replicatedstorage/events/dailyrewards/getrewardstatus.md "mention") (event)
* [updaterewards.md](../../../replicatedstorage-scripts/replicatedstorage/events/dailyrewards/updaterewards.md "mention") (event)
* [UI elements](rewardinfoupdater.md#ui-references)



## Variables

* `canClaimReward:boolean`  - indicates wheather player can or cannot claim rewards
* `rewardList` - stores list of Frames that represent rewards in GUI.

## UI References

```lua
local rewardsFrame = script.Parent.RewardsFrame.RewardsFrameTop
local claimButton = rewardsFrame.Claim.Click
local closeButton = rewardsFrame.Close.Click
local openButton = script.Parent.RewardsButton.Click
```

More information about UI elements: [.](./ "mention")

## Functions

* `getRewardList()`&#x20;

Iterates through chilred of `rewardsFrame.Rewards` and saves them into a table if their class type is `Frame`. Returns table.

```lua
local function getRewardList()
	local rewards = {}
	
	for _, item in rewardsFrame.Rewards:GetChildren() do
		if item:IsA("Frame") then
			table.insert(rewards, item)
		end
	end
	
	return rewards
end
```

* `updateRewardUI()`&#x20;

Iterates through `rewardList` provided by `getRewardList()` function, fires `GetRewardStatus` event for each reward ID. And changes reward label to text provided by [dailyrewardsconfiguration.md](../../../replicatedstorage-scripts/replicatedstorage/scripts/configuration/dailyrewardsconfiguration.md "mention")

## Event handling

* `GetRewardStatus` event sets visibility of "Claimed" overlay based on server response.

```lua
-- Handle reward status response
rewardStatusRequest.OnClientEvent:Connect(function(rewardID, rewardStatus)
	for id, rewardItem in rewardsList do
		if id == rewardID then
			rewardItem.Claimed.Visible = not rewardStatus 
		end
	end
end)
```

* `claimButton.MouseButton1Click` - fires [claim.md](../../../replicatedstorage-scripts/replicatedstorage/events/dailyrewards/claim.md "mention") event
* `closeButton.MouseButton1Click` - sets visibility of main rewardsFrame to false
* `openButton.MouseButton1Click` - sets visibility of main rewardsFrame to true
* `UpdateRewards` - fires [canclaimrewards.md](../../../replicatedstorage-scripts/replicatedstorage/events/dailyrewards/canclaimrewards.md "mention")
* `CanClaimRewards` - Sets `canClaimReward` variable to recieved status, sets claimButton visibility to recieved status, calls `updateRewardUI()` function.

```lua
canClaimRewardsRequest.OnClientEvent:Connect(function(status)
	canClaimReward = status
	claimButton.Visible = status -- Show claim button only if reward can be claimed
	updateRewardUI()
end)
```
