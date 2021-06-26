# Zep by DEX
Zeppelin is a moderation bot for Discord, and I am DEX....I dont know where I am going with this....Anyways

This is my repo for tips and tricks for Dragorys Bot

## PLUGINS:

**CURRENTLY UNDER CONSTRUCTION**
To follow updates you can join my server and keep an eye on the github channel for updates on the changes i make
on https://discord.gg/JCZf3sHYpE

[Locate User](locate.md)

[Reminders](reminder.md)

[Utility](utility.md)

[Mutes & Modactions](mutes and mod actions.md)

[Companion Channels](companion_channels.md)

[Post](post.md)

[Logs](logs.md)

[Tags](tags.md)

[Automod & Counters](automod+counters.md)

[Reaction Roles](reaction_roles.md)


###  MISCELLANEOUS

💡 **TIP**

>Overrides are always calculated top down. For example,
If you want to have mods messages not be deleted, your overrides would need to be in this order:
>-  Enable in channel xyz
-  Disable for mods
If you have it the other way round it'll delete everything, even from mods.



```yml
    overrides:

    - role: "766285827612999752" #disable rule once role is given
      config:
        rules:
          autorole:
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
```




**MULTIPLE CHANNELS IN OVERRIDE**

```yaml
overrides:
  - channel:
      - "534722948246929429" #channel 1
      - "739034889399042129" #channel 2
    config:
      settings here
```


**SAVE TO DATABASE**

> Zeppelin needs to have the message saved locally to be able to figure out the channel id (which is needed for a lot of things) such as reaction roles!

 `!save_messages_to_db CHANNELID MESSAGEID`



**YAML VALIDATOR**  http://www.yamllint.com/



**ZEPPELIN RESTARTED?**

It restarts in one of these cases:

Many errors in quick succession
Fatal error (instant crash)
Someone restarts it manually
Drag pushes an update



### Example Shots

![Example 1](assets/example1.png)

![Example 2](assets/example2.png)


See https://zeppelin.gg/ for more details.

## Contributing
Pull requests are welcome. For major changes, please open an issue first to discuss what you would like to change.
## More Info

You can find me on the zeppelin support server!
at https://discord.gg/9bCGvGw5rT
