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

### Config breakdown

Coming soon

For advanced users: Coming soon as well lmao

For total new beginners

## CONFIG FOR NEW USERS

<details>
  <summary>Click to view code!</summary>

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
              words: 
              - retard
              - e-girl
              - boobs
              - asshole
              - dick
              - cnut
              - dick
              - blowjob
              - slut
              - b1tch
              - slut
              - bitch
              - c0ck
              - pussy
              - thot
              - cunt
              - fuk
              - bitches
              - penis
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
