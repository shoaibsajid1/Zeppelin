# AUTOMOD + COUNTERS

**COUNTER TIP**

>Counter decays are currently processed every 5 minutes. They are, however, still applied according to the decay time, even if it's lower than 5 minutes, so "1 every 30s" would decay 10 points at once every 5 minutes.


**COUNTER DECAY**

> Counter decays are currently processed every 5 minutes. They are, however, still applied according to the decay time, even if it's lower than 5 minutes, so "1 every 30s" would decay 10 points at once every 5 minutes.

**LOOSE MATCHING**

`loose_matching` allows a number of letters
(controlled by `loose_matching_threshold`)
*between* letters for word matching
so e.g. if you wanted to match "hello" and enabled `loose_matching`, it would also match e.g. "h|e|l|l|o"

**ALERT TIP**
`replieduser` is whether or not to ping the user you are replying to



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

**REGEX TIP**

`((<a?:[\w~]{2,32}:\d{17,19}>)[\S\s]*?){5,}` - Detect 5 or more emoji's in a message. You can replace 5 with whatever you want.
