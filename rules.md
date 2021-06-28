# AUTOMOD RULES

#### BADWORDS

This rule works as follows:

- 1st violation = clean + one infraction + verbal warn

- 2nd violation = clean + one infraction + verbal warn

- 3rd violation = clean + one infraction + actual warning case is made + staff alerted in #punishment channel

- 4th violation = clean + counter reset + 5m mute logged + staff alerted in #punishment channel

<details>
  <summary>Click to view code!</summary>

Automod code
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
```
Counter code
```yaml
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
        # Remove 1 automod infraction points per 2 minutes
        decay:
          amount: 1
          every: 2m
```
</details>

---

#### COPYPASTA

This rule works as follows:

- 1st violation = clean + one infraction + verbal warn

- 2nd violation = clean + one infraction + verbal warn

- 3rd violation = clean + one infraction + actual warning case is made + staff alerted in #punishment channel

- 4th violation = clean + counter reset + 5m mute logged + staff alerted in #punishment channel

<details>
  <summary>Click to view code!</summary>

Automod code
```yaml
automod:
  config:
    rules:
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
```
Counter code
```yaml
counters:
  config:
    counters:
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
```
</details>

---

#### SPAM

This rule works as follows:

- 1st violation = clean + one infraction + verbal warn

- 2nd violation = clean + one infraction + verbal warn

- 3rd violation = clean + one infraction + actual warning case is made + staff alerted in #punishment channel

- 4th violation = clean + counter reset + 5m mute logged + staff alerted in #punishment channel

<details>
  <summary>Click to view code!</summary>

Automod code
```yaml
automod:
  config:
    rules:
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
```
Counter code
```yaml
counters:
  config:
    counters:
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
```
</details>

---

#### INVITES

<details>
  <summary>Click to view code!</summary>

Automod code
```yaml
automod:
  config:
    rules:
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
              - code
              - dyno
        actions:
          log: true
          clean: true
          reply:
            text:
              content: "<@{user.id}> Server invites are not allowed"
            auto_delete: 6s
```
</details>

---


#### AUTOROLE

This rule gives roles upon first message from user after they finish server gating

<details>
  <summary>Click to view code!</summary>

Automod code
```yaml
automod:
  config:
    rules:
      autorole: #adds member role upon first message on server
        enabled: true
        affects_bots: false
        triggers:
          - any_message: {} #any message sent triggers this
        actions:
          log: true
          add_roles:
            - "766285827612999752" #member
```
Override code
```yaml
  overrides:
  - role: "766285827612999752" #disable rule once role is given
    config:
      rules:
        autorole:
          enabled: false
```
</details>

---


#### LOOKING FOR GROUP

It's a bit of a hack but it works and is clean to tweak. The idea is that anything that does *not* match the `allowed_lfg` rule on the LFG channel gets the actions from the `disallowed_lfg` rule (i.e. clean + reply).

This works because automod only applies one rule per message, so when the `allowed_lfg` rule matches (and does nothing), it doesn't continue matching the other rules anymore.
I also used regex for matching ?lfg only at the beginning of the message
This will be cleaner in the future when you'll be able to do negations in triggers (i.e. `not:`)
and combine them etc.
</details>


<details>
  <summary>Click to view code!</summary>

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
---
