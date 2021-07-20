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

**Step 2:** Insert role ID for level 50 and 100

**Step 3:** Type plugins

> This is where you will start enabling modules later on

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

---

### Auto Reactions

Often used for suggestion channel, adds reactions to every message on set channel

> ![image](assets/autoreactions.png)
> 
> *An example of auto reactions being used for a suggestions channel*

---

**Moderation based plugins**

- `mod_actions` Use this to set messages for what happens when you warn, ban etc. Who can warn, ban, how many messages to delete on ban. You set all of that in this plugin

- `mutes` Same as above but for mutes

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
[Click here](cases.md)
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

