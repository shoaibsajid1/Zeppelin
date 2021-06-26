  mutes:
    replaceDefaultOverrides: true #replaces default settings if true
    config:
      mute_role: "852040311521411092" #muterole here
      move_to_voice_channel: "852040275404128257" #vc id
      kick_from_voice_channel: false #muted users are also immediately kicked from their current voice channel
      dm_on_mute: true
      dm_on_update: true #updating mute time informs user
      message_on_mute: true
      message_on_update: true
      message_channel: "852040519470940200" #muted message channel
      #mute_message for indefinite mutes
      mute_message: 'You have been muted on the {guildName} server. Reason given: {reason}'
      #timed_mute_message for mutes with an expiration time
      timed_mute_message: >-
        You have been muted on the {guildName} server for {time}. Reason given:
        {reason}
      update_mute_message: 'Your mute on the {guildName} server has been updated to {time}.'
      remove_roles_on_mute: true #removes all roles upon mute or  : ["role 1", "role 2"] and those specific roles are removed upon mute
      restore_roles_on_mute: true #restores the roles when mute is over
      can_view_list: false #can view muted list via !mutes command
    overrides:
      - level: '>=50'
        config:
          can_view_list: true
      - level: '>=100'
        config:
        #Clear dangling mutes for members who have been banned
          can_cleanup: true

  mod_actions:
    config:
      dm_on_warn: true
      dm_on_kick: false
      dm_on_ban: false
      message_on_warn: false
      message_on_kick: false
      message_on_ban: false
      message_channel: null
      warn_message: 'You have received a warning on the {guildName} server: {reason}'
      kick_message: 'You have been kicked from the {guildName} server. Reason given: {reason}'
      ban_message: 'You have been banned from the {guildName} server. Reason given: {reason}'
      tempban_message: >-
        You have been banned from the {guildName} server for {banTime}. Reason
        given: {reason}
      alert_on_rejoin: false
      alert_channel: null
      #if you have warn_notify_enabled: true, then warn_notify_threshold is the number of warnings the user must get before the !warn  command asks you "hey, this user has already been warned 5 times, warn them again?"
      warn_notify_enabled: true
      warn_notify_threshold: 5
      warn_notify_message: |-
        The user already has **{priorWarnings}** warnings!
         Please check their prior cases and assess whether or not to warn anyways.
         Proceed with the warning?
      ban_delete_message_days: 0
      can_note: false
      can_warn: false
      can_mute: false
      can_kick: false
      can_ban: false
      can_unban: false
      can_view: false
      can_addcase: false
      can_massunban: false
      can_massban: false
      can_massmute: false
      can_hidecase: false
      can_deletecase: false
      #can_act_as_other allows you to use the -mod option for commands such as !ban - this will set the case's moderator as the user you specify, and also mention your name below theirs if you view the case
      can_act_as_other: false
      #Manual actions wouls be stuff like right click ban, right click kick , it will create cases for those as well
      create_cases_for_manual_actions: true
    overrides:
      - level: '>=50'
        config:
          can_note: true
          can_warn: true
          can_mute: true
          can_kick: true
          can_ban: true
          can_unban: true
          can_view: true
          can_addcase: true
      - level: '>=100'
        config:
          can_massunban: true
          can_massban: true
          can_massmute: true
          can_hidecase: true
          can_act_as_other: true
