# LOGS


**COMMAND LOG VARIABLE**

This log type is not functional unfortunately. So just skip it!

#### PRETTY LOGS VERSION 1.0 (PLAIN EDITION)

<details>
  <summary>Click to view code!</summary>

```yaml
  logs:
    config:
      channels:
        '701603686102728725': #modlog X
          include:
            - MEMBER_WARN
            - MEMBER_MUTE
            - MEMBER_TIMED_MUTE
            - MEMBER_UNMUTE
            - MEMBER_TIMED_UNMUTE
            - MEMBER_MUTE_EXPIRED
            - MEMBER_KICK
            - MEMBER_BAN
            - MEMBER_UNBAN
            - MEMBER_FORCEBAN
            - MEMBER_SOFTBAN
            - MEMBER_NOTE
            - CLEAN
            - CASE_CREATE
            - MASSBAN
            - CASE_UPDATE
            - SET_ANTIRAID_USER
            - SET_ANTIRAID_AUTO
            - AUTOMOD_ACTION
            - MESSAGE_SPAM_DETECTED
            - OTHER_SPAM_DETECTED
            - CENSOR
            - BOT_ALERT

        '587370329622446152': #members X
          include:
            - MEMBER_JOIN
            - MEMBER_LEAVE
            - MEMBER_RESTORE
            - MEMBER_MUTE_REJOIN
            - MEMBER_JOIN_WITH_PRIOR_RECORDS

        '614858639420817469': #messages X
          include:
            - MESSAGE_EDIT
            - MESSAGE_DELETE
            - MESSAGE_DELETE_BULK
            - MESSAGE_DELETE_BARE
            - MESSAGE_DELETE_AUTO
          exclude_bots: true
          excluded_users: ["176082223894757377"]
          excluded_message_regexes:
            - /^[\d,]+?$/ # ignore messages with digits only (#count-to-a-million)

        '14860948733296649': #voice
          include:
            - VOICE_CHANNEL_JOIN
            - VOICE_CHANNEL_MOVE
            - VOICE_CHANNEL_LEAVE
            - VOICE_CHANNEL_FORCE_MOVE

        '643511827170590730': #role-changes
          include:
            - MEMBER_ROLE_ADD
            - MEMBER_ROLE_REMOVE
            - MEMBER_ROLE_CHANGES

        '846039475897106432': #simpler zep
          exclude: [] # Exclude nothing = include everything
          excluded_roles:
            - '777121217630175243' #moote role


        '799702944056475709': #zep all
          #include: []
          exclude: [] # Exclude nothing = include everything
          #batched: boolean
          #batch_time: number
          #excluded_users:
            #- as
          #excluded_message_regexes:
            #- as
          #excluded_channels:
            #- '2454' #channel name
          #excluded_categories:
            #- as
          exclude_bots: true



      format:
        timestamp: ""
        MEMBER_NOTE: "\U0001F58A Note added on {userMention(user)} by {userMention(mod)}"
        MEMBER_WARN: |-
            :warning: **MEMBER WARNED**
            ------------------
            <:iconmembers:778932116024459275> **USER**
            <@!{member.id}> | `{member.user.username}#{member.user.discriminator}` | `{member.id}`
            ------------------
            <:iconmembers:778932116024459275> **MOD**
            <@!{mod.id}> | `{mod.username}#{mod.discriminator}` | `{mod.id}`
            ------------------
            <:channelnews:779042577365205024> **REASON**
            {reason}
        MEMBER_MUTE: "\U0001F507 {userMention(user)} was muted indefinitely by {userMention(mod)}"
        MEMBER_TIMED_MUTE: "\U0001F507 {userMention(user)} was muted for **{time}** by {userMention(mod)}"
        MEMBER_UNMUTE: "\U0001F50A {userMention(user)} was unmuted by {userMention(mod)}"
        MEMBER_TIMED_UNMUTE: "\U0001F50A {userMention(user)} was scheduled to be unmuted in **{time}** by {userMention(mod)}"
        MEMBER_MUTE_EXPIRED: "\U0001F50A {userMention(member)}'s mute expired"
        MEMBER_KICK: "\U0001F462 {userMention(user)} was kicked by {userMention(mod)}"
        MEMBER_BAN: "\U0001F528 {userMention(user)} was banned by {userMention(mod)}"
        MEMBER_UNBAN: "\U0001F513 User (`{userId}`) was unbanned by {userMention(mod)}"
        MEMBER_FORCEBAN: "\U0001F528 User (`{userId}`) was forcebanned by {userMention(mod)}"
        MEMBER_SOFTBAN: "\U0001F528 {userMention(member)} was softbanned by {userMention(mod)}"

        MEMBER_JOIN: "\U0001F4E5 {new} {userMention(member)} joined (created {account_age} ago)"
        MEMBER_LEAVE: "\U0001F4E4 {userMention(member)} left the server"

        MEMBER_ROLE_ADD: |-

          **ROLE ADDED**
          ------------------
          <:iconmembers:778932116024459275> **USER**
          <@!{member.id}> | `{member.user.username}#{member.user.discriminator}` | `{member.id}`
          ------------------
          <:iconmembers:778932116024459275> **BY MOD**
          <@!{mod.id}> | `{mod.username}#{mod.discriminator}` | `{mod.id}`
          ------------------
          <:channelnews:779042577365205024> **ROLES**
          `{roles}`
        MEMBER_ROLE_REMOVE: |-

          **ROLE REMOVED**
          ------------------
          <:iconmembers:778932116024459275> **USER**
          <@!{member.id}> | {member.user.username}#{member.user.discriminator} | {member.id}
          ------------------
          <:iconmembers:778932116024459275> **BY MOD**
          <@!{mod.id}> | {mod.username}#{mod.discriminator} | {mod.id}
          ------------------
          <:iconsettings:778931333459738626> **ROLES**
          `{roles}`
        MEMBER_ROLE_CHANGES: |-

          **ROLE CHANGES**
          ------------------
          <:iconmembers:778932116024459275> **USER**
          <@!{member.id}> | {member.user.username}#{member.user.discriminator} | {member.id}
          ------------------
          <:iconmembers:778932116024459275> **BY MOD**
          <@!{mod.id}> | {mod.username}#{mod.discriminator} | {mod.id}
          ------------------
          <:channelnews:779042577365205024> **ROLES ADDED**
          {addedRoles}
          ------------------
          <:iconsettings:778931333459738626> **ROLES REMOVED**
          `{removedRoles}`

        MEMBER_NICK_CHANGE: |-
          ✏ **NICKNAME CHANGE**
          ------------------
          <:iconmembers:778932116024459275> **USER**
          <@!{member.id}> | {member.user.username}#{member.user.discriminator} | {member.id}
          ------------------
          `{oldNick}` to `{newNick}`
        MEMBER_USERNAME_CHANGE: |-
          ✏ **USERNAME CHANGE**
          ------------------
          <:iconmembers:778932116024459275> **USER**
          <@!{member.id}> | {member.user.username}#{member.user.discriminator} | {member.id}
          ------------------
          `{oldName}` to `{newName}`

        MEMBER_RESTORE: "\U0001F4BF Restored {restoredData} for {userMention(member)} on rejoin"
        MEMBER_TIMED_BAN: "\U0001F528 {userMention(user)} was tempbanned by {userMention(mod)} for {banTime}"
        MEMBER_TIMED_UNBAN: "\U0001F513 User (`{userId}`) was automatically unbanned by {userMention(mod)} after a tempban for {banTime}"

        CHANNEL_CREATE: |-
            **CHANNEL CREATED**
            <#{channel.id}> | {channel.name} | {channel.id}
        CHANNEL_DELETE: |-
          **CHANNEL DELETED**
          {channel.name} | {channel.id}
        CHANNEL_EDIT: '✏ Channel {channelMention(channel)} was edited'

        ROLE_CREATE: |-
          **ROLE CREATED**
          {role.name} | {role.id}
        ROLE_DELETE: |-
          **ROLE DELETED**
          {role.name} | {role.id}
        ROLE_EDIT: |-
          **ROLE EDITED**
          {role.name} | {role.id}

        MESSAGE_EDIT: |-
            :pencil: **MESSAGE EDITED**
            ------------------
            <:iconmembers:778932116024459275> **USER**
            <@!{user.id}> | `{user.username}#{user.discriminator}` | `{user.id}`
            ------------------
            <:channeltext:779036156175188001> **CHANNEL**
            <#{channel.id}> | `{channel.id}`
            ------------------
            <:updateMessage:843822776515297280> **MESSAGE**
            <https://discord.com/channels/736198286813167669/{channel.id}/{after.id}>
            **Before:**{messageSummary(before)}**After:**{messageSummary(after)}
        MESSAGE_DELETE: |-
          <:iconsystemx:842172192418693173> **MESSAGE DELETED**
          ------------------
          <:iconmembers:778932116024459275> **USER**
          <@!{user.id}> | `{user.username}#{user.discriminator}` | `{user.id}`
          ------------------
          <:channeltext:779036156175188001> **CHANNEL**
          <#{channel.id}> | `{channel.id}`
          ------------------
          <:deleteMessage:843820564741488671> **MESSAGE**
          `{message.id}`
          {messageSummary(message)}
        MESSAGE_DELETE_BULK: "\U0001F5D1 **{count}** messages by {authorIds} deleted in {channelMention(channel)} ({archiveUrl})"
        MESSAGE_DELETE_BARE: "\U0001F5D1 Message (`{messageId}`) deleted in {channelMention(channel)} (no more info available)"
        MESSAGE_DELETE_AUTO: "\U0001F5D1 Auto-deleted message (`{message.id}`) from {userMention(user)} in {channelMention(channel)} (originally posted at **{messageDate}**):{messageSummary(message)}"

        VOICE_CHANNEL_JOIN: |-
            <:iconundeafened:837072274527485983> **VC JOIN**
            ------------------
            <:iconmembers:778932116024459275> **USER**
            <@!{member.id}> | `{member.user.username}#{member.user.discriminator}` | `{member.id}`
            ------------------
            <:iconmembers:778932116024459275> **CHANNEL**
            <#{channel.id}> | {channel.name} | {channel.id}
        VOICE_CHANNEL_MOVE: "\U0001F399 ↔ {userMention(member)} moved from {channelMention(oldChannel)} to {channelMention(newChannel)}"
        VOICE_CHANNEL_LEAVE: |-
            <:icondeafened:837072274086953000> **VC LEAVE**
            ------------------
            <:iconmembers:778932116024459275> **USER**
            <@!{member.id}> | `{member.user.username}#{member.user.discriminator}` | `{member.id}`
            ------------------
            <:iconmembers:778932116024459275> **CHANNEL**
            <#{channel.id}> | {channel.name} | {channel.id}
        VOICE_CHANNEL_FORCE_MOVE: "\U0001F399 ✍ {userMention(member)} was moved from **{oldChannel.name}** to **{newChannel.name}** by {userMention(mod)}"
        VOICE_CHANNEL_FORCE_DISCONNECT: "\U0001F399 \U0001F6AB {userMention(member)} was forcefully disconnected from **{oldChannel.name}** by {userMention(mod)}"


        COMMAND: "\U0001F916 {userMention(member)} used command in {channelMention(channel)}:\n`{command}`"

        MESSAGE_SPAM_DETECTED: "\U0001F6D1 {userMention(member)} spam detected in {channelMention(channel)}: {description} (more than {limit} in {interval}s)\n{archiveUrl}"
        OTHER_SPAM_DETECTED: "\U0001F6D1 {userMention(member)} spam detected: {description} (more than {limit} in {interval}s)"

        CENSOR: "\U0001F6D1 Censored message (`{message.id}`) from {userMention(user)} in {channelMention(channel)}: {reason}:\n```{messageText}```"

        CLEAN: "\U0001F6BF {userMention(mod)} cleaned **{count}** message(s) in {channelMention(channel)}\n{archiveUrl}"

        CASE_CREATE: >-
          ✏ {userMention(mod)} manually created new **{caseType}** case
          (#{caseNum})
        CASE_DELETE: '✂️ **Case #{case.case_number}** was deleted by {userMention(mod)}'

        MASSUNBAN: '⚒ {userMention(mod)} mass-unbanned {count} users'
        MASSBAN: '⚒ {userMention(mod)} massbanned {count} users'
        MASSMUTE: "\U0001F4E2\U0001F6AB {userMention(mod)} massmuted {count} users"

        MEMBER_JOIN_WITH_PRIOR_RECORDS: |-
          ⚠ {userMention(member)} joined with prior records. Recent cases:
          {recentCaseSummary}

        CASE_UPDATE: |-
          ✏ {userMention(mod)} updated case #{caseNumber} ({caseType}) with note:
          ```{note}```

        MEMBER_MUTE_REJOIN: '⚠ Reapplied active mute for {userMention(member)} on rejoin'


        SCHEDULED_MESSAGE: >-
          ⏰ {userMention(author)} scheduled a message to be posted to
          {channelMention(channel)} on {datetime}
        SCHEDULED_REPEATED_MESSAGE: >-
          ⏰ {userMention(author)} scheduled a message to be posted to
          {channelMention(channel)} on {datetime}, repeated {repeatDetails}
        REPEATED_MESSAGE: >-
          ⏰ {userMention(author)} scheduled a message to be posted to
          {channelMention(channel)} {repeatDetails}
        POSTED_SCHEDULED_MESSAGE: "\U0001F4E8 Posted scheduled message (`{messageId}`) to {channelMention(channel)} as scheduled by {userMention(author)}"

        BOT_ALERT: '⚠ **BOT ALERT:** {tmplEval(body)}'

        DM_FAILED: "\U0001F6A7 Failed to send DM ({source}) to {userMention(user)}"

        AUTOMOD_ACTION: |-
            <:iconsearch:778925668536811520> **AUTOMOD ACTION**
            ------------------
            **RULE**
            {rule}
            ------------------
            <:iconmembers:778932116024459275> **USER**
            <@!{user.id}> | `{user.username}#{user.discriminator}` | `{user.id}`
            ------------------
            <:iconsettings:778931333459738626> **ACTION**
            {actionsTaken}
            ------------------
            **MESSAGE**
            {matchSummary}

        SET_ANTIRAID_USER: |-
            <:iconrole:826477127209320534> **ANTI-RAID**
            ------------------
            <:iconmembers:778932116024459275> **USER**
            <@!{user.id}> | `{user.username}#{user.discriminator}` | `{user.id}`
            ------------------
            <:iconconnection:778931450451984395> **ANTI-RAID**
            {level}
        SET_ANTIRAID_AUTO: |-
            <:iconrole:826477127209320534> **AUTO ANTI-RAID**
            ------------------
            <:iconconnection:778931450451984395> **ANTI-RAID**
            {level}

      ping_user: false
      allow_user_mentions: false
      #timestamp_format: string
      include_embed_timestamp: true
    overrides:
      - level: '>=50'
        config:
          ping_user: false
```
</details>

---

#### PRETTY LOGS VERSION 3.0 (PLAIN EDITION)

<details>
  <summary>Click to view code!</summary>

```yaml
  logs:
    config:
      channels:
        '808334772102234142': #misc
          exclude:
           - MEMBER_JOIN
           - MEMBER_LEAVE
           - AUTOMOD_ACTION
          excluded_categories:
            - "855775275228987403" #manager category
          exclude_bots: true

        '857908693567930398': #joins/leaves
          include:
           - MEMBER_JOIN
           - MEMBER_LEAVE
           - MEMBER_RESTORE
          excluded_categories:
            - "855775275228987403" #manager category
          exclude_bots: true

        '858001035360862218': #automod
          include:
           - AUTOMOD_ACTION

          excluded_categories:
            - "855775275228987403" #manager category
          exclude_bots: true
      format:
        timestamp: ""
        MEMBER_NOTE: |-
          :notepad_spiral: **NOTE**
          <:profile:841364699958607894><:dash:855062799659171850><@!{user.id}><:dot:855062799607529472>**{user.username}#{user.discriminator}**
          <:iconid:778924898176466944><:dash:855062799659171850>`{user.id}`

          <:mod:855081145788006460><:dash:855062799659171850><@!{mod.id}><:dot:855062799607529472>**{mod.username}#{mod.discriminator}**
          <:iconid:778924898176466944><:dash:855062799659171850>`{mod.id}`
          
          <:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460>

        MEMBER_WARN: |-
          :warning: **MEMBER WARNED**
          <:profile:841364699958607894><:dash:855062799659171850><@!{member.id}><:dot:855062799607529472>**{member.user.username}#{member.user.discriminator}**
          <:iconid:778924898176466944><:dash:855062799659171850>`{member.id}`

          <:mod:855081145788006460><:dash:855062799659171850><@!{mod.id}><:dot:855062799607529472>**{mod.username}#{mod.discriminator}**
          <:iconid:778924898176466944><:dash:855062799659171850>`{mod.id}`
          <:iconsupport:778924718153662495><:dash:855062799659171850>{reason}
          
          <:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460>

        MEMBER_MUTE: |-
          <:iconmuted:837072273978294283> **MEMBER MUTED INDEFINITELY**
          <:profile:841364699958607894><:dash:855062799659171850><@!{user.id}><:dot:855062799607529472>**{user.username}#{user.discriminator}**
          <:iconid:778924898176466944><:dash:855062799659171850>`{user.id}`

          <:mod:855081145788006460><:dash:855062799659171850><@!{mod.id}><:dot:855062799607529472>**{mod.username}#{mod.discriminator}**
          <:iconid:778924898176466944><:dash:855062799659171850>`{mod.id}`
          <:iconsupport:778924718153662495><:dash:855062799659171850>{reason}
          
          <:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460>

        MEMBER_TIMED_MUTE: |-
          <:iconmuted:837072273978294283> **MEMBER MUTED** ({time})
          <:profile:841364699958607894><:dash:855062799659171850><@!{user.id}><:dot:855062799607529472>**{user.username}#{user.discriminator}**
          <:iconid:778924898176466944><:dash:855062799659171850>`{user.id}`

          <:mod:855081145788006460><:dash:855062799659171850><@!{mod.id}><:dot:855062799607529472>**{mod.username}#{mod.discriminator}**
          <:iconid:778924898176466944><:dash:855062799659171850>`{mod.id}`
          <:iconsupport:778924718153662495><:dash:855062799659171850>{reason}
          <:iconclock:811925897036038165><:dash:855062799659171850>{time}
          
          <:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460>

        MEMBER_UNMUTE: |-
          <:iconunmuted:837072274766823456> **MEMBER UNMUTED**
          <:profile:841364699958607894><:dash:855062799659171850><@!{user.id}><:dot:855062799607529472>**{user.username}#{user.discriminator}**
          <:iconid:778924898176466944><:dash:855062799659171850>`{user.id}`

          <:mod:855081145788006460><:dash:855062799659171850><@!{mod.id}><:dot:855062799607529472>**{mod.username}#{mod.discriminator}**
          <:iconid:778924898176466944><:dash:855062799659171850>`{mod.id}`
          
          <:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460>

        MEMBER_TIMED_UNMUTE: |-
          <:iconunmuted:837072274766823456> **MEMBER TIMED UNMUTED** ({time})
          <:profile:841364699958607894><:dash:855062799659171850><@!{user.id}><:dot:855062799607529472>**{user.username}#{user.discriminator}**
          <:iconid:778924898176466944><:dash:855062799659171850>`{user.id}`

          <:mod:855081145788006460><:dash:855062799659171850><@!{mod.id}><:dot:855062799607529472>**{mod.username}#{mod.discriminator}**
          <:iconid:778924898176466944><:dash:855062799659171850>`{mod.id}`
          <:iconclock:811925897036038165><:dash:855062799659171850>{time}
          
          <:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460>

        MEMBER_MUTE_EXPIRED: |-
          <:iconunmuted:837072274766823456> **MEMBER EXPIRED**
          <:profile:841364699958607894><:dash:855062799659171850><@!{member.id}><:dot:855062799607529472>**{member.user.username}#{member.user.discriminator}**
          <:iconid:778924898176466944><:dash:855062799659171850>`{member.id}`
          
          <:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460>

        MEMBER_KICK: |-
          :boot: **MEMBER KICKED**
          <:profile:841364699958607894><:dash:855062799659171850><@!{user.id}><:dot:855062799607529472>**{user.username}#{user.discriminator}**
          <:iconid:778924898176466944><:dash:855062799659171850>`{user.id}`

          <:mod:855081145788006460><:dash:855062799659171850><@!{mod.id}><:dot:855062799607529472>**{mod.username}#{mod.discriminator}**
          <:iconid:778924898176466944><:dash:855062799659171850>`{mod.id}`
          
          <:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460>

        MEMBER_BAN: |-
          <:leave:754438854961922069> **MEMBER BANNED**
          <:profile:841364699958607894><:dash:855062799659171850><@!{user.id}><:dot:855062799607529472>**{user.username}#{user.discriminator}**
          <:iconid:778924898176466944><:dash:855062799659171850>`{user.id}`

          <:mod:855081145788006460><:dash:855062799659171850><@!{mod.id}><:dot:855062799607529472>**{mod.username}#{mod.discriminator}**
          <:iconid:778924898176466944><:dash:855062799659171850>`{mod.id}`
          
          <:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460>

        MEMBER_UNBAN: |-
          <:statusonline:714853868420202529> **MEMBER UNBANNED**
          <:iconid:778924898176466944><:dash:855062799659171850>`{user.id}`

          <:mod:855081145788006460><:dash:855062799659171850><@!{mod.id}><:dot:855062799607529472>**{mod.username}#{mod.discriminator}**
          <:iconid:778924898176466944><:dash:855062799659171850>`{mod.id}`
          
          <:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460>

        MEMBER_FORCEBAN: |-
          <:leave:754438854961922069> **MEMBER FORCEBANNED**
          <:iconid:778924898176466944><:dash:855062799659171850>`{user.id}`

          <:mod:855081145788006460><:dash:855062799659171850><@!{mod.id}><:dot:855062799607529472>**{mod.username}#{mod.discriminator}**
          <:iconid:778924898176466944><:dash:855062799659171850>`{mod.id}`
          
          <:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460>

        MEMBER_SOFTBAN: |-
          <:leave:754438854961922069> **MEMBER SOFTBANNED**
          <:profile:841364699958607894><:dash:855062799659171850><@!{member.id}><:dot:855062799607529472>**{member.user.username}#{member.user.discriminator}**
          <:iconid:778924898176466944><:dash:855062799659171850>`{member.id}`

          <:mod:855081145788006460><:dash:855062799659171850><@!{mod.id}><:dot:855062799607529472>**{mod.username}#{mod.discriminator}**
          <:iconid:778924898176466944><:dash:855062799659171850>`{mod.id}`
          
          <:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460>


        MEMBER_JOIN: |-
          <:join:754438854487965807> **MEMBER JOINED**
          <:profile:841364699958607894><:dash:855062799659171850><@!{member.id}><:dot:855062799607529472>**{member.user.username}#{member.user.discriminator}**
          <:iconid:778924898176466944><:dash:855062799659171850>`{member.id}`
          <:iconclock:811925897036038165><:dash:855062799659171850>created {account_age} ago
          
          <:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460>

        MEMBER_LEAVE: |-
          <:leave:754438854961922069> **MEMBER LEFT**
          <:profile:841364699958607894><:dash:855062799659171850><@!{member.id}><:dot:855062799607529472>**{member.user.username}#{member.user.discriminator}**
          <:iconid:778924898176466944><:dash:855062799659171850>`{member.id}`
          <:join:754438854487965807><:dash:855062799659171850><t:{rand(div(member.joinedAt, 1000), div(member.joinedAt, 1000))}> (<t:{rand(div(member.joinedAt, 1000), div(member.joinedAt, 1000))}:R>)
          
          <:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460>


        MEMBER_ROLE_ADD: |-
          <:statusonline:714853868420202529> **ROLE ADDED**
          <:profile:841364699958607894><:dash:855062799659171850><@!{member.id}><:dot:855062799607529472>**{member.user.username}#{member.user.discriminator}**
          <:iconid:778924898176466944><:dash:855062799659171850>`{member.id}`

          <:mod:855081145788006460><:dash:855062799659171850><@!{mod.id}><:dot:855062799607529472>**{mod.username}#{mod.discriminator}**
          <:iconid:778924898176466944><:dash:855062799659171850>`{mod.id}`
          <:iconrole:826477127209320534>`{roles}`
          
          <:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460>

        MEMBER_ROLE_REMOVE: |-
          <:statusdnd:714833495524114464> **ROLE REMOVED**
          <:profile:841364699958607894><:dash:855062799659171850><@!{member.id}><:dot:855062799607529472>**{member.user.username}#{member.user.discriminator}**
          <:iconid:778924898176466944><:dash:855062799659171850>`{member.id}`

          <:mod:855081145788006460><:dash:855062799659171850><@!{mod.id}><:dot:855062799607529472>**{mod.username}#{mod.discriminator}**
          <:iconid:778924898176466944><:dash:855062799659171850>`{mod.id}`
          <:iconrole:826477127209320534>`{roles}`
          
          <:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460>

        MEMBER_ROLE_CHANGES: |-
          :pencil: **ROLE CHANGES**
          <:profile:841364699958607894><:dash:855062799659171850><@!{member.id}><:dot:855062799607529472>**{member.user.username}#{member.user.discriminator}**
          <:iconid:778924898176466944><:dash:855062799659171850>`{member.id}`

          <:mod:855081145788006460><:dash:855062799659171850><@!{mod.id}><:dot:855062799607529472>**{mod.username}#{mod.discriminator}**
          <:iconid:778924898176466944><:dash:855062799659171850>`{mod.id}`
          <:iconrole:826477127209320534><:join:754438854487965807><:dash:855062799659171850>{addedRoles}
          <:iconrole:826477127209320534><:leave:754438854961922069><:dash:855062799659171850>{addedRoles}{removedRoles}
          
          <:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460>

        MEMBER_NICK_CHANGE: |-
          ✏ **NICKNAME CHANGE**
          <:profile:841364699958607894><:dash:855062799659171850><@!{member.id}><:dot:855062799607529472>**{member.user.username}#{member.user.discriminator}**
          <:iconid:778924898176466944><:dash:855062799659171850>`{member.id}`
          `{oldNick}` to `{newNick}`
          
          <:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460>

        MEMBER_USERNAME_CHANGE: |-
          ✏ **USERNAME CHANGE**
          <:profile:841364699958607894><:dash:855062799659171850><@!{user.id}><:dot:855062799607529472>**{user.username}#{user.discriminator}**
          <:iconid:778924898176466944><:dash:855062799659171850>`{user.id}`
          ------------------
          `{oldName}` to `{newName}`
          
          <:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460>

        MEMBER_RESTORE: |-
          <:downloadupdate:758794223176384512> **MEMBER RE-JOIN**
          <:profile:841364699958607894><:dash:855062799659171850><@!{member.id}><:dot:855062799607529472>**{member.user.username}#{member.user.discriminator}**
          <:iconid:778924898176466944><:dash:855062799659171850>`{member.id}`

          {restoredData}
          
          <:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460>

        MEMBER_TIMED_BAN: |-
          :hammer: **TEMP BAN**
          <:profile:841364699958607894><:dash:855062799659171850><@!{user.id}><:dot:855062799607529472>**{user.username}#{user.discriminator}**
          <:iconid:778924898176466944><:dash:855062799659171850>`{user.id}`

          <:mod:855081145788006460><:dash:855062799659171850><@!{mod.id}><:dot:855062799607529472>**{mod.username}#{mod.discriminator}**
          <:iconid:778924898176466944><:dash:855062799659171850>`{mod.id}`
          <:iconclock:811925897036038165><:dash:855062799659171850>{banTime}
          
          <:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460>

        MEMBER_TIMED_UNBAN: |-
          <:statusonline:714853868420202529> **TEMP UNBAN** ({banTime})
          <:iconid:778924898176466944><:dash:855062799659171850>`{user.id}`

          <:mod:855081145788006460><:dash:855062799659171850><@!{mod.id}><:dot:855062799607529472>**{mod.username}#{mod.discriminator}**
          <:iconid:778924898176466944><:dash:855062799659171850>`{mod.id}`
          <:iconclock:811925897036038165><:dash:855062799659171850>{banTime}
          
          <:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460>


        CHANNEL_CREATE: |-
          <:statusonline:714853868420202529> **CHANNEL CREATED**
          <:channeltext:779036156175188001><:dash:855062799659171850>**{channel.name}**<:dot:855062799607529472>`{channel.id}`
          
          <:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460>

        CHANNEL_DELETE: |-
          :x: **CHANNEL DELETED**
          <:channeltext:779036156175188001><:dash:855062799659171850>**{channel.name}**<:dot:855062799607529472>`{channel.id}`
          
          <:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460>

        CHANNEL_EDIT: |-
          :pencil: **CHANNEL EDITED**
          <:channeltext:779036156175188001><:dash:855062799659171850><#{channel.id}><:dot:855062799607529472>**{channel.name}**<:dot:855062799607529472>`{channel.id}`
          
          <:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460>

        #roles
        ROLE_CREATE: |-
          <:statusonline:714853868420202529> **ROLE CREATED**
          {role.name}<:dot:855062799607529472>`{role.id}`
          
          <:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460>

        ROLE_DELETE: |-
          <:statusdnd:714833495524114464> **ROLE DELETED**
          {role.name}<:dot:855062799607529472>`{role.id}`
          
          <:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460>

        ROLE_EDIT: |-
          :pencil: **ROLE EDITED**
          {role.name}<:dot:855062799607529472>`{role.id}`
          
          <:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460>

        #Messages

        MESSAGE_EDIT: |-
          :pencil: **MESSAGE EDITED**
          <:profile:841364699958607894><:dash:855062799659171850><@!{user.id}><:dot:855062799607529472>**{user.username}#{user.discriminator}**
          <:iconid:778924898176466944><:dash:855062799659171850>`{user.id}`
          <:channeltext:779036156175188001><:dash:855062799659171850><#{channel.id}><:dot:855062799607529472>`{channel.id}`
          <:iconrichpresence:842328614883295232>
          <https://discord.com/channels/736198286813167669/{channel.id}/{after.id}>
          **Before:**{messageSummary(before)}**After:**{messageSummary(after)}
          
          <:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460>

        MESSAGE_DELETE: |-
          <:iconsystemx:842172192418693173> **MESSAGE DELETED**
          <:profile:841364699958607894><:dash:855062799659171850><@!{user.id}><:dot:855062799607529472>**{user.username}#{user.discriminator}**
          <:iconid:778924898176466944><:dash:855062799659171850>`{user.id}`
          <:channeltext:779036156175188001><:dash:855062799659171850><#{channel.id}><:dot:855062799607529472>`{channel.id}`
          <:iconrichpresence:842328614883295232><:dash:855062799659171850>`{message.id}`
          {messageSummary(message)}
          
          <:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460>

        MESSAGE_DELETE_BULK: |-
          <:iconsystemx:842172192418693173> **{count} BULK DELETED**
          <:profile:841364699958607894><:dash:855062799659171850>{authorIds}
          <:channeltext:779036156175188001><:dash:855062799659171850><#{channel.id}><:dot:855062799607529472>`{channel.id}`
          <:iconrichpresence:842328614883295232><:dash:855062799659171850>{archiveUrl}
          
          <:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460>

        MESSAGE_DELETE_BARE: |-
          <:iconsystemx:842172192418693173> **MESSAGE DELETED BARE**
          <:channeltext:779036156175188001><:dash:855062799659171850><#{channel.id}><:dot:855062799607529472>`{channel.id}`
          <:iconrichpresence:842328614883295232><:dash:855062799659171850>{messageId}
          
          <:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460>

        MESSAGE_DELETE_AUTO: |-
          <:trashcan:750152850310561853> **AUTO DELETE**
          <:profile:841364699958607894><:dash:855062799659171850><@!{user.id}><:dot:855062799607529472>**{user.username}#{user.discriminator}**
          <:iconid:778924898176466944><:dash:855062799659171850>`{user.id}`
          <:channeltext:779036156175188001><:dash:855062799659171850><#{channel.id}><:dot:855062799607529472>`{channel.id}`
          <:iconrichpresence:842328614883295232><:dash:855062799659171850>`{message.id}`
          {messageSummary(message)}
          
          <:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460>

        VOICE_CHANNEL_JOIN: |-
          <:join:754438854487965807> **VC JOIN**
          <:profile:841364699958607894><:dash:855062799659171850><@!{member.id}><:dot:855062799607529472>**{member.user.username}#{member.user.discriminator}**
          <:iconid:778924898176466944><:dash:855062799659171850>`{member.id}`
          <:channeltext:779036156175188001><:dash:855062799659171850><#{channel.id}><:dot:855062799607529472>**{channel.name}**<:dot:855062799607529472>`{channel.id}`
          
          <:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460>

        VOICE_CHANNEL_MOVE: |-
          <:iconundeafened:837072274527485983> **VC MOVE**
          <:profile:841364699958607894><:dash:855062799659171850><@!{member.id}><:dot:855062799607529472>**{member.user.username}#{member.user.discriminator}**
          <:iconid:778924898176466944><:dash:855062799659171850>`{member.id}`
          <:leave:754438854961922069><:dash:855062799659171850>**{oldChannel.name}**<:dot:855062799607529472>`{oldChannel.id}`
          <:join:754438854487965807><:dash:855062799659171850>**{newChannel.name}**<:dot:855062799607529472>`{newChannel.id}`
          
          <:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460>

        VOICE_CHANNEL_LEAVE: |-
          <:leave:754438854961922069> **VC LEAVE**
          <:profile:841364699958607894><:dash:855062799659171850><@!{member.id}><:dot:855062799607529472>**{member.user.username}#{member.user.discriminator}**
          <:iconid:778924898176466944><:dash:855062799659171850>`{member.id}`
          <:channeltext:779036156175188001><:dash:855062799659171850><#{channel.id}><:dot:855062799607529472>**{channel.name}**<:dot:855062799607529472>`{channel.id}`
          
          <:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460>
        VOICE_CHANNEL_FORCE_MOVE: |-
          <:iconundeafened:837072274527485983> **VC FORCE MOVE**
          <:profile:841364699958607894><:dash:855062799659171850><@!{member.id}><:dot:855062799607529472>**{member.user.username}#{member.user.discriminator}**
          <:iconid:778924898176466944><:dash:855062799659171850>`{member.id}`

          <:mod:855081145788006460><:dash:855062799659171850><@!{mod.id}><:dot:855062799607529472>**{mod.username}#{mod.discriminator}**
          <:iconid:778924898176466944><:dash:855062799659171850>`{mod.id}`

          <:channeltext:779036156175188001><:dash:855062799659171850><#{oldchannel.id}><:dot:855062799607529472>**{oldChannel.name}**<:dot:855062799607529472>`{oldChannel.id}`
          <:channeltext:779036156175188001><:dash:855062799659171850><#{newldchannel.id}><:dot:855062799607529472>**{newChannel.name}**<:dot:855062799607529472>`{newChannel.id}`
          
          <:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460>

        VOICE_CHANNEL_FORCE_DISCONNECT: |-
          <:icondeafened:837072274086953000> **VC FORCE DISCONNECT**
          <:profile:841364699958607894><:dash:855062799659171850><@!{member.id}><:dot:855062799607529472>**{member.user.username}#{member.user.discriminator}**
          <:iconid:778924898176466944><:dash:855062799659171850>`{member.id}`

          <:mod:855081145788006460><:dash:855062799659171850><@!{mod.id}><:dot:855062799607529472>**{mod.username}#{mod.discriminator}**
          <:iconid:778924898176466944><:dash:855062799659171850>`{mod.id}`

          <:channeltext:779036156175188001><:dash:855062799659171850>**{oldChannel.name}**<:dot:855062799607529472>`{oldChannel.id}`
          
          <:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460>



        #COMMAND: "\U0001F916 {userMention(member)} used command in {channelMention(channel)}:\n`{command}`"
        #unused in zep atm


        MESSAGE_SPAM_DETECTED: "\U0001F6D1 {userMention(member)} spam detected in {channelMention(channel)}: {description} (more than {limit} in {interval}s)\n{archiveUrl}"

        OTHER_SPAM_DETECTED: "\U0001F6D1 {userMention(member)} spam detected: {description} (more than {limit} in {interval}s)"

        CLEAN: |-
          :soap: **{count} MESSAGES CLEANED**
          <:profile:841364699958607894><:dash:855062799659171850><@!{mod.id}><:dot:855062799607529472>**{mod.username}#{mod.discriminator}**<:dot:855062799607529472>`{mod.id}`
          <:channeltext:779036156175188001><:dash:855062799659171850><#{channel.id}><:dot:855062799607529472>`{channel.id}`
          <:iconrichpresence:842328614883295232><:dash:855062799659171850>{archiveUrl}
          
          <:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460>


        CASE_CREATE: >-
          ✏ {userMention(mod)} manually created new **{caseType}** case
          (#{caseNum})

        CASE_DELETE: |-
          <:statusdnd:714833495524114464> **CASE DELETED**
          <:profile:841364699958607894><:dash:855062799659171850><@!{mod.id}><:dot:855062799607529472>`{mod.id}`
          <:channeltext:779036156175188001><:dash:855062799659171850>**Case#{case.case_number}**
          
          <:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460>


        MASSUNBAN: '⚒ {userMention(mod)} mass-unbanned {count} users'

        MASSBAN: '⚒ {userMention(mod)} massbanned {count} users'

        MASSMUTE: "\U0001F4E2\U0001F6AB {userMention(mod)} massmuted {count} users"

        MEMBER_JOIN_WITH_PRIOR_RECORDS: |-
          ⚠ {userMention(member)} joined with prior records. Recent cases:
          {recentCaseSummary}
          
          <:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460>

        CASE_UPDATE: |-
          ✏ {userMention(mod)} updated case #{caseNumber} ({caseType}) with note:
          ```{note}```

        MEMBER_MUTE_REJOIN: |-
          <:icondeafened:837072274086953000> **MEMBER MUTE RE-JOIN**
          <:profile:841364699958607894><:dash:855062799659171850><@!{member.id}><:dot:855062799607529472>**{member.user.username}#{member.user.discriminator}**
          <:iconid:778924898176466944><:dash:855062799659171850>`{member.id}`
          
          <:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460>

        SCHEDULED_MESSAGE: >-
          ⏰ {userMention(author)} scheduled a message to be posted to
          {channelMention(channel)} on {datetime}

        SCHEDULED_REPEATED_MESSAGE: >-
          ⏰ {userMention(author)} scheduled a message to be posted to
          {channelMention(channel)} on {datetime}, repeated {repeatDetails}

        REPEATED_MESSAGE: >-
          ⏰ {userMention(author)} scheduled a message to be posted to
          {channelMention(channel)} {repeatDetails}

        POSTED_SCHEDULED_MESSAGE: "\U0001F4E8 Posted scheduled message (`{messageId}`) to {channelMention(channel)} as scheduled by {userMention(author)}"

        BOT_ALERT: |-
          :warning: **BOT ALERT**
          {tmplEval(body)}
          
          <:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460>

        DM_FAILED: "\U0001F6A7 Failed to send DM ({source}) to {userMention(user)}"

        AUTOMOD_ACTION: |-
          <:iconsearch:778925668536811520> **AUTOMOD ACTION**
          <:iconprivacysettings:845090111976636446><:dash:855062799659171850>{rule}
          <:profile:841364699958607894><:dash:855062799659171850><@!{user.id}><:dot:855062799607529472>**{user.username}#{user.discriminator}**
          <:iconid:778924898176466944><:dash:855062799659171850>`{user.id}`
          <:iconsettings:778931333459738626><:dash:855062799659171850>{actionsTaken}
          <:iconrichpresence:842328614883295232><:dash:855062799659171850>{matchSummary}
          
          <:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460>

        SET_ANTIRAID_USER: |-
          <:iconrole:826477127209320534> **ANTI-RAID**
          <:profile:841364699958607894><:dash:855062799659171850><@!{user.id}><:dot:855062799607529472>**{user.username}#{user.discriminator}**
          <:iconid:778924898176466944><:dash:855062799659171850>`{user.id}`
          <:iconconnection:778931450451984395><:dash:855062799659171850>**{level}**
          
          <:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460>

        SET_ANTIRAID_AUTO: |-
          <:iconrole:826477127209320534> **AUTO ANTI-RAID**
          <:iconconnection:778931450451984395> **ANTI-RAID**
          {level}
          
          <:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460>

      ping_user: false
      allow_user_mentions: false
      #timestamp_format: string
      include_embed_timestamp: true
    overrides:
      - level: '>=50'
        config:
          ping_user: false

```
</details>

---

#### PRETTY LOGS (EMBED EDITION)

<details>
  <summary>Click to view code!</summary>

```yaml
# - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
      format:
        timestamp: 'DD-MM-YYYY HH:mm:ss'
        # welcome-log
        MEMBER_JOIN:
          embed:
            author:
              name: '{member.user.username}#{member.user.discriminator}'
              url: Null
            title: 'MEMBER JOINED'
            description: |-
              **User:** <@{member.id}> 
              **Created:** {account_age} ago
            image:
              url: 'https://cdn.discordapp.com/attachments/670339348956446772/808055881966813234/embed_width.png'
            footer:
              text: 'UserID: {member.id} • Time: {timestamp}UTC'
            color: 0x2EFF27 #green
            thumbnail:
              url: 'https://cdn.discordapp.com/attachments/670339348956446772/808292686691172392/inbox_tray.png'
        
        MEMBER_LEAVE:
          embed:
            author:
              name: '{member.user.username}#{member.user.discriminator}'
              url: Null
            title: 'MEMBER LEFT'
            description: |-
              **User:** <@{member.id}> left the server
            image: 
              url: 'https://cdn.discordapp.com/attachments/670339348956446772/808055881966813234/embed_width.png'
            footer:
              text: 'UserID: {member.id} • Time: {timestamp}UTC'
            color: 0xFFA027 #orange
            thumbnail:
              url: 'https://cdn.discordapp.com/attachments/670339348956446772/808292702202363954/outbox_tray.png'
        
        MEMBER_KICK:
          embed:
            author:
              name: '{user.username}#{user.discriminator}'
            title: 'MEMBER KICKED'
            description: |-
              User: <@{user.id}> 
              By: <@{mod.id}>
            image: 
              url: 'https://cdn.discordapp.com/attachments/670339348956446772/808055881966813234/embed_width.png'
            footer:
              text: 'UserID: {member.id} • Time: {timestamp}UTC'
            color: 0xFF2727 #red
        
        MEMBER_JOIN_WITH_PRIOR_RECORDS:
          embed:
            author:
              name: '{member.user.username}#{member.user.discriminator}'
            title: 'JOIN WITH PRIOR RECORDS'
            description: |-
              **User:** {new} <@{member.id}>
              **Created:** {account_age}
              **Recent cases:**
              {recentCaseSummary}
            image:
              url: 'https://cdn.discordapp.com/attachments/670339348956446772/808055881966813234/embed_width.png'
            footer:
              text: 'UserID: {member.id} • Time: {timestamp}UTC'
            color: 0xFF2727 #red
            thumbnail:
              url: 'https://cdn.discordapp.com/attachments/670339348956446772/808292686691172392/inbox_tray.png'
        
        MEMBER_BAN:
          embed:
            author:
              name: '{user.username}#{user.discriminator}'
            title: 'MEMBER BANNED'
            description: |-
              **User:** <@{user.id}>
              **By:** <@{mod.id}>
            image:
              url: 'https://cdn.discordapp.com/attachments/670339348956446772/808055881966813234/embed_width.png'
            footer:
              text: 'UserID: {member.id} • Time: {timestamp}UTC'
            color: 0xFF2727 #red
        
        MEMBER_FORCEBAN:
          embed:
            author:
              name: '{user.username}#{user.discriminator}'
            title: 'MEMBER FORCE BANNED'
            description: |-
              **User:** <@{user.id}>
              **By:** <@{mod.id}>
            image:
              url: 'https://cdn.discordapp.com/attachments/670339348956446772/808055881966813234/embed_width.png'
            footer:
              text: 'UserID: {member.id} • Time: {timestamp}UTC'
            color: 0xFF2727 #red
        
        MASSBAN:
          embed:
            title: 'MASSBAN'
            description: |-
              {count} users were massbanned
              **By:** <@{mod.id}>
            image:
              url: 'https://cdn.discordapp.com/attachments/670339348956446772/808055881966813234/embed_width.png'
            footer:
              text: 'Time: {timestamp}UTC'
            color: 0x000000 #black
        
        MEMBER_SOFTBAN:
          embed:
            author:
              name: '{user.username}#{user.discriminator}'
            title: 'MEMBER SOFT BANNED'
            description: |-
              **User:** <@{user.id}>
              **By:** <@{mod.id}>
            image: 
              url: 'https://cdn.discordapp.com/attachments/670339348956446772/808055881966813234/embed_width.png'
            footer:
              text: 'UserID: {user.id} • Time: {timestamp}UTC'
            color: 0xFFA027 #orange
        
        MEMBER_MUTE_REJOIN:
          embed:
            author:
              name: '{member.user.username}#{member.user.discriminator}'
            title: 'MUTED MEMBER REJOIN'
            description: |-
              Reapplied active mute on rejoin
              **User:** <@{member.id}>
            image:
              url: 'https://cdn.discordapp.com/attachments/670339348956446772/808055881966813234/embed_width.png'
            footer:
              text: 'UserID: {member.id} • Time: {timestamp}UTC'
            color: 0xFF2727 #red
# - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
        # auto-log
        AUTOMOD_ACTION:
          embed:
            title: '{user.username}#{user.discriminator}'
            fields:
            -  name : '**Type:**'
               value : '{rule}'
               inline : true
            -  name : '**Mention:**'
               value : '<@{user.id}>'
               inline : true
            -  name : '**Action:**'
               value : '{actionsTaken}'
               inline : true
            -  name: '**Match:**'
               value: '{matchSummary}'
               inline : false
            image: 
              url: 'https://cdn.discordapp.com/attachments/670339348956446772/808055881966813234/embed_width.png'
            footer:
              text: 'UserID: {user.id} • Time: {timestamp}UTC'
            color: 0xFF2727 #red
# - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
        # msg-log
        DM_FAILED:
          embed:
            author:
              name: '{user.username}#{user.discriminator}'
            title: 'DM FAILED'
            description: |-
              Failed to send DM ({source})
              **To:** <@{user.id}>
            image: 
              url: 'https://cdn.discordapp.com/attachments/670339348956446772/808055881966813234/embed_width.png'
            footer:
              text: 'UserID: {user.id} • Time: {timestamp}UTC'
            color: 0xFFA027 #orange
        
        MESSAGE_DELETE:
          embed:
            title: '{user.username}#{user.discriminator}'
            description: |-
              :wastebasket: **Message sent by <@{user.id}>  deleted in <#{channel.id}>**
              {messageSummary(message)} 
            image: 
              url: 'https://cdn.discordapp.com/attachments/670339348956446772/808055881966813234/embed_width.png'
            color: 0xFF2727 #red
            footer: 
              text: 'UserID: {user.id} • Time: {timestamp}UTC'
        
        MESSAGE_DELETE_BARE:
          embed:
            title: '{user.username}#{user.discriminator}'
            description: |-
              :wastebasket: **Message deleted in <#{channel.id}>**
              (no more info available)
            image: 
              url: 'https://cdn.discordapp.com/attachments/670339348956446772/808055881966813234/embed_width.png'
            color: 0xFF2727 #red
            footer: 
              text: 'MessageID: {message.id} • Time: {timestamp}UTC'
        
        MESSAGE_EDIT: 
          embed:
            author:
              name: '{user.username}#{user.discriminator}'
            description: |-
              :pencil: **[message](https://canary.discord.com/channels/261157716792311818/{channel.id}/{after.id}) sent by <@{user.id}> edited in <#{channel.id}>**
              **Old Message:**
              {messageSummary(before)}
              **New Message:**
              {messageSummary(after)}
            image: 
              url: 'https://cdn.discordapp.com/attachments/670339348956446772/808055881966813234/embed_width.png'
            color: 0xFFA027 #orange
            footer: 
              text: 'UserID: {user.id} • Time: {timestamp}UTC'
        
        MESSAGE_SPAM_DETECTED:
          embed:
            author:
              name: '{user.username}#{user.discriminator}'
            title: 'MESSAGE SPAM DETECTED'
            description: |-
              Message spam in <#{message.id}> by <@{member.id}>
              {description}
              (more than {limit} in {interval}s)
              {archiveUrl}
            image: 
              url: 'https://cdn.discordapp.com/attachments/670339348956446772/808055881966813234/embed_width.png'
            footer: 
              text: 'UserID: {user.id} • Time: {timestamp}UTC'
            color: 0xFFA027 #orange
        
        CLEAN:
          embed:
            title: 'MESSAGES CLEANED'
            fields:
            -  name : '**User:**'
               value : '<@{mod.id}>'
               inline : true
            -  name : '**Cleaned:**'
               value : '{count} message(s)'
               inline : true
            -  name : '**In:**'
               value : '<#{channel.id}>'
               inline : true
            -  name: '**Messages:**'
               value: '[Archive]({archiveUrl})'
               inline : true
            image: 
              url: 'https://cdn.discordapp.com/attachments/670339348956446772/808055881966813234/embed_width.png'
            footer: 
              text: 'Time: {timestamp}UTC'
            color: 0xFF2727 #red
        
        MESSAGE_DELETE_BULK:
          embed:
            title: '{count} MESSAGES DELETED'
            fields:
            -  name : '**By:**'
               value : '{authorIds}'
               inline : true
            -  name : '**In:**'
               value : '<#{channel.id}>'
               inline : true
            -  name : '**Messages:**'
               value : '[Archive]({archiveUrl})'
               inline : true
            image: 
              url: 'https://cdn.discordapp.com/attachments/670339348956446772/808055881966813234/embed_width.png'
            footer: 
              text: 'Time: {timestamp}UTC'
            color: 0xFF2727 #red
        
        POSTED_SCHEDULED_MESSAGE:
          embed:
            title: 'POSTED SCHEDULED MESSAGE'
            description: |-
              **Posted scheduled message:** (`{messageId}`)
              **To:** {channelMention(channel)}
              **Scheduled by:** {userMention(author)}
            image: 
              url: 'https://cdn.discordapp.com/attachments/670339348956446772/808055881966813234/embed_width.png'
            footer: 
              text: 'Time: {timestamp}UTC'
            color: 0x000000 #black
        
        SCHEDULED_MESSAGE:
          embed:
            title: 'SCHEDULED MESSAGE'
            description: |-
              {userMention(author)} scheduled a message
              **To be posted to:** {channelMention(channel)}
              **On: {datetime}
            image: 
              url: 'https://cdn.discordapp.com/attachments/670339348956446772/808055881966813234/embed_width.png'
            footer: 
              text: 'Time: {timestamp}UTC'
            color: 0x000000 #black
        
        SCHEDULED_REPEATED_MESSAGE:
          embed:
            title: 'SCHEDULED REPEATED MESSAGE'
            description: |-
              {userMention(author)} scheduled a message
              **To be posted to:** {channelMention(channel)}
              **On:** {datetime}
              **Repeated:** {repeatDetails}
            image: 
              url: 'https://cdn.discordapp.com/attachments/670339348956446772/808055881966813234/embed_width.png'
            footer: 
              text: 'Time: {timestamp}UTC'
            color: 0x000000 #black
        
        REPEATED_MESSAGE:
          embed:
            title: 'REPEATED MESSAGE'
            description: |-
              {userMention(author)} scheduled a message
              **To be posted to:** {channelMention(channel)}
              **Repeated:** {repeatDetails}
            image: 
              url: 'https://cdn.discordapp.com/attachments/670339348956446772/808055881966813234/embed_width.png'
            footer: 
              text: 'Time: {timestamp}UTC'
            color: 0x000000 #black
# - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
        # rank-log
        MESSAGE_DELETE_AUTO:
          embed:
            author: 
              name: '{user.username}#{user.discriminator}'
            title: 'MESSAGE AUTO-DELETED'
            fields:
            -  name : '**From:**'
               value : '<@{user.id}>'
               inline : true
            -  name : '**In:**'
               value : '<#{channel.id}>'
               inline : true
            -  name : '**Message:**'
               value : '{messageSummary(message)}'
               inline : false
            image: 
              url: 'https://cdn.discordapp.com/attachments/670339348956446772/808055881966813234/embed_width.png'
            footer: 
              text: 'UserID: {user.id} • Time: {timestamp}UTC'
            color: 0xFF2727 #red
# - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
        # name-log
        MEMBER_NICK_CHANGE:
          embed:
            author:
              name: '{member.user.username}#{member.user.discriminator}'
              url: '{user.member.avatarURL}'
            description: ':pencil: <@{member.id}> **nickname edited**'
            fields:
            -  name : '**Old Nickname**'
               value : '`{oldNick}`'
               inline : true
            -  name : '**New Nickname**'
               value : '`{newNick}`'
               inline : true
            color: 0x2744FF #blue
            footer: 
              text: 'UserID: {member.id} • Time: {timestamp}UTC'
        
        MEMBER_USERNAME_CHANGE:
          embed:
            author:
              name: '{member.user.username}#{member.user.discriminator}'
              url: '{user.member.avatarURL}'
            description: ':pencil: <@{member.id}> **username edited**'
            fields:
            -  name : '**Old Username**'
               value : '`{oldName}`'
               inline : true
            -  name : '**New Username**'
               value : '`{newName}`'
               inline : true
            color: 0x2744FF #blue
            footer: 
              text: 'UserID: {member.id} • Time: {timestamp}UTC'
# - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
        # voice-log
        VOICE_CHANNEL_JOIN:
          embed:
            title: 'Voice Join'
            description: |-
              🎙 <@{member.id}>
              **Joined:** {channel.name}
            image: 
              url: 'https://cdn.discordapp.com/attachments/670339348956446772/808055881966813234/embed_width.png'
            footer: 
              text: 'UserID: {member.id} • Time: {timestamp}UTC'
            color: 0x2EFF27 #green
        
        VOICE_CHANNEL_MOVE:
          embed:
            title: 'Voice Move'
            description: |-
              🎙 <@{member.id}>
              **From:** {oldChannel.name}
              **To:** {newChannel.name}
            image: 
              url: 'https://cdn.discordapp.com/attachments/670339348956446772/808055881966813234/embed_width.png'
            footer: 
              text: 'UserID: {member.id} • Time: {timestamp}UTC'
            color: 0x2744FF #blue
        
        VOICE_CHANNEL_LEAVE:
          embed:
            title: 'Voice Leave'
            description: |-
              🎙 <@{member.id}>
              **Left:** {channel.name}
            image: 
              url: 'https://cdn.discordapp.com/attachments/670339348956446772/808055881966813234/embed_width.png'
            footer: 
              text: 'UserID: {member.id} • Time: {timestamp}UTC'
            color: 0xFF2727 #red
        
        VOICE_CHANNEL_FORCE_MOVE:
          embed:
            title: 'Voice Forced Move'
            description: |-
              🎙 <@{member.id}>
              **From:** {oldChannel.name}
              **To:** {newChannel.name}
              **By:** <@{mod.id}>
            image: 
              url: 'https://cdn.discordapp.com/attachments/670339348956446772/808055881966813234/embed_width.png'
            footer: 
              text: 'UserID: {member.id} • Time: {timestamp}UTC'
            color: 0xFFA027 #orange
# - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
        # other-log
        MEMBER_ROLE_ADD:
          embed:
            author:
              name: '{member.user.username}#{member.user.discriminator}'
            title: 'ROLE(S) ADDED'
            fields:
            -  name : '**User:**'
               value : '<@{member.id}>'
               inline : true
            -  name : '**Role(s) Added:**'
               value : '{roles}'
               inline : true
            image: 
              url: 'https://cdn.discordapp.com/attachments/670339348956446772/808055881966813234/embed_width.png'
            footer: 
              text: 'UserID: {member.id} • Time: {timestamp}UTC'
            color: 0x2EFF27 #green
        
        MEMBER_ROLE_REMOVE:
          embed:
            author:
              name: '{member.user.username}#{member.user.discriminator}'
            title: 'ROLE(S) REMOVED'
            fields:
            -  name : '**User:**'
               value : '<@{member.id}>'
               inline : true
            -  name : '**Role(s) Removed:**'
               value : '{roles}'
               inline : true
            image: 
              url: 'https://cdn.discordapp.com/attachments/670339348956446772/808055881966813234/embed_width.png'
            footer: 
              text: 'UserID: {member.id} • Time: {timestamp}UTC'
            color: 0xFF2727 #red
        
        MEMBER_ROLE_CHANGES:
          embed:
            author:
              name: '{member.user.username}#{member.user.discriminator}'
            title: 'ROLE(S) CHANGED'
            fields:
            -  name : '**User:**'
               value : '<@{member.id}>'
               inline : true
            -  name : '**Role(s) Added:**'
               value : '{addedRoles}'
               inline : true
            -  name : '**Role(s) Removed:**'
               value : '{removedRoles}'
               inline : true
            image: 
              url: 'https://cdn.discordapp.com/attachments/670339348956446772/808055881966813234/embed_width.png'
            footer: 
              text: 'UserID: {member.id} • Time: {timestamp}UTC'
            color: 0x2744FF #blue
        
        CASE_DELETE:
          embed:
            title: 'CASE DELETED'
            fields:
            -  name : '**Case:**'
               value : '#{caseNumber}'
               inline : true
            -  name : '**By:**'
               value : '<@{mod.id}>'
               inline : true
            image: 
              url: 'https://cdn.discordapp.com/attachments/670339348956446772/808055881966813234/embed_width.png'
            footer: 
              text: 'Time: {timestamp}UTC'
            color: 0xFF2727 #red
        
        CASE_UPDATE:
          embed:
            title: 'CASE UPDATED'
            fields:
            -  name : '**By:**'
               value : '<@{mod.id}>'
               inline : true
            -  name : '**Case:**'
               value : '#{caseNumber}({caseType})'
               inline : true
            -  name : '**Note:**'
               value : '```{note}```'
               inline : false
            image: 
              url: 'https://cdn.discordapp.com/attachments/670339348956446772/808055881966813234/embed_width.png'
            footer: 
              text: 'Time: {timestamp}UTC'
            color: 0xFFA027 #orange
        
        SET_ANTIRAID_USER:
          embed:
            title: 'ANTI-RAID SET'
            description: |-
              '⚔ <@{user.ID}> set anti-raid to **{level}**'
            image: 
              url: 'https://cdn.discordapp.com/attachments/670339348956446772/808055881966813234/embed_width.png'
            footer: 
              text: 'Time: {timestamp}UTC'
            color: 0x2EFF27 #green
        
        SET_ANTIRAID_AUTO:
          embed:
            title: 'AUTO ANTI-RAID'
            description: |-
              '⚔ Anti-raid automatically set to **{level}**'
            image: 
              url: 'https://cdn.discordapp.com/attachments/670339348956446772/808055881966813234/embed_width.png'
            footer: 
              text: 'Time: {timestamp}UTC'
            color: 0x2EFF27 #green
        
        BOT_ALERT:
          embed:
            title: 'BOT ALERT'
            description: |-
              <@90031537206099968>
              {tmplEval(body)}
            image: 
              url: 'https://cdn.discordapp.com/attachments/670339348956446772/808055881966813234/embed_width.png'
            footer: 
              text: 'Time: {timestamp}UTC'
            color: 0xFFFFFF #black
```
</details>

---


#### LATEST PRETTY EMBED LOGS, COMPACT EDITON (highly recommended)

<details>
  <summary>Click to view code!</summary>

```yaml
        '846039475897106432': #simpler zep
          exclude: [] # Exclude nothing = include everything
          exclude_bots: false
      format:
        timestamp: ""

        CASE_CREATE: >-
          ✏ {userMention(mod)} manually created new **{caseType}** case
          (#{caseNum})

        CASE_DELETE: |-
          <:statusdnd:714833495524114464> **CASE DELETED**
          <:profile:841364699958607894><:dash:855062799659171850><@!{mod.id}><:dot:855062799607529472>`{mod.id}`
          <:channeltext:779036156175188001><:dash:855062799659171850>**Case#{case.case_number}**
          
          <:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460><:line:855055669824061460>

        CASE_UPDATE: |-
          ✏ {userMention(mod)} updated case #{caseNumber} ({caseType}) with note:
          ```{note}```

        BOT_ALERT:
          embed: 
            description: |-
              :warning: **BOT ALERT** 
              {tmplEval(body)}

        DM_FAILED:
          embed: 
            description: |-
              :construction: **DM FAILED** Failed to send DM to <@{user.id}>
              Source: {source}
            footer: 
              text: '{user.id}'
              icon_url: https://cdn.discordapp.com/{if(user.avatar, concat("avatars/", user.id, "/", user.avatar, ".",if(eq(slice(concat(user.avatar),0,2),"a_"),"gif","png")),concat("embed/avatars/", rand(1, 4,user.id), ".png"))}

        # MODERATION
        MEMBER_NOTE:
          embed: 
            description: |-
              :notepad_spiral: `[{caseNumber}]` **note** on <@{user.id}> by <@{mod.id}>
            color: 0xffb347 #pastel orange
            footer: 
              text: '{user.id}'
              icon_url: https://cdn.discordapp.com/{if(member.user.avatar, concat("avatars/", member.user.id, "/", member.user.avatar, ".",if(eq(slice(concat(member.user.avatar),0,2),"a_"),"gif","png")),concat("embed/avatars/", rand(1, 4,member.user.id), ".png"))}

        MEMBER_WARN:
          embed: 
            description: |-
              :warning: `[{caseNumber}]` **<@{member.id}> warned** by <@{mod.id}>```{reason}```
            color: 0xfdfd96 #pastel yellow
            footer: 
              text: '{member.id}'
              icon_url: https://cdn.discordapp.com/{if(member.user.avatar, concat("avatars/", member.user.id, "/", member.user.avatar, ".",if(eq(slice(concat(member.user.avatar),0,2),"a_"),"gif","png")),concat("embed/avatars/", rand(1, 4,member.user.id), ".png"))}

        MEMBER_MUTE:
          embed: 
            description: |-
              <:iconmuted:837072273978294283> `[{caseNumber}]` **<@{user.id}> muted forever** by <@{mod.id}>```{reason}```
            color: 0xff6666 #pastel red
            footer: 
              text: '{user.id}'
              icon_url: https://cdn.discordapp.com/{if(user.avatar, concat("avatars/", user.id, "/", user.avatar, ".",if(eq(slice(concat(user.avatar),0,2),"a_"),"gif","png")),concat("embed/avatars/", rand(1, 4,user.id), ".png"))}

        MEMBER_TIMED_MUTE:
          embed: 
            description: |-
              <:iconmuted:837072273978294283> `[{caseNumber}]` **<@{user.id}> muted** for {time} by <@{mod.id}>```{reason}```
            color: 0xff6666 #pastel red
            footer: 
              text: '{user.id}'
              icon_url: https://cdn.discordapp.com/{if(user.avatar, concat("avatars/", user.id, "/", user.avatar, ".",if(eq(slice(concat(user.avatar),0,2),"a_"),"gif","png")),concat("embed/avatars/", rand(1, 4,user.id), ".png"))}
        
        MASSMUTE: "\U0001F4E2\U0001F6AB {userMention(mod)} massmuted {count} users"

        MEMBER_UNMUTE:
          embed: 
            description: |-
              <:iconunmuted:837072274766823456> `[{caseNumber}]` **<@{user.id}> was unmuted** by <@{mod.id}>```{reason}```
            color: 0x77dd77 #pastel green
            footer: 
              text: '{user.id}'
              icon_url: https://cdn.discordapp.com/{if(user.avatar, concat("avatars/", user.id, "/", user.avatar, ".",if(eq(slice(concat(user.avatar),0,2),"a_"),"gif","png")),concat("embed/avatars/", rand(1, 4,user.id), ".png"))}

        MEMBER_TIMED_UNMUTE:
          embed: 
            description: |-
              <:iconunmuted:837072274766823456> **<@{user.id}> TIMED UNMUTED** by <@{mod.id}>. Time for mute was {time}
            color: 0x77dd77 #pastel green
            footer: 
              text: '{user.id}'
              icon_url: https://cdn.discordapp.com/{if(user.avatar, concat("avatars/", user.id, "/", user.avatar, ".",if(eq(slice(concat(user.avatar),0,2),"a_"),"gif","png")),concat("embed/avatars/", rand(1, 4,user.id), ".png"))}

        MEMBER_MUTE_EXPIRED:
          embed: 
            description: |-
              <:iconunmuted:837072274766823456> <@{member.id}> mute expired
            color: 0xfdfd96 #pastel yellow
            footer: 
              text: '{member.id}'
              icon_url: https://cdn.discordapp.com/{if(member.user.avatar, concat("avatars/", member.user.id, "/", member.user.avatar, ".",if(eq(slice(concat(member.user.avatar),0,2),"a_"),"gif","png")),concat("embed/avatars/", rand(1, 4,member.user.id), ".png"))}

        MEMBER_KICK:
          embed: 
            description: |-
              :boot: `[{caseNumber}]` **<@{user.id}> KICKED** by <@{mod.id}>```{reason}```
            color: 0xffb347 #pastel orange
            footer: 
              text: '{user.id}'
              icon_url: https://cdn.discordapp.com/{if(user.avatar, concat("avatars/", user.id, "/", user.avatar, ".",if(eq(slice(concat(user.avatar),0,2),"a_"),"gif","png")),concat("embed/avatars/", rand(1, 4,user.id), ".png"))}

        MEMBER_BAN:
          embed: 
            description: |-
              <:ban:863367110339330099> `[{caseNumber}]` **<@{user.id}> was banned** by <@{mod.id}>```{reason}```
            color: 0xff6666 #pastel red
            footer: 
              text: '{user.id}'
              icon_url: https://cdn.discordapp.com/{if(user.avatar, concat("avatars/", user.id, "/", user.avatar, ".",if(eq(slice(concat(user.avatar),0,2),"a_"),"gif","png")),concat("embed/avatars/", rand(1, 4,user.id), ".png"))}

        MEMBER_TIMED_BAN:
          embed: 
            description: |-
              <:ban:863367110339330099> `[{caseNumber}]` **<@{user.id}> TEMP BANNED** for {banTime} by <@{mod.id}> for {reason}
            color: 0xff6666 #pastel red
            footer: 
              text: '{user.id}'
              icon_url: https://cdn.discordapp.com/{if(user.avatar, concat("avatars/", user.id, "/", user.avatar, ".",if(eq(slice(concat(user.avatar),0,2),"a_"),"gif","png")),concat("embed/avatars/", rand(1, 4,user.id), ".png"))}

        MEMBER_FORCEBAN:
          embed: 
            description: |-
              <:ban:863367110339330099> `[{caseNumber}]` **{userId} was force banned** by <@{mod.id}>```{reason}```
            color: 0xff6666 #pastel red
            footer: 
              text: '{user.id}'
              icon_url: https://cdn.discordapp.com/{if(user.avatar, concat("avatars/", user.id, "/", user.avatar, ".",if(eq(slice(concat(user.avatar),0,2),"a_"),"gif","png")),concat("embed/avatars/", rand(1, 4,user.id), ".png"))}
        
        MASSBAN:
          embed: 
            description: |-
              <:ban:863367110339330099> **<@{mod.id}> massbanned {count} users**
            color: 0xff6666 #pastel red
            footer: 
              text: '{mod.id}'
              icon_url: https://cdn.discordapp.com/{if(mod.avatar, concat("avatars/", mod.id, "/", mod.avatar, ".",if(eq(slice(concat(mod.avatar),0,2),"a_"),"gif","png")),concat("embed/avatars/", rand(1, 4,mod.id), ".png"))}
        
        MEMBER_SOFTBAN:
          embed: 
            description: |-
              <:ban:863367110339330099> `[{caseNumber}]` **<@{member.id}>** (created {account_age} ago) **softbanned** by <@{mod.id}>
            color: 0xff6666 #pastel red
            footer: 
              text: '{member.id}'
              icon_url: https://cdn.discordapp.com/{if(member.user.avatar, concat("avatars/", member.user.id, "/", member.user.avatar, ".",if(eq(slice(concat(member.user.avatar),0,2),"a_"),"gif","png")),concat("embed/avatars/", rand(1, 4,member.user.id), ".png"))}
 
        MEMBER_UNBAN:
          embed: 
            description: |-
              <:statusonline:714853868420202529> `[{caseNumber}]` **{userId} was unbanned** by <@{mod.id}>```{reason}```              
            color: 0x77dd77 #pastel green
            footer: 
              text: '{user.id}'
              icon_url: https://cdn.discordapp.com/{if(user.avatar, concat("avatars/", user.id, "/", user.avatar, ".",if(eq(slice(concat(user.avatar),0,2),"a_"),"gif","png")),concat("embed/avatars/", rand(1, 4,user.id), ".png"))}

        MEMBER_TIMED_UNBAN:
          embed: 
            description: |-
              <:ban:863367110339330099> `[{caseNumber}]` **<@{user.id}> UNBANNED** by <@{mod.id}>. The orignal ban time was {bantime}
            color: 0x77dd77 #pastel green
            footer: 
              text: '{user.id}'
              icon_url: https://cdn.discordapp.com/{if(user.avatar, concat("avatars/", user.id, "/", user.avatar, ".",if(eq(slice(concat(user.avatar),0,2),"a_"),"gif","png")),concat("embed/avatars/", rand(1, 4,user.id), ".png"))}

        MASSUNBAN:
          embed: 
            description: |-
              <:ban:863367110339330099> **<@{mod.id}> mass unbanned {count} users**
            color: 0x77dd77 #pastel green
            footer: 
              text: '{mod.id}'
              icon_url: https://cdn.discordapp.com/{if(mod.avatar, concat("avatars/", mod.id, "/", mod.avatar, ".",if(eq(slice(concat(mod.avatar),0,2),"a_"),"gif","png")),concat("embed/avatars/", rand(1, 4,mod.id), ".png"))}
        
        MEMBER_JOIN: 
          embed: 
            description: |-
              <:join:754438854487965807> **MEMBER JOIN**
              <@{member.id}> | {member.user.username} created {account_age} ago
            color: 0x77dd77 #pastel green
            footer: 
              text: '{member.id}'
              icon_url: https://cdn.discordapp.com/{if(member.user.avatar, concat("avatars/", member.user.id, "/", member.user.avatar, ".",if(eq(slice(concat(member.user.avatar),0,2),"a_"),"gif","png")),concat("embed/avatars/", rand(1, 4,member.user.id), ".png"))}
        
        MEMBER_JOIN_WITH_PRIOR_RECORDS:
          embed: 
            description: |-
              :warning: **<@{member.id}>** joined with prior records
              Summary:{recentCaseSummary}
            color: 0xfdfd96 #pastel yellow
            footer: 
              text: '{member.id}'
              icon_url: https://cdn.discordapp.com/{if(member.user.avatar, concat("avatars/", member.user.id, "/", member.user.avatar, ".",if(eq(slice(concat(member.user.avatar),0,2),"a_"),"gif","png")),concat("embed/avatars/", rand(1, 4,member.user.id), ".png"))}
        
        MEMBER_MUTE_REJOIN:
          embed: 
            description: |-
              <:icondeafened:837072274086953000> **<{member.id}> mute rejoin**
            color: 0xfdfd96 #pastel yellow
            footer: 
              text: '{member.id}'
              icon_url: https://cdn.discordapp.com/{if(member.user.avatar, concat("avatars/", member.user.id, "/", member.user.avatar, ".",if(eq(slice(concat(member.user.avatar),0,2),"a_"),"gif","png")),concat("embed/avatars/", rand(1, 4,member.user.id), ".png"))}
        
        MEMBER_RESTORE:
          embed: 
            description: |-
              <:downloadupdate:758794223176384512> **MEMBER RESTORE** for <@{member.id}>
              Data Restored: {restoredData}
            color: 0x77dd77 #pastel green
            footer: 
              text: '{member.id}'
              icon_url: https://cdn.discordapp.com/{if(member.user.avatar, concat("avatars/", member.user.id, "/", member.user.avatar, ".",if(eq(slice(concat(member.user.avatar),0,2),"a_"),"gif","png")),concat("embed/avatars/", rand(1, 4,member.user.id), ".png"))}

        MEMBER_LEAVE:
          embed: 
            description: |-
              <:leave:754438854961922069> **<@{member.id}> ({member.user.username}) left the server**
              <:join:754438854487965807> <t:{rand(div(member.joinedAt, 1000), div(member.joinedAt, 1000))}> (<t:{rand(div(member.joinedAt, 1000), div(member.joinedAt, 1000))}:R>)
            color: 0xff6666 #pastel red
            footer: 
              text: '{member.id}'
              icon_url: https://cdn.discordapp.com/{if(member.user.avatar, concat("avatars/", member.user.id, "/", member.user.avatar, ".",if(eq(slice(concat(member.user.avatar),0,2),"a_"),"gif","png")),concat("embed/avatars/", rand(1, 4,member.user.id), ".png"))}

        MEMBER_ROLE_ADD:
          embed: 
            description: |-
              <:statusonline:714853868420202529> **{roles}** added to <@{member.id}> by <@{mod.id}>
            color: 0x77dd77 #pastel green
            footer: 
              text: '{member.id}'
              icon_url: https://cdn.discordapp.com/{if(member.user.avatar, concat("avatars/", member.user.id, "/", member.user.avatar, ".",if(eq(slice(concat(member.user.avatar),0,2),"a_"),"gif","png")),concat("embed/avatars/", rand(1, 4,member.user.id), ".png"))}

        MEMBER_ROLE_REMOVE:
          embed: 
            description: |-
              <:statusdnd:714833495524114464> **{roles}** removed from <@{member.id}> by <@{mod.id}>
            color: 0xff6666 #pastel red
            footer: 
              text: '{member.id}'
              icon_url: https://cdn.discordapp.com/{if(member.user.avatar, concat("avatars/", member.user.id, "/", member.user.avatar, ".",if(eq(slice(concat(member.user.avatar),0,2),"a_"),"gif","png")),concat("embed/avatars/", rand(1, 4,member.user.id), ".png"))}

        MEMBER_ROLE_CHANGES:
          embed: 
            description: |-
              :pencil: **ROLE CHANGES**
              <:leave:754438854961922069> **{removedRoles}** <:join:754438854487965807> **{addedRoles}** for <@{member.id}> by <@{mod.id}>
            footer: 
              text: '{member.id}'
              icon_url: https://cdn.discordapp.com/{if(member.user.avatar, concat("avatars/", member.user.id, "/", member.user.avatar, ".",if(eq(slice(concat(member.user.avatar),0,2),"a_"),"gif","png")),concat("embed/avatars/", rand(1, 4,member.user.id), ".png"))}

        MEMBER_NICK_CHANGE:
          embed: 
            description: |-
              :pencil: **NICKNAME CHANGE** for <@{member.id}>
              `{oldNick}` to **{newNick}**
            color: 0xffb347 #pastel orange
            footer: 
              text: '{member.id}'
              icon_url: https://cdn.discordapp.com/{if(member.user.avatar, concat("avatars/", member.user.id, "/", member.user.avatar, ".",if(eq(slice(concat(member.user.avatar),0,2),"a_"),"gif","png")),concat("embed/avatars/", rand(1, 4,member.user.id), ".png"))}

        MEMBER_USERNAME_CHANGE:
          embed: 
            description: |-
              :pencil: **USER CHANGE** by <@{user.id}>
              `{oldName}` to `{newName}`
            color: 0xffb347 #pastel orange
            footer: 
              text: '{user.id}'
              icon_url: https://cdn.discordapp.com/{if(user.avatar, concat("avatars/", user.id, "/", user.avatar, ".",if(eq(slice(concat(user.avatar),0,2),"a_"),"gif","png")),concat("embed/avatars/", rand(1, 4,user.id), ".png"))}


        CHANNEL_CREATE:
          embed: 
            description: |-
              <:statusonline:714853868420202529> **CHANNEL CREATE** <#{channel.id}>
            color: 0x77dd77 #pastel green
              
        CHANNEL_DELETE:
          embed: 
            description: |-
              :x: **CHANNEL DELETE** {channel.name}
            color: 0xff6666 #pastel red

        #channel     
        CHANNEL_EDIT:
          embed: 
            description: |-
              :pencil: **CHANNEL EDIT** <#{channel.id}>
            color: 0xffb347 #pastel orange
            
        #roles
        ROLE_CREATE:
          embed: 
            description: |-
              <:statusonline:714853868420202529> **ROLE CREATE** 
              <@&{role.id}> **{role.name}**
            color: 0x77dd77 #pastel green
            
        ROLE_DELETE:  
          embed: 
            description: |-
              :x: **ROLE DELETE**
              **{role.name}** `{role.id}`
            color: 0xff6666 #pastel red
        ROLE_EDIT:
          embed: 
            description: |-
              :pencil: **ROLE EDITED** 
              <@&{role.id}> **{role.name}**

        #Messages
        MESSAGE_EDIT: 
          embed: 
            # UPDATE THE SERVER ID IN THE LINK BELOW!
            description: |-
              :pencil: **[MESSAGE EDITED](https://discord.com/channels/572102445921075210/{channel.id}/{after.id})** by <@{user.id}> in <#{channel.id}>
              **Before:**{messageSummary(before)}**After:**{messageSummary(after)}
            color: 0xffb347 #pastel orange
            footer: 
              text: '{user.id}'
              icon_url: https://cdn.discordapp.com/{if(user.avatar, concat("avatars/", user.id, "/", user.avatar, ".",if(eq(slice(concat(user.avatar),0,2),"a_"),"gif","png")),concat("embed/avatars/", rand(1, 4,user.id), ".png"))}

        MESSAGE_DELETE:
          embed: 
            description: |-
              :x: **MESSAGE DELETE** by <@{user.id}> in <#{channel.id}>
              {messageSummary(message)}
            color: 0xff6666 #pastel red
            footer: 
              text: '{user.id}'
              icon_url: https://cdn.discordapp.com/{if(user.avatar, concat("avatars/", user.id, "/", user.avatar, ".",if(eq(slice(concat(user.avatar),0,2),"a_"),"gif","png")),concat("embed/avatars/", rand(1, 4,user.id), ".png"))}
        MESSAGE_DELETE_BULK:
          embed: 
            description: |-
              :x: **[{count} MESSAGE DELETE]({archiveUrl})** by {authorIds} in <#{channel.id}>
              {messageSummary(message)}
            color: 0xff6666 #pastel red
            footer: 
              text: '{user.id}'
              icon_url: https://cdn.discordapp.com/{if(user.avatar, concat("avatars/", user.id, "/", user.avatar, ".",if(eq(slice(concat(user.avatar),0,2),"a_"),"gif","png")),concat("embed/avatars/", rand(1, 4,user.id), ".png"))}

        MESSAGE_DELETE_BARE:
          embed: 
            description: |-
              <:iconsystemx:842172192418693173> **MESSAGE DELETE BARE** `{message.id}`
              in <#{channel.id}> {messageSummary(message)}
            color: 0xff6666 #pastel red

        MESSAGE_DELETE_AUTO:
          embed: 
            description: |-
              <:trashcan:750152850310561853> **AUTO DELETE** `{message.id}`
              by <@{user.id}> in <#{channel.id}> {messageSummary(message)}
            color: 0xff6666 #pastel red
            footer: 
              text: '{user.id}'
              icon_url: https://cdn.discordapp.com/{if(user.avatar, concat("avatars/", user.id, "/", user.avatar, ".",if(eq(slice(concat(user.avatar),0,2),"a_"),"gif","png")),concat("embed/avatars/", rand(1, 4,user.id), ".png"))}
        CLEAN:
          embed: 
            description: |-
              :soap: **[{count} MESSAGE CLEAN]({archiveUrl})** by <@{mod.id}> in <#{channel.id}>
            color: 0xff6666 #pastel red
            footer: 
              text: '{mod.id}'
              icon_url: https://cdn.discordapp.com/{if(mod.avatar, concat("avatars/", mod.id, "/", mod.avatar, ".",if(eq(slice(concat(mod.avatar),0,2),"a_"),"gif","png")),concat("embed/avatars/", rand(1, 4,mod.id), ".png"))}
        
        VOICE_CHANNEL_JOIN:
          embed: 
            description: |-
              <:join:754438854487965807> **VC JOIN** by <@{member.id}> in <#{channel.id}>
            color: 0x77dd77 #pastel green
            footer: 
              text: '{member.id}'
              icon_url: https://cdn.discordapp.com/{if(member.user.avatar, concat("avatars/", member.user.id, "/", member.user.avatar, ".",if(eq(slice(concat(member.user.avatar),0,2),"a_"),"gif","png")),concat("embed/avatars/", rand(1, 4,member.user.id), ".png"))}

        VOICE_CHANNEL_MOVE:
          embed: 
            description: |-
              <:iconundeafened:837072274527485983> **VC MOVE** <#{oldChannel.id}> to <#{newChannel.id}> by <@{member.id}>
            color: 0xffb347 #pastel orange
            footer: 
              text: '{member.id}'
              icon_url: https://cdn.discordapp.com/{if(member.user.avatar, concat("avatars/", member.user.id, "/", member.user.avatar, ".",if(eq(slice(concat(member.user.avatar),0,2),"a_"),"gif","png")),concat("embed/avatars/", rand(1, 4,member.user.id), ".png"))}
        VOICE_CHANNEL_FORCE_MOVE:
          embed: 
            description: |-
              <:iconundeafened:837072274527485983> **VC FORCE MOVE** <@{member.id}> moved by <@{mod.id}>
              <#{oldChannel.id}> to <#{newChannel.id}>

        VOICE_CHANNEL_LEAVE:
          embed: 
            description: |-
              <:leave:754438854961922069> **VC LEAVE** by <@{member.id}> in <#{channel.id}>
            color: 0xff6666 #pastel red
            footer: 
              text: '{member.id}'
              icon_url: https://cdn.discordapp.com/{if(member.user.avatar, concat("avatars/", member.user.id, "/", member.user.avatar, ".",if(eq(slice(concat(member.user.avatar),0,2),"a_"),"gif","png")),concat("embed/avatars/", rand(1, 4,member.user.id), ".png"))}
        VOICE_CHANNEL_FORCE_DISCONNECT:
          embed: 
            description: |-
              <:icondeafened:837072274086953000> **VC FORCE DISCONNECT**
              for <@{member.id}> from <#{oldChannel.id}> by <@{mod.id}>
            color: 0xff6666 #pastel red
            footer: 
              text: '{member.id}'
              icon_url: https://cdn.discordapp.com/{if(member.user.avatar, concat("avatars/", member.user.id, "/", member.user.avatar, ".",if(eq(slice(concat(member.user.avatar),0,2),"a_"),"gif","png")),concat("embed/avatars/", rand(1, 4,member.user.id), ".png"))}


        #COMMAND: "\U0001F916 {userMention(member)} used command in {channelMention(channel)}:\n`{command}`"
        #unused in zep atm

        #legacy not included
        #MESSAGE_SPAM_DETECTED: "\U0001F6D1 {userMention(member)} spam detected in {channelMention(channel)}: {description} (more than {limit} in {interval}s)\n{archiveUrl}"
        #legacy not included
        #OTHER_SPAM_DETECTED: "\U0001F6D1 {userMention(member)} spam detected: {description} (more than {limit} in {interval}s)"

        SCHEDULED_MESSAGE:
          embed: 
            description: |-
              ⏰ {userMention(author)} scheduled a message to be posted to
              {channelMention(channel)} on {datetime}
            color: 0xffb347 #pastel orange
            
        SCHEDULED_REPEATED_MESSAGE:
          embed: 
            description: |-
              ⏰ {userMention(author)} scheduled a message to be posted to
              {channelMention(channel)} on {datetime}, repeated {repeatDetails}
            color: 0xffb347 #pastel orange

        REPEATED_MESSAGE:
          embed: 
            description: |-
              ⏰ {userMention(author)} scheduled a message to be posted to
              {channelMention(channel)} {repeatDetails}
            color: 0xffb347 #pastel orange

        POSTED_SCHEDULED_MESSAGE:
          embed: 
            description: |-
              Posted scheduled message (`{messageId}`) to {channelMention(channel)} as scheduled by {userMention(author)}
            color: 0xffb347 #pastel orange

        AUTOMOD_ACTION:
          embed: 
            description: |-
              <:iconsearch:778925668536811520> **AUTOMOD ACTION**
              <@{user.id}> triggered {rule}, Actions taken: **{actionsTaken}** {matchSummary}
            color: 0xffb347 #pastel orange
            footer: 
              text: '{user.id}'
              icon_url: https://cdn.discordapp.com/{if(user.avatar, concat("avatars/", user.id, "/", user.avatar, ".",if(eq(slice(concat(user.avatar),0,2),"a_"),"gif","png")),concat("embed/avatars/", rand(1, 4,user.id), ".png"))}

        SET_ANTIRAID_USER:
          embed: 
            description: |-
              <:iconrole:826477127209320534> **ANTI-RAID**
              Antiraid level: **{level}**
            color: 0xffb347 #pastel orange
            footer: 
              text: '{user.id}'
              icon_url: https://cdn.discordapp.com/{if(user.avatar, concat("avatars/", user.id, "/", user.avatar, ".",if(eq(slice(concat(user.avatar),0,2),"a_"),"gif","png")),concat("embed/avatars/", rand(1, 4,user.id), ".png"))}

        SET_ANTIRAID_AUTO:
          embed: 
            description: |-
              <:iconrole:826477127209320534> **AUTO ANTI-RAID**
              Antiraid level: **{level}**
            color: 0xffb347 #pastel orange
```
</details>

---
