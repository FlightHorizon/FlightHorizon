---
icon: scroll
description: Script
---

# DailyRewardsManager

Script for managing daily rewards on server side.

## Part of [daily-rewards-system.md](../../../systems/systems/rewards/daily-rewards-system.md "mention")

## Services and Dependencies

* `DataStoreService`
* `RunService`
* [dailyrewardsconfiguration.md](../../../replicatedstorage-scripts/replicatedstorage/scripts/configuration/dailyrewardsconfiguration.md "mention")
* [canclaimrewards.md](../../../replicatedstorage-scripts/replicatedstorage/events/dailyrewards/canclaimrewards.md "mention") (event)
* [claim.md](../../../replicatedstorage-scripts/replicatedstorage/events/dailyrewards/claim.md "mention") (event)
* [getrewardstatus.md](../../../replicatedstorage-scripts/replicatedstorage/events/dailyrewards/getrewardstatus.md "mention") (event)
* [updaterewards.md](../../../replicatedstorage-scripts/replicatedstorage/events/dailyrewards/updaterewards.md "mention") (event)
* [dailyrewards.md](../../../datastores/datastores/dailyrewards.md "mention") (datastore)

## Variables

* `playerRewardInfo:dict`  stores current info about player rewards. Format: `[player:Player] = {LastReward:number, LastRewardTime:number}`

## Functions

* `fetchPlayerInfo(player: Player)`

Function that loads player reward info from datastore to  `playerRewardInfo` dictionary. Returns `nil`

* `savePlayerInfo(player: Player)`

Function that saves player data from `playerRewardInfo` to datastore. Returns `nil`

* `playerCanClaim(player: Player) : boolean`

Function that checks player's permission to claim reward at the moment based on data stored in `playerRewardInfo.LastRewardTime` . Returns `boolean`.

* `claimPlayersReward(player:Player)`

Function uses `playerCanClaim` to verify the permission of the player to claim the reward.  If player can claim reward then it gives player the reward and sets `playerRewardInfo.LastReward` to reward's id. Then it fires `UpdateRewardsEvent`  to update client's GUI.

## Event handling

* `game.Players.PlayerAdded` runs `fetchPlayerInfo()` .
* `game.Players.PlayerRemoving` runs `savePlayerInfo()` .
* `RunService.Heartbeat` event updates player GUI in real time.

{% code fullWidth="false" %}
```lua
runService.Heartbeat:Connect(function(deltaTime: number) 
	for _, plr in pairs(players:GetPlayers()) do
		local canClaim = playerCanClaim(plr)
		
		if canClaim then
			updateRewardsEvent:FireClient(plr)
		end
	end	
end)
```
{% endcode %}

* `CanClaimRewards` event fires `playerCanClaim()` output back to client.
* `Claim` event runs `claimPlayersReward()` function.
* `RewardStatusRequest` runs logic that checks if reward with specified ID has already been claimed by player or not.

{% code fullWidth="false" %}
```lua
rewardStatusRequest.OnServerEvent:Connect(function(player: Player, rewardID:number)
	local rewardData = playerRewardInfo[player]
	local lastReward = rewardData.LastReward
	local rewardStatus = false -- true - can be claimed, false - cannot be claimed
	
	if rewardID > lastReward then
		rewardStatus = true
	end
	
	rewardStatusRequest:FireClient(player, rewardID, rewardStatus)
end)
```
{% endcode %}
