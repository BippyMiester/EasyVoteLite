# NEW UPDATE

The plugin has been completely rewritten for performance in mind! Due to the fact that this plugin has been renamed, you don't have to delete your config/data/lang files but you should migrate the data over and then delete them to save on server space.

**THIS PLUGIN IS IN BETA STAGES RIGHT NOW! BE SURE TO TEST THIS PLUGIN ON A TEST SERVER FIRST!**

## New Features

- Ability to control when a player gets notified that they have unclaimed votes/need to vote
- Discord Messages plugin is no longer required to send discord webhooks
- Rewards are now strictly command based. No more commands section in the config. Just put in your command in the reward section and you're off!
- You can now change the description for each reward whenever a player runs the /rewardlist command
- Added useful command line command to check players vote count, reset their vote count and more
- Added an option to reset a players vote count whenever a map wipes
- Added useful debug options for easier debugging
- Ability to add as many reward tiers as you want! All you have to do is change the number under rewards to the amount of votes a player needs for those rewards to be given. I.e. vote3 in the previous config is now just 3, vote6 in the previous config is now just 6
  No more permissions system. Why on earth would you not want a player to vote for your server?!?!?

## What is EasyVote Pro?

I'll be releasing EasyVote Pro at a later date, but the expected features in EasyVote Pro that EasyVote Lite doesn't have are:

- Discord embeds instead of just straight text messages
- Dedicated Support section
- More voting sites! You can add a support ticket and i'll be happy to add the site of your choice! Currently there are 2 new voting sites being added (top-serveurs.net & servertilt.com)
- Custom Status Frames integration
- Notify Integrations

## General Features

Players receive a reward every time they vote successfully. You can edit the available rewards in the configuration file.

Add custom reward based how many time player has voted. You can add many as you like custom rewards, there is no limits.

Supports Rust-Servers.net, RustServers.info and BestServers.com

Global Announcement - Alert to every player in server. Who and how many time player has voted.

Discord Announcement - Alert to every player in server. Who and how many time player has voted.

And much more!

## Variables

Use the below replacement variables when creating your rewards.

`{playername}` -- player's display name
`{playerid}` -- player's Steam ID

## Chat Commands

**/vote** -- Show vote link(s)
**/claim** -- Claim vote reward(s)
**/rewardlist** -- Display what reward(s) can get

## Console Commands

`clearvote <steamID>` - Clears a players vote count to 0

`checkvote <steamID>` - Check the players current vote count

`setvote <steamID> <number>` - Set the players vote count to a specific number

`resetvotedata` - Resets all voting data for every player

## Plugin API Hooks

```c#
// Returns an int value of the number of votes a player has
(int) getPlayerVotes(string steamID)
```

## **Configuration**

The settings and options for this plugin can be configured in the EasyVoteLite.json file in the config directory. The use of a JSON editor or validation site such as jsonlint.com is recommended to avoid formatting issues and syntax errors.

```json
{
  "Debug Settings": {
    "Debug Enabled?": "false",
    "Enable Verbose Debugging? (READ DOCUMENTATION FIRST!)": "false",
    "Set Check API Response Code (0 = Not found, 1 = Has voted and not claimed, 2 = Has voted and claimed)": "0",
    "Set Claim API Response Code (0 = Not found, 1 = Has voted and not claimed. The vote will now be set as claimed., 2 = Has voted and claimed": "0"
  },
  "Plugin Settings": {
    "Enable logging => logs/EasyVote (true / false)": "true",
    "Wipe Rewards Count on Map Wipe?": "true",
    "Vote rewards cumulative (true / false)": "false",
    "Chat Prefix": "<color=#e67e22>[EasyVote]</color> "
  },
  "Notification Settings": {
    "Globally announcment in chat when player voted (true / false)": "true",
    "Enable the 'Please Wait' message when checking voting status?": "true",
    "Notify player of rewards when they stop sleeping?": "false",
    "Notify player of rewards when they connect to the server?": "true"
  },
  "Discord": {
    "Discord webhook (URL)": "https://support.discord.com/hc/en-us/articles/228383668-Intro-to-Webhooks",
    "DiscordMessage Enabled (true / false)": "false",
    "Discord Title": "A player has just voted for us!"
  },
  "Rewards": {
    "@": [
      "giveto {playerid} supply.signal 1"
    ],
    "first": [
      "giveto {playerid} stones 10000",
      "sr add {playerid} 10000"
    ],
    "3": [
      "addgroup {playerid} vip 7d"
    ],
    "6": [
      "grantperm {playerid} plugin.test 1d"
    ],
    "10": [
      "zl.lvl {playerid} * 2"
    ]
  },
  "Reward Descriptions": {
    "@": "Every Vote: 1 Supply Signal",
    "first": "First Vote: 10000 Stones, 10000 RP",
    "3": "3rd Vote: 7 days of VIP rank",
    "6": "6th Vote: 1 day of plugin.test permission",
    "10": "10th Vote: 2 zLevels in Every Category"
  },
  "Server Voting IDs and Keys": {
    "ServerName1": {
      "Rust-Servers.net": "ID:KEY",
      "Rustservers.gg": "ID:KEY",
      "BestServers.com": "ID:KEY"
    },
    "ServerName2": {
      "Rust-Servers.net": "ID:KEY",
      "Rustservers.gg": "ID:KEY",
      "BestServers.com": "ID:KEY"
    }
  },
  "Voting Sites API Information": {
    "Rust-Servers.net": {
      "API Claim Reward (GET URL)": "http://rust-servers.net/api/?action=custom&object=plugin&element=reward&key={0}&steamid={1}",
      "API Vote status (GET URL)": "http://rust-servers.net/api/?object=votes&element=claim&key={0}&steamid={1}",
      "Vote link (URL)": "http://rust-servers.net/server/{0}",
      "Site Uses Username Instead of Player Steam ID?": "false"
    },
    "Rustservers.gg": {
      "API Claim Reward (GET URL)": "https://rustservers.gg/vote-api.php?action=claim&key={0}&server={2}&steamid={1}",
      "API Vote status (GET URL)": "https://rustservers.gg/vote-api.php?action=status&key={0}&server={2}&steamid={1}",
      "Vote link (URL)": "https://rustservers.gg/server/{0}",
      "Site Uses Username Instead of Player Steam ID?": "false"
    },
    "BestServers.com": {
      "API Claim Reward (GET URL)": "https://bestservers.com/api/vote.php?action=claim&key={0}&steamid={1}",
      "API Vote status (GET URL)": "https://bestservers.com/api/vote.php?action=status&key={0}&steamid={1}",
      "Vote link (URL)": "https://bestservers.com/server/{0}",
      "Site Uses Username Instead of Player Steam ID?": "false"
    }
  }
}
```

## FAQ

Get Your API Keys:

Add your server to Rust-Server.net, RustServers.gg, or BestServers.com, or all.

You can find the id from the last part of the voting site's URL for your server.

- in RustServers.gg id is right here https://rustservers.gg/server/123 <- in this case, is 123
- In Rust-Servers.net, id is right here http://rust-servers.net/server/123 <- in this case, is 123
- In BestServers.com, id is right here [http://BestServers.com/server/123](http://bestservers.com/server/123) <- in this case, is 123

Key is secret key what you should not share any one. Key is hidden in the voting site dashboard. Login your account and navigate to modify your server, somewhere there should be your apikey, key, secret token, etc.

Note that you can add all your servers in this config and let player vote all your server. It also let players claim reward in any server. Here is example how it could look after you finished to found your ID and KEY.

```JSON
"Servers": {
  "My Server x10": {
    "RustServers.gg": "12345:gsvdwsdsdsfddfgsfdg21342uJTRA9oOPIASCNDJK12343b",
    "Rust-Servers.net": "12345:gsvdwsdsdsfddfgsfdg21342uJTRA9oOPIASCNDJK12343b",
    "BestServers.com" : "12345:gsvdwsdsdsfddfgsfdg21342uJTRA9oOPIASCNDJK12343b"
  },
  "My Second server x10000": {
    "Rustservers.gg": "12345:gsvdwsdsdsfddfgsfdg21342uJTRA9oOPIASCNDJK12343b",
    "Rust-Servers.net": "12345:gsvdwsdsdsfddfgsfdg21342uJTRA9oOPIASCNDJK12343b",
    "BestServers.com" : "12345:gsvdwsdsdsfddfgsfdg21342uJTRA9oOPIASCNDJK12343b"
  }
}
```

You must reload the plugin after making changes to the config.
If you found out that you do not get any reward after voting server or /vote chat command not showing any server what you just added. Then open logs (oxide/logs/EasyVote) and there you can see what cause the error. You can also enable debug mode and you can then reach out in the Discussions tab with your issue.
If everything works just fine then start modifying rewards settings.

## What is Closest reward feature?

Here is an example configuration:

```JSON
"Rewards": {
    "@": [
      "giveto {playerid} supply.signal 1"
    ],
    "first": [
      "addgroup {playerid} vip 7d"
    ],
    "3": [
      "sr add {playerid} 1000"
    ],
    "6": [
      "sr add {playerid} 5000"
    ]
},
```

Plugin will always give the last/closest reward based on their votes.

"@" means all the time reward, "first" means once time reward.

```
[First Vote] -> first & @ reward
[2nd Vote] -> @ reward
[3rd Vote] -> 3 & @ reward
[4th Vote] -> @ reward
[5th Vote] -> @ reward
[6th Vote] -> 6 & @ reward
Etc. etc.
```

If "Vote rewards cumulative" is enabled from config. Player will got all past reward(s), like so..

```
[First Vote] -> first & @ reward
[2nd Vote] -> first & @ reward
[3rd Vote] -> first & 3 & @ reward
[4th Vote] -> first & 3 & @ reward
[5th Vote] -> first & 3 & @ reward
[6th Vote] -> first & 3 & 6 & @ reward
Etc. etc.
```

