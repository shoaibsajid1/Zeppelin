# UTILITY

**AVATAR**
![avatar](https://media.discordapp.net/attachments/770256340639416320/830444957654843413/Screen_Shot_2021-04-10_at_7.11.36_PM.png)

**JUMBO**
![jumbo](https://cdn.discordapp.com/attachments/832964085976530964/834393774426816552/Screen_Shot_2021-04-21_at_4.40.37_PM.png)

🚩 **SEARCH FLAGS**

`!s -sort id dex` sort all dex results by ID

`!s -bot` lists all bots

`!s -p 1 dex` search page 1 of dex results

`!s -e` export results (via a link)

`!s -ids` excludes usernames and lists only ids

`!s -re dex` regex search for users named dex

`!s -v` lists all ppl in vc

Examples:
`!s -ids -e dex` exports all ids of users named dex on server
Note: *the results can be used for `!massban` command afterwards*

🗒️ **CLEAN MESSAGES FROM USER AND ADD TO CASE**

`!clear <count> -u userid -c #channel -update`

Note: the `-update` at the end is if you want to add it to their mod log case


**CLEAN COMMAND TIP**

Deletes everything but image attachments

![clean](https://media.discordapp.net/attachments/846691383280009216/856783756232359946/unknown.png?width=581&height=518)

#### PLUGIN CODE

```yaml
utility: #https://zeppelin.gg/docs/plugins/utility/usage
  replaceDefaultOverrides: true #replaces default settings if true
  config:
    #List all roles or roles matching a search
    #!roles [search] -counts -sort
    can_roles: true

    #Show the permission level of a user
    #!level [member]
    can_level: false

    #Search banned users
    #!bansearch <query> [-page] [-sort] [-case-sensitive] [-export] [-ids] [-regex]
    #Search server members
    #!search [query] [-page] [-role] [-voice] [-bot] [-sort] [-case-sensitive] [-export] [-ids] [-regex] [-status-search]
    can_search: true

    #Remove a number of recent messages
    #!clean <count>
    can_clean: false

    #Show information about the specified thing
    #needed for many info sub commands
    #!info [value]
    can_info: false

    #Show server information
    #!server [serverId]
    can_server: false

    #Show information about an invite
    #!invite <inviteCode>
    can_inviteinfo: false

    #Show information about a channel
    #!channel [channel]
    can_channelinfo: false

    #Show information about a message
    #!message <message>
    can_messageinfo: false

    #Show information about a user
    #!user [user] -compact
    can_userinfo: false

    #Show information about a role
    #!roleinfo <role>
    can_roleinfo: false

    #Show information about an emoji
    #!emoji [emoji]
    can_emojiinfo: false

    #Show information about a snowflake ID
    #!snowflake <id>
    can_snowflake: false

    #Reload the Zeppelin configuration and all plugins for the server.
    #This can sometimes fix issues.
    #!reload_guild
    can_reload_guild: false

    #Set a member's nickname
    #!nickname <member> <nickname>
    #Reset a member's nickname to their username
    #!nickname reset <member>
    can_nickname: false

    #Test the bot's ping to the Discord API
    #!ping
    can_ping: false

    #View the message source of the specified message id
    #!source <message>
    can_source: false

    #Move a member to another voice channel
    #!vcmove <member> <channel>
    #Move all members of a voice channel to another voice channel
    #!vcmoveall <oldChannel> <channel>
    can_vcmove: false

    #Disconnect a member from their voice channel
    #!vcdisconnect <member>
    can_vckick: false

    #Show a quick reference for the specified command's usage
    #!help <command>
    can_help: false

    #Show information about Zeppelin's status on the server
    #!about
    can_about: false

    #Get a link to the context of the specified message
    #!context <channel> <messageId>
    can_context: false

    #Makes an emoji jumbo
    #!jumbo <emoji>
    can_jumbo: false
    jumbo_size: 128

    #Retrieves a user's profile picture
    #!avatar [user]
    can_avatar: false

    info_on_single_result: true
  overrides:
    - level: '>=50'
      config:
        can_roles: true
        can_level: true
        can_search: true
        can_clean: true
        can_info: true
        can_server: true
        can_inviteinfo: true
        can_channelinfo: true
        can_messageinfo: true
        can_userinfo: true
        can_roleinfo: true
        can_emojiinfo: true
        can_snowflake: true
        can_nickname: true
        can_vcmove: true
        can_vckick: true
        can_help: true
        can_context: true
        can_jumbo: true
        can_avatar: true
        can_source: true
    - level: '>=100'
      config:
        can_reload_guild: true
        can_ping: true
        can_about: true
```
