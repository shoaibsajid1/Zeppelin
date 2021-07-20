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

### What plugins are there ?

Whoa!, you here already? What a pro. There are many plugins which I cover in detail. But lets start with the most important ones first.

### Cases
This plugin  shows all the cases in a set channel
>![image](assets/cases.png)
> 
> *An example of cases channel*


<details>
  <summary>To see more about cases plugin, click to expand</summary>

`log_automatic_actions: true` 

Enabling this logs all manually created actions as well , such as when u right click and ban manually instead of using bot commands.

`case_log_channel: "1234"` 

This setting allows you to set the channel for logging all your cases, in this instance, `1234` is the channel ID

⏲️  **RELATIVE TIME**

`show_relative_times: true` This enables the relative time setting

`relative_time_cutoff: 7d` is the amount of time after which `!cases` will show the full date, not a relative time (e.g. "5 hours ago")

so if you set relative time cutoff to 24h, any cases older than 24h would show the full date, e.g. "2021-01-30", rather than e.g. "1 day ago"

---

`case_colors` [Optional] This setting allows you to customize the embed strip color for various actions such as warn,mute etc. You can either type color names like `yellow` `green` or use hex values such as `2EFF27` which is green.
If you would like to use the default setting, u may delete this part of the code

`case_icons` [Optional] This setting allows you to customize the case icons, you can either use custom emoji like `<:do_not_disturb:841799310797832244>` but note that zeppelin needs to be in the same server as the emote or it wont work or you can use default unicode emojis such as `:boot:`.  If you would like to use the default setting, u may delete this part of the code


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

</details>
---

### Mod Actions

 Use this to set messages for what happens when you warn, ban etc. Who can warn, ban, how many messages to delete on ban. You set all of that in this plugin

### Mutes

 Same as above but for mutes

### Auto Reactions

Often used for suggestion channel, adds reactions to every message on set channel

> ![image](assets/suggestions.png)
> 
> *An example of auto reactions being used for a suggestions channel, in this case 👍 👎*

---

### Persist

>  This plugin allows you to restore the roles back to the user when they join the server back. Please note that you need to add every role one by one on the config and if you delete role that was on config, the plugin will break so i recommend you use YAGPDB or carlbot for this instead. 

```yaml
  persist:
    replaceDefaultOverrides: true #replaces default settings if true
    config:
      persisted_roles:

        - "827840992111099935" #Bronze
        - "827841264489725983" #Silver
        - "827841321716678698" #Gold
        - "827841368374247454" #Platinum
        
        - "828659945158737931" #Regulars

        - "808718941785554985" #⭐️ star

        - "832922355009060894" #dexians
      persist_nicknames: true
      persist_voice_mutes: true
```
To view default setting: https://zeppelin.gg/docs/plugins/persist#:~:text=Config%20schema-,Click,-to%20expand

---

### Welcome Message

Send a welcome message in dm or in a channel

> ![image](assets/welcome.png)
>
>*Example of message sent to dm*
 

For more info on this plugin [Click Here](welcome_message.md)

---

The following plugins are very old and outdated now so I will not cover them but those are:

- [Autodelete](autodelete.md) (deletes everything in channel after x seconds)

- `spam_protection` (Use `automod` instead)

- `censor` (Use `automod` instead)

[Automod & Counters](automod+counters.md)
[Click here](autoreactions.md)
[Automod Rules](rules.md)

[Companion Channels](companion_channels.md)
[Locate User](locate.md) 
[Click here](logs.md)
[Miscellaneous](miscellaneous.md) 
[Mutes & Mod actions](mutes&modactions.md) 
[Persist](persist.md) 
[Pingable roles](pingable_roles.md)
[Post](post.md) 
[Reaction Roles](reaction_roles.md)
[Reminders](reminder.md)
[Roles](roles.md)
[Self grantable roles](self_grantable_roles.md)
[Slowmode](slowmode.md)
[Starboard](starboard.md)
[Tags](tags.md)
[Time and Date](time_and_date.md)
[Utility](utility.md)


--- 


See https://zeppelin.gg/ for more details.

## Contributing
Pull requests are welcome. For major changes, please open an issue first to discuss what you would like to change.
## More Info

You can also find me on the zeppelin support server

[![Join our Discord server!](https://invidget.switchblade.xyz/9bCGvGw5rT)](http://discord.gg/9bCGvGw5rT)

You can join my server and follow github channel for updates or to play with Zeppelin there (since you cant use zeppelin on Zep support server)

[![Join our Discord server!](https://invidget.switchblade.xyz/JCZf3sHYpE)](http://discord.gg/JCZf3sHYpE)

