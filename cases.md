  cases:
    replaceDefaultOverrides: false #replaces default settings if true
    config:
      log_automatic_actions: true
      case_log_channel: "851837989545050162" #cases channel
      show_relative_times: true
      #relative_time_cutoff is the amount of time after which !cases will show the full date, not a relative time (e.g. "5 hours ago")
      #if you set relative time cutoff to 24h, any cases older than 24h would show the full date, e.g. "2021-01-30", rather than e.g. "1 day ago"
      relative_time_cutoff: 7d
      #case_colors: #to enable these options, delete the # infront of the items below
        #warn: yellow
        #ban: red
        #unban: 2EFF27 #green
        #note: FEE9E9 #whitish
        #kick: F34B80 #pinkish
        #mute: yellow
        #unmute: 2EFF27 #green
        #deleted: orange
        #softban: F73C4F #Lighter shade of red
      case_icons:
        warn: ":warning:"
        ban: ":hammer:"
        unban: ":green_circle:"
        note: ":pencil:"
        kick: ":boot:"
        mute: ":mute:"
        unmute: ":green_circle:"
        deleted: ":no_entry:"
        softban: ":boot:"
        #for custom emoji "<:do_not_disturb:841799310797832244>"
