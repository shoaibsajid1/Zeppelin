# Zep by DEX
Zeppelin is a moderation bot for Discord, and I am DEX....I dont know where I am going with this....Anyways

This is my repo for tips and tricks for Dragorys Bot

## PLUGINS:

**CURRENTLY UNDER CONSTRUCTION**
To follow updates you can join my server and keep an eye on the github channel for updates on the changes i make, u can also follow the channel on your server and leave the server


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
<details>
  <summary>Click to view code</summary>

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



**NOTIFY TIP**

>Available variables are  `off` / `dm` / `channel`

> if using channel, `-notify-channel` is also required to be set!



**YAML VALIDATOR**  http://www.yamllint.com/






📣 **GOOD TO KNOW**
Massbans are logged as cases but not automatically posted on your case log channel since it would be very spammy

You *should* be able to see those cases if you do `!cases <userid>` for one of the banned users however





📣 **GOOD TO KNOW**
Massbans are logged as cases but not automatically posted on your case log channel since it would be very spammy

You *should* be able to see those cases if you do `!cases <userid>` for one of the banned users however



<:peepo_ping:714656171763695617> **ALERT TIP** by <@!108552944961454080>
`replieduser` is whether or not to ping the user you are replying to
--

**ZEPPELIN RESTARTED?**

It restarts in one of these cases:

Many errors in quick succession
Fatal error (instant crash)
Someone restarts it manually
Drag pushes an update


**BAN TIP**

Add this to your ban message to give it that extra zing
![bangif](https://images-ext-1.discordapp.net/external/ca4NEXYwFeI_9-iPkqo747gF5Hlz1iyuXFis1UDhYfM/https/i.imgur.com/V4TVpbC.mp4)

**CLEAN COMMAND TIP**

Deletes everything but image attachments

![clean](https://media.discordapp.net/attachments/846691383280009216/856783756232359946/unknown.png?width=581&height=518)

[Badword](badword.md)

### Example Shots

![Example 1](assets/example1.png)

![Example 2](assets/example2.png)


See https://zeppelin.gg/ for more details.

## Contributing
Pull requests are welcome. For major changes, please open an issue first to discuss what you would like to change.
## More Info

You can find me on the zeppelin support server!
at https://discord.gg/9bCGvGw5rT
