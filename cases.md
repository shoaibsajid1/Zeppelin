# CASES

This plugin contains basic configuration for cases created by other plugins

`log_automatic_actions: true` Enabling this logs all manually created actions as well , such as when u right click and ban manually instead of using bot commands.

`case_log_channel: "1234"` This setting allows you to set the channel for logging all your cases, in this instance, `1234` is the channel ID

⏲️  **RELATIVE TIME**

`show_relative_times: true` This enables the relative time setting

`relative_time_cutoff: 7d` is the amount of time after which `!cases` will show the full date, not a relative time (e.g. "5 hours ago")

so if you set relative time cutoff to 24h, any cases older than 24h would show the full date, e.g. "2021-01-30", rather than e.g. "1 day ago"

---

`case_colors` [Optional] This setting allows you to customize the embed strip color for various actions such as warn,mute etc. You can either type color names like `yellow` `green` or use hex values such as `2EFF27` which is green.
If you would like to use the default setting, u may delete this part of the code

`case_icons` [Optional] This setting allows you to customize the case icons, you can either use custom emoji like `<:do_not_disturb:841799310797832244>` but note that zeppelin needs to be in the same server as the emote or it wont work or you can use default unicode emojis such as `:boot:`.  If you would like to use the default setting, u may delete this part of the code


#### PLUGIN CODE

```yaml
  cases:
    replaceDefaultOverrides: true #replaces default settings if true
    config:
      log_automatic_actions: true
      case_log_channel: "851837989545050162" #cases channel
      #case_log_channel: *cases
      show_relative_times: true
      relative_time_cutoff: 7d
      case_colors:
        warn: yellow
        ban: red
        unban: 2EFF27 #green
        note: FEE9E9 #whitish
        kick: F34B80 #pinkish
        mute: yellow
        unmute: 2EFF27 #green
        deleted: orange
        softban: F73C4F #Lighter shade of red
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
```
