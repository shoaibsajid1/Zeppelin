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
