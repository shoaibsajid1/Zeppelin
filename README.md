# Zep by DEX
Zeppelin is a moderation bot for Discord, and I am DEX....I dont know where I am going with this....Anyways

This is my repo for tips and tricks for Dragorys Bot

## PLUGINS:

[Locate User](locate.md)

[Reminders](reminder.md)

[Utility](utility.md)

### Mutes
**HOW TO USE AGE AND EXPORT FLAGS IN MUTE COMMAND**
<details>
  <summary>Click to view</summary>

`-export` simply exports the result to an archive link
e.g: `!mutes -e` would give you a link rather than show it all on the channel

`-age` allows you to restrict the command to only show mutes older than X period
e.g: `!mutes -age 2h` would only show mutes that have been active for 2h or longer
</details>

🔇 **HOW TO HARDMUTE**
<details>
  <summary>Click to view</summary>

`remove_roles_on_mute: true` removes roles on mute

`restore_roles_on_mute:true`gives back the roles upon unmute

`kick_from_voice_channel: true` muted users are also immediately kicked from their current voice channel

Bonus!
`remove_roles_on_mute: ["role 1", "role 2"]` those specific roles are removed upon mute
</details>
------------------------------------------

### Welcome
**WELCOME PLUGIN VARIABLES**
<details>
  <summary>Click to view</summary>

`member`, `user`, and `guild`

Usage:
welcome `{user.username}` to `{guild.name}!`
welcome `<@!{user.id}>!`
</details>

### Counters
**COUNTER TIP**

>Counter decays are currently processed every 5 minutes. They are, however, still applied according to the decay time, even if it's lower than 5 minutes, so "1 every 30s" would decay 10 points at once every 5 minutes.




**COUNTER DECAY**

> Counter decays are currently processed every 5 minutes. They are, however, still applied according to the decay time, even if it's lower than 5 minutes, so "1 every 30s" would decay 10 points at once every 5 minutes.

### POST

📮 **SCHEDULED POSTS**

<details>
  <summary>Click to view</summary>
scheduled posts are messages that are scheduled to be posted later, using the `-schedule` option for `!post`,

 e.g. `!post -schedule="2021-02-01 12:00" Some message that is posted on Feb 1 at 12pm`
</details>

### CASES
⏲️ **RELATIVE TIME**
<details>
  <summary>Click to view</summary>

`relative_time_cutoff: 7d`

`relative_time_cutoff` is the amount of time after which `!cases` will show the full date, not a relative time (e.g. "5 hours ago")

so if you set relative time cutoff to 24h, any cases older than 24h would show the full date, e.g. "2021-01-30", rather than e.g. "1 day ago"
</details>



### LOGS
**COMMAND LOG VARIABLE**

This log type is not functional unfortunately. So just skip it!

### MOD ACTION

**MOD ACTION TIP**

`can_act_as_other` allows you to use the `-mod` option for commands such as `!ban` - this will set the case's moderator as the user you specify, and also mention your name below theirs if you view the case

**MOD ACTION TIP**
`create_cases_for_manual_actions` - Manual actions wouls be stuff like right click ban, right click kick

Zepp will take the reason you put and make a case for that action with that reason


### TAGS

💡 **TAG TIP**
<details>
  <summary>Click to view</summary>

`user_tag_cooldown`is the cooldown per user per tag

`global_tag_cooldown` is the global cooldown (server wide) per tag

`user_cooldown` is the cooldown per user (not tag specific)

`global_cooldown` is the global cooldown (server wide) (not tag specific)
</details>

<details>
  <summary>Click to view</summary>

🌡 **TEMPERATURE TAG**

**CtoF** `{if(args.0, if(or(eq(args.0, "0"), not(eq(add(args.0, 1), 1))), concat(add(mul(args.0, div(9, 5)), 32), "**°F**"), ":warning: Temperature must be a number"),":warning: Please provide a temperature to convert")}`

**FtoC** `{if(args.0, if(or(eq(args.0, "0"), not(eq(add(args.0, 1), 1))), concat(mul(sub(args.0, 32), div(5, 9)), "**°C**"), "⚠️ Temperature must be a number"),"⚠️ Please provide a temperature to convert")}`
</details>



**TAGS RESOURCES**
<details>
  <summary>Click to view</summary>

`member / user` here:
https://github.com/Dragory/ZeppelinBot/blob/master/backend/src/plugins/Tags/util/renderTagFromString.ts#L30

base template functions (also available in other places with variables) here:
https://github.com/Dragory/ZeppelinBot/blob/master/backend/src/templateFormatter.ts#L261

tag functions here:
https://github.com/Dragory/ZeppelinBot/blob/master/backend/src/plugins/Tags/TagsPlugin.ts#L116

and a few extra tag things here:
https://github.com/Dragory/ZeppelinBot/blob/master/backend/src/plugins/Tags/util/renderTagBody.ts#L20

useful doc
https://gist.github.com/vcokltfre/8cff17725485f70992c44970f53977fd
</details>


### REACTION ROLE

**REACTION ROLE TIP**
"auto refresh interval" for reaction roles sets how often the reactions are "refreshed", i.e. removed and re-added. This is done because high-volume reactions like reaction roles can become very glitchy after some time if they're not reset.

you can also do this manually with `!reaction_roles refresh MESSAGE_ID`

### AUTOMOD

**LOOSE MATCHING**
<details>
  <summary>Click to view</summary>

 `loose_matching` allows a number of letters
 (controlled by `loose_matching_threshold`)
 *between* letters for word matching
 so e.g. if you wanted to match "hello" and enabled `loose_matching`, it would also match e.g. "h|e|l|l|o"
</details>

**AUTOMOD TIP**

>setting up an automod config that insta-bans people if they mention more than 15 people in the same message
use `mention_spam` with amount 15, within 0s
as the trigger


`only_full_words`
      - if `true`: if it needs to filter `banana` in a message it'll delete `I am a banana` but not `I am a banananan`
      - if `false`: if it needs to filter `banana` in a message it'll delete both `banana` and `bananana`

`normalize`
When enabled, the matched text is normalized (converted to alphanumeric) before matching
        - Allows matching text even when some letters have been replaced by similar looking letters from other alphabets

`loose_matching` and `loose_matching_threshold`
        - When `loose_matching` is enabled, words are matched even when there are other letters or spaces between the letters

        - `loose_matching_threshold` controls how many extra letters, at most, can be between the letters (spaces are unlimited). Defaults to 4.

###  MISCELLANEOUS

💡 **TIP**

>Overrides are always calculated top down. For example,
If you want to have mods messages not be deleted, your overrides would need to be in this order:
>-  Enable in channel xyz
-  Disable for mods
If you have it the other way round it'll delete everything, even from mods.

<details>
  <summary>Click to view code</summary>

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
</details>

---

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
</details>

---

**SAVE TO DATABASE**

> Zeppelin needs to have the message saved locally to be able to figure out the channel id (which is needed for a lot of things) such as reaction roles!

 `!save_messages_to_db CHANNELID MESSAGEID`

 ---

**NOTIFY TIP**

>Available variables are  `off` / `dm` / `channel`

> if using channel, `-notify-channel` is also required to be set!

---

**YAML VALIDATOR**  http://www.yamllint.com/






**REGEX TIP**

`(<a?:[\w~]{2,32}:\d{17,19}>)` is an emoji regex for animated and non-animated emojis.








📣 **GOOD TO KNOW**
the default modifier, if not specified, is `>=`



**LOOKING FOR GROUP**

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

It's a bit of a hack but it works and is clean to tweak. The idea is that anything that does *not* match the `allowed_lfg` rule on the LFG channel gets the actions from the `disallowed_lfg` rule (i.e. clean + reply).

This works because automod only applies one rule per message, so when the `allowed_lfg` rule matches (and does nothing), it doesn't continue matching the other rules anymore.
I also used regex for matching ?lfg only at the beginning of the message
This will be cleaner in the future when you'll be able to do negations in triggers (i.e. `not:`)
and combine them etc.



📣 **GOOD TO KNOW**
Massbans are logged as cases but not automatically posted on your case log channel since it would be very spammy

You *should* be able to see those cases if you do `!cases <userid>` for one of the banned users however



**REGEX TIP**

`((<a?:[\w~]{2,32}:\d{17,19}>)[\S\s]*?){5,}` - Detect 5 or more emoji's in a message. You can replace 5 with whatever you want.



📣 **GOOD TO KNOW**
Massbans are logged as cases but not automatically posted on your case log channel since it would be very spammy

You *should* be able to see those cases if you do `!cases <userid>` for one of the banned users however



<:peepo_ping:714656171763695617> **ALERT TIP** by <@!108552944961454080>
`replieduser` is whether or not to ping the user you are replying to
-----------------------------------------

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
