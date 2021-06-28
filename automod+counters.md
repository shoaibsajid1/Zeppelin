# AUTOMOD + COUNTERS

**COUNTER TIP**

>Counter decays are currently processed every 5 minutes. They are, however, still applied according to the decay time, even if it's lower than 5 minutes, so "1 every 30s" would decay 10 points at once every 5 minutes.


**COUNTER DECAY**

> Counter decays are currently processed every 5 minutes. They are, however, still applied according to the decay time, even if it's lower than 5 minutes, so "1 every 30s" would decay 10 points at once every 5 minutes.

**LOOSE MATCHING**

`loose_matching` allows a number of letters
(controlled by `loose_matching_threshold`)
*between* letters for word matching
so e.g. if you wanted to match "hello" and enabled `loose_matching`, it would also match e.g. "h|e|l|l|o"

**ALERT TIP**
`replieduser` is whether or not to ping the user you are replying to



**AUTOMOD TIP**

>setting up an automod config that insta-bans people if they mention more than 15 people in the same message
 use `mention_spam` with amount 15, within 0s
 as the trigger

`only_full_words`
- if `true`: if it needs to filter `banana` in a message it'll delete `I am a banana` but not `I am a banananan`
- if `false`: if it needs to filter `banana` in a message it'll delete both `banana` and `bananana`

`normalize`
When enabled, the matched text is normalized (converted to alphanumeric) before matching
- Allows matching text even when some letters have been replaced by similar looking letters from other alphabets

`loose_matching` and `loose_matching_threshold`
- When `loose_matching` is enabled, words are matched even when there are other letters or spaces between the letters

- `loose_matching_threshold` controls how many extra letters, at most, can be between the letters (spaces are unlimited). Defaults to 4.


**REGEX TIP**

`(<a?:[\w~]{2,32}:\d{17,19}>)` is an emoji regex for animated and non-animated emojis.




📣 **GOOD TO KNOW**
         the default modifier, if not specified, is `>=`



**LOOKING FOR GROUP**

 ```yml
 plugins:
   automod:
     config:
       rules:
         # Rule that does not do anything when it matches the *allowed* format.
         # This stops automod from processing further rules.
         allowed_lfg:
           enabled: false
           triggers:
             match_regex:
               patterns: ["^\\?lfg"]
           actions:
             log: false

         # Rule that is run for *every message* that does not match the allowed format above
         disallowed_lfg:
           enabled: false
           triggers:
             match_regex:
               patterns: [".*"] # Match anything
           actions:
             clean: true
             reply: "Please use ?lfg"

     overrides:
       - channel: "1234123412341234" # LFG channel ID here
         config:
           rules:
             allowed_lfg:
               enabled: true
             disallowed_lfg:
               enabled: true
 ```

It's a bit of a hack but it works and is clean to tweak. The idea is that anything that does *not* match the `allowed_lfg` rule on the LFG channel gets the actions from the `disallowed_lfg` rule (i.e. clean + reply).

This works because automod only applies one rule per message, so when the `allowed_lfg` rule matches (and does nothing), it doesn't continue matching the other rules anymore.
I also used regex for matching ?lfg only at the beginning of the message
This will be cleaner in the future when you'll be able to do negations in triggers (i.e. `not:`)
and combine them etc.

**REGEX TIP**

`((<a?:[\w~]{2,32}:\d{17,19}>)[\S\s]*?){5,}` - Detect 5 or more emoji's in a message. You can replace 5 with whatever you want.

#### PLUGIN CODE

```yaml
automod:
  config:
    rules:
      badwords: #badwords
        enabled: true
        triggers:
        - match_words:
            words:
            - retard
            - retarted
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
            - shit
            - stfu
            - ass
            - porn
            - hentai
            - cock
            - cock-sucker
            - cockface
            - cockhead
            - cocks
            - cocksuck
            - cocksucked
            - cocksucker
            - cocksucking
            - cocksucks
            - penis
            - dumbass
            case_sensitive: true
            only_full_words: true
            normalize: true
            loose_matching: false
            loose_matching_threshold: 0
            strip_markdown: true
            match_messages: true
            match_embeds: true
            match_visible_names: false
        - match_words:
            words:
            - 'fuck'
            case_sensitive: true
            only_full_words: false
            normalize: true
            loose_matching: false
            loose_matching_threshold: 0
            strip_markdown: true
            match_messages: true
            match_embeds: true
            match_visible_names: false
        - match_regex:
            patterns:
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
          clean: true
          reply:
            text:
              content: "<@{user.id}> Watch your language"
            auto_delete: 5s
          add_to_counter:
            counter: "badword"
            amount: 1 # This infraction adds 1 automod infraction points

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
              content: "<@{user.id}> No copypasta please"
            auto_delete: 10s
          add_to_counter:
            counter: "spam"
            amount: 1 # This infraction adds 1 automod infraction points

      invites:
        enabled: true
        triggers:
        - match_invites:
            allow_group_dm_invites: true
            exclude_guilds: []
            match_messages: true
            match_embeds: true
            match_visible_names: false
            exclude_invite_codes:
              - rey #rey server
              - tribegaming #tribegaming server
        actions:
          log: true
          clean: true
          reply:
            text:
              content: "<@{user.id}> Server invites are not allowed"
            auto_delete: 6s
          add_to_counter:
            counter: "spam"
            amount: 1 # This infraction adds 1 automod infraction points

      spam:
        enabled: true
        triggers:
        - message_spam:
            amount: 10
            within: 7s
        - mention_spam:
            amount: 7
            within: 10s
        - link_spam:
            amount: 6
            within: 20s
            per_channel: false
        - attachment_spam:
            amount: 5
            within: 10s
        - emoji_spam:
            amount: 8
            within: 10s
        - line_spam:
            amount: 7
            within: 8s
        - character_spam:
            amount: 4000
            within: 10s
        - sticker_spam:
            amount: 5
            within: 10s
        actions:
          log: true
          clean: false
          reply:
            text:
              content: "<@{user.id}> Spam Detected"
            auto_delete: 6s
          add_to_counter:
            counter: "spam"
            amount: 1 # This infraction adds 1 automod infraction points

      owner:
        enabled: true
        triggers:
        - match_words:
            words:
              - 'nat ♡'
            case_sensitive: false
            match_messages: false
            match_embeds: false
            match_visible_names: true
            only_full_words: true
            loose_matching: false
            loose_matching_threshold: 50
        actions:
          clean: false
          log: true
          reply:
            text:
              content: "<@{user.id}> You can't have the same name as Server Owner"
            auto_delete: 10s
          change_nickname:
            name: >-
              Change your name

      name:
        enabled: true
        triggers:
        - match_regex:
            patterns:
              - 'dragory maximus|potato'
        actions:
          clean: true
          alert:
            channel: "572122519616749586" #mod chat
            text: |-
              :link: <@!{user.id}>(`{user.id}`) said nats name!
              {matchSummary}
              *Automatically Cleaned*

      natping:
        enabled: true
        triggers:
        - match_regex:
            patterns: ['<@!?237661249335328768>']
        actions:
          clean: false
          log: true
          reply:
            text:
              content: "<@{user.id}> One nat ping is fine, continued pings will result in action"
            auto_delete: 10s
          add_to_counter:
            counter: "natping_c"
            amount: 1 # This infraction adds 1 automod infraction points

      nonenglish: #non english filter
        enabled: true
        affects_bots: false
        triggers:
        - match_regex:
            patterns:
              - "[\u0600-\u06FF]+" # Arabic
              - "(\u0196|\u0214|\u0220|\u0223|\u0228|\u0246|\u0252)+" # German
              - "(\u0192|\u0194|\u0196|\u0198|\u0199|[\u0200-\u0204]|\u0206|\u0207|\u0210|\u0212|\u0140|\u0217|\u0219|\u0220|\u0224|\u0226|\u0228|\u0230|\u0231|[\u0232-\u0236]|\u0238|\u0239|\u0244|\u0244|\u0156|\u0249|\u0251|\u0252)+" # French/Italian
              - "(\u0161|\u0191|\u0193|\u0201|\u0205|\u0209|\u0211|\u0218|\u0220|\u0225|\u0233|\u0237|\u0241|\u0243|\u0250|\u0252)+" #Spanish
              - "[\u4e00-\u9faf\u3400-\u4dbf]+" # Chinese
              - "[\u0400-\u04FF]+" # Cryllic (Russian)
              - "[\u0370-\u03FF]+" # Greek
              - "[\u1F00-\u1FFF]+" # Greek Extended
              - "[\u05BE-\u05F4]+" # Hebrew
              - "(?![ツ])[\u30A0-\u30FF]+" # Japanese (Hiragana)
              - "(?![ツ])[\u30A0-\u30FF]+" # Japanese (Kana)
        actions:
          clean: false
          reply:
            text:
              content: "<@{user.id}> Lets try to keep it english only"

      boostadded:
        enabled: true
        triggers:
        - role_added: ['618663125016641537'] #booster role
        actions:
          alert:
            channel: "808334772102234142" #misc channel
            text: >-
              :green_circle: <@!{user.id}> Just boosted Server! (alert)

      boostremoved:
        enabled: true
        triggers:
        - role_removed: ['618663125016641537'] #booster role
        actions:
          remove_roles:
            - '754619197358604389' #blue
            - '753514538820698133' #red
            - '762207737857703946' #green
            - '762207748732747818' #yellow
            - '762207747592028160' #purple
            - '772424797719625749' #brown
            - '772424620149833748' #white
          alert:
            channel: "572122519616749586" #mod chat
            text: >-
              :red_circle: <@!{user.id}> stopped boosting! Pls check if roles were removed (alert)

      off:
        enabled: false
        triggers:
        - match_regex:
            patterns:
              - '^\!off\b'
        actions:
          log: true
          set_antiraid_level: "off"
          reply:
            text:
              content: "<@{user.id}> Antiraid is off!"

      low:
        enabled: false
        triggers:
        - match_regex:
            patterns:
              - '^\!low\b'
        actions:
          log: true
          set_antiraid_level: "low"
          reply:
            text:
              content: "<@{user.id}> Antiraid is now set to low (default)"
          set_counter:
            counter: "antiraid_decay"
            value: 0 # "Reset!"

      high:
        enabled: false
        triggers:
        - match_regex:
            patterns:
              - '^\!high\b'
        actions:
          log: true
          set_antiraid_level: "high"
          reply:
            text:
              content: "<@{user.id}> Antiraid is set to high, it will go back to low in 20m automatically"
          set_counter:
            counter: "antiraid_decay"
            value: 2 # "Disable after 20min"

      disable_antiraid_after_timer:
        triggers:
          - counter_trigger:
              counter: "antiraid_decay"
              trigger: "disable"
        actions:
          set_antiraid_level: "low"

      newalert:
        enabled: true
        triggers:
        - member_join:
            only_new: true
            new_threshold: 3h
        actions:
          alert:
            channel: "857908693567930398" #joins
            text: |-
              :eyes: {user.username} (`{user.id}`) is a brand new account.
              <:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460>

      high_trigger:
        enabled: true
        triggers:
        - member_join_spam:
            amount: 10
            within: 18s
        actions:
          set_antiraid_level: "high"
          alert:
            channel: "572122519616749586" #modchat
            text: |-
              Dear <@&572104727077322763> MASS JOIN ALERT
              10 people joined within 18 seconds , Could be a raid
              Antiraid is now set to **high**
            allowed_mentions:
              everyone: false
              users: true
              roles: true
              repliedUser: false

      highspam:
        enabled: false
        triggers:
        - message_spam:
            amount: 10
            within: 7s
        - mention_spam:
            amount: 7
            within: 10s
        - link_spam:
            amount: 6
            within: 20s
            per_channel: false
        - attachment_spam:
            amount: 5
            within: 10s
        - emoji_spam:
            amount: 8
            within: 10s
        - line_spam:
            amount: 7
            within: 8s
        - character_spam:
            amount: 4000
            within: 10s
        - sticker_spam:
            amount: 5
            within: 10s
        actions:
          log: true
          reply:
            text:
              content: "<@{user.id}> Spam Detected!!!!"
            auto_delete: 6s
          add_to_counter:
            counter: "spam"
            amount: 1 # This infraction adds 1 automod infraction points

      autokick:
        enabled: false
        triggers:
        - member_join:
            only_new: true
            new_threshold: 3h
        actions:
          kick:
            reason: "Your account is very new and is marked as suspcious so it got kicked, If you think this is a mistake. Please try joining again in some time (like 30 minutes or so?) at discord.gg/nat"

      rob:
        enabled: false
        triggers:
          - match_words:
              only_full_words: false
              case_sensitive: false
              normalize: true
              match_nicknames: false
              words:
                - 'pls rob'
                - 'pls heist'
                - 'pls steal'
                - 'pls bankrob'
        actions:
          log: false
          clean: false
          add_to_counter:
            counter: 'auto_response_counter'
            amount: 1
          reply: ':x: <@!{user.id}> **This command is disabled in this server because users simply join to steal from the richest person and then leave.**'

      autorole: #adds member role upon first message on server
        enabled: true
        affects_bots: false
        triggers:
          - any_message: {} #any message sent triggers this
        actions:
          log: true
          add_roles:
            - "766285827612999752" #member

      badwordc1:
        triggers:
          - counter_trigger:
              counter: "badword"
              trigger: "silent"
        actions:
          log: false

      badwordc2:
        triggers:
          - counter_trigger:
              counter: "badword"
              trigger: "warning"
        actions:
          alert:
            channel: "855843592417050624" #punishments
            text: |-
              **BAD WORD**
              <:profile:841364699958607894><:dash:855062799659171850><@!{user.id}><:dot:855062799607529472>**{user.username}#{user.discriminator}**
              <:iconid:778924898176466944><:dash:855062799659171850>`{user.id}`
              <:iconbuildoverride:815459629869826048> User was warned automatically after 2 violations!
              <:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460>
          warn:
            reason: |-
              **Badwords detected , Continuing will result in a mute**

            notify: dm
            postInCaseLog: false
            hide_case: true

      badwordc3:
        triggers:
          - counter_trigger:
              counter: "badword"
              trigger: "mute"
        actions:
          mute:
            reason: |-
              **Badwords detected** , Already Warned Before
            duration: 5m
            remove_roles_on_mute: true
            restore_roles_on_mute: true
            postInCaseLog: false
            hide_case: true
          alert:
            channel: "855843592417050624" #punishments
            text: |-
              **BAD WORD**
              <:profile:841364699958607894><:dash:855062799659171850><@!{user.id}><:dot:855062799607529472>**{user.username}#{user.discriminator}**
              <:iconid:778924898176466944><:dash:855062799659171850>`{user.id}`
              <:iconbuildoverride:815459629869826048> User muted automatically (For 5m) after 3 violations
              <:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460>
          set_counter:
            counter: "badword"
            value: 0

      spamc1:
        triggers:
          - counter_trigger:
              counter: "spam"
              trigger: "silent"
        actions:
          log: false

      spamc2:
        triggers:
          - counter_trigger:
              counter: "spam"
              trigger: "silent2"
        actions:
          log: false
          clean: true

      spamc3:
        triggers:
          - counter_trigger:
              counter: "spam"
              trigger: "warning"
        actions:
          alert:
            channel: "855843592417050624" #punishments
            text: |-
              **BAD WORD**
              <:profile:841364699958607894><:dash:855062799659171850><@!{user.id}><:dot:855062799607529472>**{user.username}#{user.discriminator}**
              <:iconid:778924898176466944><:dash:855062799659171850>`{user.id}`
              <:iconbuildoverride:815459629869826048> User was warned automatically after 2 violations!
              <:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460>
          warn:
            reason: |-
              **Spam detected , Continuing will result in a mute**

            postInCaseLog: false
            hide_case: true

      spamc4:
        triggers:
          - counter_trigger:
              counter: "spam"
              trigger: "mute"
        actions:
          mute:
            reason: |-
              **Spam detected** , Already Warned Before
            duration: 5m
            remove_roles_on_mute: true
            restore_roles_on_mute: true
            postInCaseLog: false
            hide_case: true
          alert:
            channel: "855843592417050624" #punishments
            text: |-
              **SPAM DETECTED**
              <:profile:841364699958607894><:dash:855062799659171850><@!{user.id}><:dot:855062799607529472>**{user.username}#{user.discriminator}**
              <:iconid:778924898176466944><:dash:855062799659171850>`{user.id}`
              <:iconbuildoverride:815459629869826048> User muted automatically (For 5m) after 3 violations
              <:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460>
          set_counter:
            counter: "spam"
            value: 0

      natpingc1:
        triggers:
          - counter_trigger:
              counter: "natping_c"
              trigger: "silent"
        actions:
          log: false

      natpingc2:
        triggers:
          - counter_trigger:
              counter: "natping_c"
              trigger: "warning"
        actions:
          alert:
            channel: "855843592417050624" #punishments
            text: |-
              **PINGED NAT 2nd TIME**
              <:profile:841364699958607894><:dash:855062799659171850><@!{user.id}><:dot:855062799607529472>**{user.username}#{user.discriminator}**
              <:iconid:778924898176466944><:dash:855062799659171850>`{user.id}`
              <:iconbuildoverride:815459629869826048> User was warned automatically after 2nd Ping!
              <:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460>
          warn:
            reason: |-
              **Pinging nat 2x in one min , Continuing will result in a mute**
            postInCaseLog: false
            hide_case: true

      natpingc3:
        triggers:
          - counter_trigger:
              counter: "natping_c"
              trigger: "mute"
        actions:
          mute:
            reason: |-
              **Pinged nat 3x in one min , Already Warned Before**
            duration: 5m
            remove_roles_on_mute: true
            restore_roles_on_mute: true
            postInCaseLog: false
            hide_case: true
          alert:
            channel: "855843592417050624" #punishments
            text: |-
              **PINGED NAT 3rd TIME**
              <:profile:841364699958607894><:dash:855062799659171850><@!{user.id}><:dot:855062799607529472>**{user.username}#{user.discriminator}**
              <:iconid:778924898176466944><:dash:855062799659171850>`{user.id}`
              <:iconbuildoverride:815459629869826048> User muted automatically (For 5m) after 3 Pings in 1m
              <:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460>
          set_counter:
            counter: "natping_c"
            value: 0

      accumulate_activity:
        triggers:
          - any_message: {} #triggers on every message
        actions:
          log: false # Don't spam logs with activity changes
          add_to_counter:
            counter: "activity"
            amount: 1 # Each message adds 1 to the counter
        cooldown: 1m # Only count 1 message per minute

      grant_activity_role: #give regulars role
        triggers:
          - counter_trigger:
              counter: "activity"
              trigger: "grant_role"
        actions:
          add_roles: ["766917973885059082"] # Role ID for activity role

      remove_activity_role: #remove role when irregular
        triggers:
          - counter_trigger:
              counter: "activity"
              trigger: "grant_role"
              reverse: true # This indicates we want to use the *reverse* of the specified trigger, see reverse_condition in counters above
        actions:
          remove_roles: ["766917973885059082"] # Role ID for activity role

  overrides:
  - role: "766285827612999752" #disable rule once role is given
    config:
      rules:
        autorole:
          enabled: false

  - extra:
      antiraid_level: "off"
    config:
      rules:
        spam:
          enabled: false
        copypasta:
          enabled: false
        highspam:
          enabled: false
        autokick:
          enabled: false

  - extra:
      antiraid_level: "low"
    config:
      rules:
        highspam:
          enabled: false

  - extra:
      antiraid_level: "high"
    config:
      rules:
        high_trigger:
          enabled: false
        autokick:
          enabled: true

  - level: '>=50'
    config:
      can_view_antiraid: true
      can_set_antiraid: true
      rules:
        badwords:
          enabled: false
        copypasta:
          enabled: false
        owner:
          enabled: false
        name:
          enabled: false
        highspam:
          enabled: false
        spam:
          enabled: false
        autokick:
          enabled: false
        invites:
          enabled: false
        nonenglish:
          enabled: false
        natping:
          enabled: false
        off:
          enabled: true
        low:
          enabled: true
        high:
          enabled: true

counters:
  config:
    counters:
      badword:
        per_user: true
        triggers:
          silent:
            condition: ">=1"
          warning:
            condition: ">=3"
          mute:
            condition: ">=4"
        # Remove 1 automod infraction points per 20s
        decay:
          amount: 1
          every: 2m

      spam:
        per_user: true
        triggers:
          silent:
            condition: ">=1"
          silent2:
            condition: ">=2"
          warning:
            condition: ">=3"
          mute:
            condition: ">=4"
        # Remove 1 automod infraction points per 20s
        decay:
          amount: 1
          every: 2m

      natping_c:
        per_user: true
        triggers:
          silent:
            condition: ">=1"
          warning:
            condition: ">=2"
          mute:
            condition: ">=3"
        # Remove 1 automod infraction points per 20s
        decay:
          amount: 1
          every: 3m

      activity:
        per_user: true
        triggers:
          grant_role:
            condition: ">=20"
            # We set a separate threshold for when the role should be removed. This is so the decay doesn't remove the activity role immediately.
            # If this value isn't set, reverse_condition defaults to the opposite of the condition, i.e. "<100" in this case.
            reverse_condition: "<5"
        decay:
          amount: 1
          every: 24h

      antiraid_decay:
        triggers:
          disable:
            condition: "<1"
        decay:
          amount: 1
          every: 1m
```
