# ZEP BY DEX
![Zep banner](assets/zepbanner.png)


**CONSIDER PUTTING A ⭐️ ON THIS REPO**

### What is Zeppelin ?

>Zeppelin is a bot that offers high level of customization, its basically build a bot where you decide what you want the bot to do.

### How to use zep ?

> You use zep via online dashboard, unlike most dashboard you control the entire thing by updating just one file (its called a yaml file). There are various plugins/modules that you enable and customize.

### Where do I start ?

The bot works as follows, you can have levels from 1 to 100. By default, zeppelin assumes mod as level 50, and admin as level 100 but you can change that once you get used to the bot.

**Step 1:** Set the prefix

**Step 2:** Insert role IDs for level 50 and 100

**Step 3:** Type plugins

 This is where you will start enabling modules later on

**EXAMPLE SETUP**

The image below shows what the dashboard looks like after you set all these. In this example we enabled the `auto_reactions` plugin. Note that the `success_emoji` and `error_emoji` are optional if you want to set your own you can but if you dont type anything, it will use the default.

![Example Config](assets/dashboard.png)

## CONFIG FOR NEW USERS

> Note: This excludes Counters, companion_channels, persist, pingable_roles, roles, self_grantable_roles, starboard & tags plugins as they are not often used by starters. But this should get you off to a good start with default settings on zep!

<details>
  <summary>Click to view beginners config!</summary>

```yaml
prefix: '!'

levels:
  "844782218563944488": 100 #admin role
  "844759879847247893": 50  #Mod role

plugins:
  post: {}
  reminders: {}
  auto_reactions: {}
  locate_user: {}
  reaction_roles: {}
  slowmode: {}
  utility: {}
  time_and_date: {}
  
  cases:
    config:
      case_log_channel: "854373344232865832" #cases channel id

  mutes:
    config:
      mute_role: "777121217630175243" #muterole id here

  mod_actions:
    config:
      dm_on_kick: true
      dm_on_ban: true
      
 
  welcome_message:
    config:
      send_dm: true
      message: |-
              **Welcome to Dexter's Laboratory**
              
              **Invite others with**
              https://discord.gg/... 

  logs:
    config:
      channels:
        '761972021612904519': #log channel id here 
          exclude: [] #exclude nothing, include everythinh
      format:
        timestamp: ""

  automod:
    config:
      rules:
        badwords: #badwords
          enabled: true
          triggers:
          - match_words:
              words: [
                "﷽","﷽", "|", "⣿",
                "pornhub", "seggz", "dildo", "edp445", "卍", "simping", "slmp", "slmps",
                "simp", "s1mp", "simps", "s1mps", "biitch", "tards", "Fäg", "sex", 
                "virgin", "ræpe", "sexual", "r*pist", "r*apist", "r*pe",
                "superstraight", "bitch", "bitches", "b1tch", "b1tches",
                "milf", "milfs", "xp grind", "raped", "Cum", "Rape", "kys", "kill yourself",
                "cumming", "autist", "raping", "porn", "pornography", "anal", "cunt", "cnut",
                "pussy", "cock", "cocks", "c0ck", "hentai", "shemale", "pedophile", "pedo", 
                "nazi", "porno", "puta", "semen", "slut", "twat", "wank", "loli", "rape",
                "rapist", "lolis", "tits", "boob", "boobies", "tit", "nude", "nudes", "vagina",
                "retard", "braindead", "hoe", "libtard", "titty", "porn", "thot", 
                "sperg", "dick", "hoes", "retrad", "penis", "whore", "suicide", "kill myself", 
                "cuck", "blowjob", "raping", "boobs", "retarded", "incel", "retards", "incel",
                "cunts", "tarded", "discord.gift", "lolicon", "loli","⣠", "⡖","⠋", "⠉","⠛",
                "testicals","卐", "ching chong", "Fag"]
              case_sensitive: true
              only_full_words: true
              normalize: true
              loose_matching: false
              loose_matching_threshold: 0
              strip_markdown: true
              match_messages: true
              match_embeds: true
              match_visible_names: false
          - match_regex:
              patterns:
                #- 'fuck'
                - 'afak'
                - 'n[il1]+g{2,}(er|a)' #nigger
                - "n[\\s.\\-]*[i1][\\s.\\-]*[g6][\\s.\\-]*[g6][\\s.\\-]*[e3][\\s.\\-]*r" #nigger
                - "n[\\s.\\-]*[i1][\\s.\\-]*[g6][\\s.\\-]*[g6][\\s.\\-]*a" #nigga
                - "f[\\s.\\-]*a[\\s.\\-]*[g6][\\s.\\-]*[g6][\\s.\\-]*o[\\s.\\-]*[t7]" #faggot
              normalize: true
              strip_markdown: true
              match_messages: true
              match_embeds: true
              match_visible_names: false
          actions:
            clean: false
            reply:
              text: 
                content: "<@{user.id}> Whoa :p"
              auto_delete: 3s


        copypasta: #copy paste spam
          enabled: true
          triggers:
            - match_regex:
                patterns: 
                  - "[⠁⠂⠃⠄⠅⠆⠇⠈⠉⠊⠋⠌⠍⠎⠏⠐⠑⠒⠓⠔⠕⠖⠗⠘⠙⠚⠛⠜⠝⠞⠟⠠⠡⠢⠣⠤⠥⠦⠧⠨⠩⠪⠫⠬⠭⠮⠯⠰⠱⠲⠳⠴⠵⠶⠷⠸⠹⠺⠻⠼⠽⠾⠿]"
                  - "[░▐▌█▀▄]"
                  - \# - "^(\\s*\\|\\|.+?\\|\\|\\s*)+$" 
                  - (?:[\u2500-\u25FF\u2800-\u28FF]\s*){4,}
                  - '▐▀█▀▌'
                  - ⠟⠑⡄⠀⠀⠀⠀⠀⠀⠀ ⣀⣀⣤⣤⣤⣀⡀
                  - ඞ
                  - ████
                  - ⣿⣿⣿
                case_sensitive: false
                normalize: true
                strip_markdown: true
                match_messages: true
                match_embeds: true
          actions:
            log: true
            reply:
              text: 
                content: "<@{user.id}> No copypasta spam pls"
              auto_delete: 5s
    overrides:
    #Overrides are always calculated top down
    #For example:
    #If you want to have mods messages not be deleted, your overrides would need to be in this order:

    #1. Enable in channel xyz
    #2. Disable for mods
    #If you have it the other way round it'll delete everything, even from mods.

    - level: '>=50' #mods are not affected as its disabled for them
      config:
        can_view_antiraid: true #can view the antiraid level
        can_set_antiraid: true #can set the antiraid level
        rules:
          badwords:
            enabled: false 
          copypasta:
            enabled: false
```

</details>

---

## CONFIG FOR FAMILAR USERS

> Note: This config includes **ALL** the plugins zeppelin has to offer and should be more than enough for 90% of the servers!

<details>
  <summary>Click to view medium difficulty config!</summary>

```yaml
prefix: '!'

levels:
  "844782218563944488": 100 #admin role
  "844759879847247893": 50  #Mod role

plugins:
  post: {}
  reminders: {}
  auto_reactions: {}
  locate_user: {}
  reaction_roles: {}
  slowmode: {}
  utility: {}
  time_and_date: {}
  
  cases:
    config:
      case_log_channel: "854373344232865832" #cases channel id

  mutes:
    config:
      mute_role: "777121217630175243" #muterole id here

  mod_actions:
    config:
      dm_on_kick: true
      dm_on_ban: true
      
 
  welcome_message:
    config:
      send_dm: true
      message: |-
              **Welcome to Dexter's Laboratory**
              
              **Invite others with**
              https://discord.gg/... 

  logs:
    config:
      channels:
        '761972021612904519': #log channel id here 
          exclude: [] #exclude nothing, include everythinh
      format:
        timestamp: ""

  auto_delete:
    config:
      enabled: false
      delay: 5s
    overrides:
      - channel: "109672661671505920" #channel id
        config:
          enabled: true
          delay: 5s
      - level: '>=50' #mods are not affected as its disabled for them
        config:
          enabled: false

  companion_channels:
    config:
      entries:
        public_vcs: #name of the entry, could be anything
          voice_channel_ids: 
            - "799704245338112050" #voice vc
            - "855391042227404820" #music vc
          text_channel_ids:
            - "854374779691728946" # vc text
          #this can be calculated using https://discordapi.com/permissions.html
          permissions: 1024
          enabled: true

  persist:
    config:
      persisted_roles:
        - "844759879847247893" #member role id here
      persist_nicknames: true
      persist_voice_mutes: true

  self_grantable_roles:
    config:
      entries:
        basic: #you can have many entries and name them as u like
          roles:
            "762164188922904607": ["announce", "alert", "alerts"] #can have options too!
          can_use: true #can use this entry? since we can have multiple!
          can_ignore_cooldown: true #does nothing i guess? not sure ask #support
          max_roles: 1 #maximum no of roles user can pick from the list
      mention_roles: true #mentions the role itself (but no ping)

  roles:
    config:
      assignable_roles: #roles u can add to another user
        - '558037973581430785'
        - '875361358907060295'
    overrides:
      - level: '>=50'
        config:
          can_assign: true #level 50 and up can assign
      - level: '>=100'
        config:
          can_mass_assign: true # level 100 can mass assign and remove roles

  pingable_roles: #makes a role pingable when you start typing in a specific channel
    overrides:
      - level: '>=100'
        config:
          #Usage: !pingable_role <channelId> <role>
          #To disable: !pingable_role disable <channelId> <role>
          can_manage: true #only level 100 can run that ^

  starboard:
    config:
      boards:
        basic:
          channel_id: "604342689038729226"
          stars_required: 5

  tags:
    config:
      prefix: "!"
      delete_with_command: true ##delete_with_command would delete the bot response when the original message is deleted
      user_tag_cooldown: null #user_tag_cooldown is the cooldown per user per tag
      global_tag_cooldown: null #global_tag_cooldown is the global cooldown (server wide) per tag
      user_cooldown: 10s #user_cooldown is the cooldown per user (not tag specific)
      allow_mentions: false #allow tags to ping?, Can be enabled conditionally via overrides for e.g. only moderators
      global_cooldown: null #global_cooldown is the global cooldown (server wide) (not tag specific)
      auto_delete_command: false #When turned on, the message triggering a tag will be automatically deleted after the tag is posted
      can_create: false
      can_use: true
      can_list: true
      categories:
        "mental": 
          tags:
            "health":
              embed:
                title: "Mental Health Resources"
                color: 0xFF0000
                footer: 
                  text: "Remember, You Matter <3"
                  icon_url: https://media.discordapp.net/attachments/770256340639416320/854689949193076737/Medical_31-60_974.jpg?width=523&height=523
                #image: 
                  #url: https://i.pinimg.com/originals/f6/f6/e6/f6f6e629e0bb1ab4ef763c12b5457074.png
                thumbnail: 
                  url: https://media.discordapp.net/attachments/770256340639416320/854690141279748096/PngItem_4479310.png?width=523&height=523
                fields:
                -  name: "**National Suicide Prevention Hotline (U.S.):**"
                   value: |
                    **Call:** 1-800-273-8255, available 24/7 for emotional support
                    **Text: HOME** to 741741
                    https://suicidepreventionlifeline.org/chat/
                    
                    Outside the U.S: Find a supportive resource on [this Wikipedia list of worldwide crisis hotlines](https://en.wikipedia.org/wiki/List_of_suicide_crisis_lines)
                   inline: false
                -  name: "**More Support**"
                   value: |
                    For Substance Abuse Support, Eating Disorder Support & Child Abuse and Domestic Violence:
                    [Click to go to Discord's Health & Safety Page](https://discord.com/safety/360044103771-Mental-health-on-Discord#h_01EGRGT08QSZ5BNCH2E9HN0NYV)

  counters:
    config:
      counters:
        automod_infractions:
          per_user: true
          triggers:
            # When a user accumulates 100 or more (>=100) automod infraction points, this trigger will activate
            # The numbers here are arbitrary - you could choose to use 10 or 1000 instead.
            too_many_infractions:
              condition: ">=100"
          # Remove 100 automod infraction points per hour
          decay:
            amount: 100
            every: 1h
            
  automod:
    config:
      rules:
        badwords: #badwords
          enabled: true
          triggers:
          - match_words:
              words: [
                "﷽","﷽", "|", "⣿",
                "pornhub", "seggz", "dildo", "edp445", "卍", "simping", "slmp", "slmps",
                "simp", "s1mp", "simps", "s1mps", "biitch", "tards", "Fäg", "sex", 
                "virgin", "ræpe", "sexual", "r*pist", "r*apist", "r*pe",
                "superstraight", "bitch", "bitches", "b1tch", "b1tches",
                "milf", "milfs", "xp grind", "raped", "Cum", "Rape", "kys", "kill yourself",
                "cumming", "autist", "raping", "porn", "pornography", "anal", "cunt", "cnut",
                "pussy", "cock", "cocks", "c0ck", "hentai", "shemale", "pedophile", "pedo", 
                "nazi", "porno", "puta", "semen", "slut", "twat", "wank", "loli", "rape",
                "rapist", "lolis", "tits", "boob", "boobies", "tit", "nude", "nudes", "vagina",
                "retard", "braindead", "hoe", "libtard", "titty", "porn", "thot", 
                "sperg", "dick", "hoes", "retrad", "penis", "whore", "suicide", "kill myself", 
                "cuck", "blowjob", "raping", "boobs", "retarded", "incel", "retards", "incel",
                "cunts", "tarded", "discord.gift", "lolicon", "loli","⣠", "⡖","⠋", "⠉","⠛",
                "testicals","卐", "ching chong", "Fag"]
              case_sensitive: true
              only_full_words: true
              normalize: true
              loose_matching: false
              loose_matching_threshold: 0
              strip_markdown: true
              match_messages: true
              match_embeds: true
              match_visible_names: false
          - match_regex:
              patterns:
                #- 'fuck'
                - 'afak'
                - 'n[il1]+g{2,}(er|a)' #nigger
                - "n[\\s.\\-]*[i1][\\s.\\-]*[g6][\\s.\\-]*[g6][\\s.\\-]*[e3][\\s.\\-]*r" #nigger
                - "n[\\s.\\-]*[i1][\\s.\\-]*[g6][\\s.\\-]*[g6][\\s.\\-]*a" #nigga
                - "f[\\s.\\-]*a[\\s.\\-]*[g6][\\s.\\-]*[g6][\\s.\\-]*o[\\s.\\-]*[t7]" #faggot
              normalize: true
              strip_markdown: true
              match_messages: true
              match_embeds: true
              match_visible_names: false
          actions:
            clean: false
            reply:
              text: 
                content: "<@{user.id}> Whoa :p"
              auto_delete: 3s


        copypasta: #copy paste spam
          enabled: true
          triggers:
            - match_regex:
                patterns: 
                  - "[⠁⠂⠃⠄⠅⠆⠇⠈⠉⠊⠋⠌⠍⠎⠏⠐⠑⠒⠓⠔⠕⠖⠗⠘⠙⠚⠛⠜⠝⠞⠟⠠⠡⠢⠣⠤⠥⠦⠧⠨⠩⠪⠫⠬⠭⠮⠯⠰⠱⠲⠳⠴⠵⠶⠷⠸⠹⠺⠻⠼⠽⠾⠿]"
                  - "[░▐▌█▀▄]"
                  - \# - "^(\\s*\\|\\|.+?\\|\\|\\s*)+$" 
                  - (?:[\u2500-\u25FF\u2800-\u28FF]\s*){4,}
                  - '▐▀█▀▌'
                  - ⠟⠑⡄⠀⠀⠀⠀⠀⠀⠀ ⣀⣀⣤⣤⣤⣀⡀
                  - ඞ
                  - ████
                  - ⣿⣿⣿
                case_sensitive: false
                normalize: true
                strip_markdown: true
                match_messages: true
                match_embeds: true
          actions:
            log: true
            reply:
              text: 
                content: "<@{user.id}> No copypasta spam pls"
              auto_delete: 5s

        # An example automod rule that adds automod infraction points
        some_infraction:
          triggers:
            - match_words:
                words: ['poopoo head']

          actions:
            clean: true
            reply: 'Do not insult other users'
            add_to_counter:
              counter: "automod_infractions"
              amount: 25 # This infraction adds 25 automod infraction points

        # An example rule that is triggered when the user accumulates too many automod infraction points
        automute_on_too_many_infractions:
          triggers:
            - counter_trigger:
                counter: "automod_infractions"
                trigger: "too_many_infractions"

          actions:
            mute:
              reason: "You have been muted for tripping too many automod filters"
              remove_roles_on_mute: true
              restore_roles_on_mute: true

    overrides:
    #Overrides are always calculated top down
    #For example:
    #If you want to have mods messages not be deleted, your overrides would need to be in this order:

    #1. Enable in channel xyz
    #2. Disable for mods
    #If you have it the other way round it'll delete everything, even from mods.

    - level: '>=50' #mods are not affected as its disabled for them
      config:
        can_view_antiraid: true #can view the antiraid level
        can_set_antiraid: true #can set the antiraid level
        rules:
          badwords:
            enabled: false 
          copypasta:
            enabled: false
            
```

</details>

---

## CONFIG FOR POWER USERS

> Note: This is madlad stuff. This is wild as shit. You probbaly need to be insane to do this

<details>
  <summary>Click to view madlad difficulty config!</summary>

Coming soon
  </details>