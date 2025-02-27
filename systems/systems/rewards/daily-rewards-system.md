---
description: System
---

# Daily Rewards System

System responsible for giving player a reward once a day. Used for encouraging player to return for the reward the following day.

## Current functions are:

* Keep track of claimed rewards
* Give rewards to player once claimed
* Keep track of last time

## Configuration

[dailyrewardsconfiguration.md](../../../replicatedstorage-scripts/replicatedstorage/scripts/configuration/dailyrewardsconfiguration.md "mention") - Location:

`ReplicatedStorage/Scripts/Configuration/DailyRewardsConfiguration`

## Scripts and components:

* [dailyrewardsmanager.md](../../../server-scripts/serverscriptservice/rewards/dailyrewardsmanager.md "mention") - Location: `ServerScriptService/Rewards/DailyRewardsManager`
* [rewardinfoupdater.md](../../../ui-scripts/startergui/rewards/rewardinfoupdater.md "mention") - Location: `GUI/Rewards/RewardInfoUpdater`
* [rewards](../../../ui-scripts/startergui/rewards/ "mention") (GUI) - Location: `GUI/Rewards`
* [dailyrewards.md](../../../datastores/datastores/dailyrewards.md "mention") (Datastore) - Location: -
* [canclaimrewards.md](../../../replicatedstorage-scripts/replicatedstorage/events/dailyrewards/canclaimrewards.md "mention")(Event) - Location: `ReplicatedStorage/Events/DailyRewards/CanClaimRewards`
* &#x20;[claim.md](../../../replicatedstorage-scripts/replicatedstorage/events/dailyrewards/claim.md "mention")(Event) - Location: `ReplicatedStorage/Events/DailyReward/Claim`
* &#x20;[getrewardstatus.md](../../../replicatedstorage-scripts/replicatedstorage/events/dailyrewards/getrewardstatus.md "mention")(Event) - Location: `ReplicatedStorage/Events/DailyRewards/GetRewardStatus`
* [updaterewards.md](../../../replicatedstorage-scripts/replicatedstorage/events/dailyrewards/updaterewards.md "mention")(Event) - Location: `ReplicatedStorage/Events/DailyRewards/UpdateRewards`



## Interactions and functions

*   DailyRewardsManager (Server Side) - responsible for :&#x20;

    * Managing datastore (Saving\&Loading data)
    * Verify claim permission (whether player can claim or cannot claim specific reward)
    * Updating claim permissions (live)
    * Responding to client requests (mainly events)


* RewardInfoUpdater (Client Side) - responsible for:
  * Updating GUI with reward info

### Interactions:

* (_A --< A) - interaction of side with itself. Where A is server or client._
* _(A --> B) - interaction of 2 sides with one another. Where A is server or client and B is oposite side._
* _(A <— B) - interaction where B affects A (e.g. what happens when received request/response, a 'push for action' by B)_

**DailyRewardsManager <---> RewardInfoUpdater**

1. When player joins the information is being loaded from datastore by `DailyRewardsManager` script _(S --< S)_
2. In heartbeat loop `DailyRewardsManager` checks the reward statuses for each player. _(S --< S)_
3. `RewardInfoUpdater`once initialized requests information about player ability to claim rewards (in general) from the server by using `CanClaimRewards` event. _(C --> S)_
4. `RewardInfoUpdater`once received response from `CanClaimRewards` _(C <— S),_ it sets button status accordingly and updates reward status for each ["Reard Box"](#user-content-fn-1)[^1] by requesting info about each day by firing the `RewardStatusRequest` event. _(C --> S)_
5. `DailyRewardManager`

will be updated soon



[^1]: Unit of daily reward. Encased block that contains: image, name and day of the reward. (UI element)
