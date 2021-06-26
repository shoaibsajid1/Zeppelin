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



```yaml

  automod:
    config:
      rules:
        badwords:
          enabled: true
          triggers:
          - match_words:
              words:
              - retard
              - e-girl
              - boobs
              - asshole
              - dick
              - cnut
              - dick
              - blowjob
              - slut
              - b1tch
              - slut
              - bitch
              - c0ck
              - pussy
              - thot
              - cunt
              - fuk
              - bitches
              - penis
              case_sensitive: true
              only_full_words: true
              normalize: true
              loose_matching: false
              loose_matching_threshold: 0
              strip_markdown: true
              match_messages: true
              match_embeds: true
              match_visible_names: false
          - match_regex:
              patterns:
                - 'fuck'
                - 'n[il1]+g{2,}(er|a)' #nigger
                - "n[\\s.\\-]*[i1][\\s.\\-]*[g6][\\s.\\-]*[g6][\\s.\\-]*[e3][\\s.\\-]*r" #nigger
                - "n[\\s.\\-]*[i1][\\s.\\-]*[g6][\\s.\\-]*[g6][\\s.\\-]*a" #nigga
                - "f[\\s.\\-]*a[\\s.\\-]*[g6][\\s.\\-]*[g6][\\s.\\-]*o[\\s.\\-]*[t7]" #faggot
              normalize: true
              strip_markdown: true
              match_messages: true
              match_embeds: true
              match_visible_names: false
          actions:
            clean: true
            reply:
              text: |-
                <@{user.id}> sent a bad word (sample detection)
            add_to_counter:
              counter: "badword_counter"
              amount: 1 # This infraction adds 1 automod infraction points
        copypasta:
          enabled: true
          triggers:
            - match_regex:
                patterns:
                  - "[⠁⠂⠃⠄⠅⠆⠇⠈⠉⠊⠋⠌⠍⠎⠏⠐⠑⠒⠓⠔⠕⠖⠗⠘⠙⠚⠛⠜⠝⠞⠟⠠⠡⠢⠣⠤⠥⠦⠧⠨⠩⠪⠫⠬⠭⠮⠯⠰⠱⠲⠳⠴⠵⠶⠷⠸⠹⠺⠻⠼⠽⠾⠿]"
                  - "[░▐▌█▀▄]"
                  - \# - "^(\\s*\\|\\|.+?\\|\\|\\s*)+$"
                  - (?:[\u2500-\u25FF\u2800-\u28FF]\s*){4,}
                  - '▐▀█▀▌'
                  - ⠟⠑⡄⠀⠀⠀⠀⠀⠀⠀ ⣀⣀⣤⣤⣤⣀⡀
                  - ඞ
                  - ████
                  - ⣿⣿⣿
                case_sensitive: false
                normalize: true
                strip_markdown: true
                match_messages: true
                match_embeds: true
          actions:
            log: true
            alert:
                channel: "831498216704049172" #dashboard
                text: |-
                  :bust_in_silhouette: **Mention:** <@!{user.id}>
                  :credit_card: **ID:** `{user.id}`
                  :construction: **Violation:** Copy Pasta detcted words in chat!
                  :warning: **Action:** Nothing . Mod may take action in chat if needed

                  :information_source: **Details:** {matchSummary}
            add_to_counter:
              counter: "automod"
              amount: 2 # This infraction adds 1 automod infraction points
        auto_nick:
          enabled: false
          triggers:
          - match_words:
              words:
                - 'w̴̅́'
                - 'ñ̷͝'
                - '꧁'
                - '𝓔'
                - '𝓟'
                - '𝓘'
                - '𝓒'
                - '𝓖'
                - '𝓞'
                - '𝓓'
                - '꧂'
                - '𝓮'
                - '𝓻'
                - '𝓲'
                - '𝓴'
                - '𝓪'
                - '﷽'
                - '𝖋'
                - '𝖑'
                - '𝖙'
                - '𒐫'
                - 'd̶̀̃'
                - 'a̷͒̍'
                - '𝖗'
                - '𝖝'
                - 'ȶ'
                - 'ʊ'
                - 'ȶ'
                - '҉҉'
                - '𝐓'
                - '박'
                - '의'
                - '윤'
                - '𝐇'
                - '𝕿'
                - '𝕺'
                - '𝐄'
                - 'ム'
                - '✧'
                - '▄'
                - 'ㄒ'
                - '乃'
                - '卂'
                - 'ᗪ'
                - 'ℳ'
                - 'Ⱡ'
                - '₳'
                - 'Ɽ'
                - 'Ӿ'
                - 'Ø'
                - '𝒶'
                - '𝓁'
                - '𝒾'
                - '𝓀'
                - '乃'
                - 'ㄖ'
                - 'ㄚ'
                - 'ᴇ'
                - 'ᴠ'
                - 'ɪ'
                - 'ʟ'
                - '𝕥'
                - '𝕒'
                - '𝕣'
                - '𝕕'
                - 'ᴇ'
                - 'ᴠ'
                - 'ᴇ'
                - 'ʀ'
                - 'ʏ'
                - '𝐘'
                - '𝓔'
                - '𝓚'
                - '🄲'
                - '🄷'
                - '🄴'
                - '🅁'
                - '🅁'
                - '🅈'
                - '𝓐'
                - '𝓜'
                - '╗'
                - '╚'
                - '𝐊'
                - '𝐍'
                - '𝐈'
                - '𝓐'
                - '𝔃'
                - '𝓾'
                - '𝓻'
                - '𝓴'
                - '𝓲'
                - '𝓪'
                - '𝐆'
                - '𝐇'
                - '𝓛'
                - '𝓸'
                - '˞˞˞˞˞˞˞˞˞˞˞˞˞˞˞˞˞˞˞˞'
                - '𝓵'
                - 'お'
                - 'み'
                - 'わ'
                - '𝐓'
                - 'ペ'
                - '』'
                - '『'
                - '╲'
                - '⎝'
                - '⧹'
                - 'Ξ'
                - 'ت'
                - '☆'
                - 'M̸'
                - 'п'
                - 'и'
                - 'в'
                - 'т'
                - 'м'
                - 'г'
                - '𒅌'
                - 'nigger'
                - '𝓻'
                - '𝓪'
                - '𝓭'
                - '𝓴'
                - '𝓪'
                - '𝓽'
                - '🅔'
                - '🅧'
                - '🅘'
                - '🅢'
                - '🅣'
                - '╾'
                - '━'
                - '╤'
                - 'デ'
                - '╦'
                - '︻'
                - '🅔'
                - '🅝'
                - '🅣'
                - 'Ù̸͑'
                - 'ň̸͂'
                - 'ḱ̸͉'
                - 'ń̷̃'
                - 'ő̵̔'
                - 'w̶̓͋'
                - 'n̴̅̀'
                - '🅗'
                - '𝒮'
                - '𝒦'
                - '𝒴'
                - '🅤'
                - '🅝'
                - 'ة'
                - 'ا'
                - 'ث'
                - 'س'
                - 'ؤ'
                - '🅣'
                - 'ᵃ'
                - 'ᵉ'
                - 'ʳ'
                - 'ᵒ'
                - '🅔'
                - '🅡'
                - '❼'
                - '꧅'
                - '𝕮'
                - '𝖍'
                - '𝖎'
                - '𝖈'
                - '𝖐'
                - '𝖊'
                - '𝖓'
                - '𝕔'
                - '𝕓'
                - '𝕖'
                - '𝕫'
                - 'ȶ'
                - 'ȶ'
                - 'ʟ'
                - 'ɛ'
                - 'Ｌ'
                - 'ｉ'
                - 'ａ'
                - 'ｍ'
                - '҉҉'
                - '𝓫'
                - '𝓮'
                - '𝓼'
                - '𝓽'
                - '𝓤'
                - '𝓝'
                - '𝓡'
                - '𝓤'
                - '𝓛'
                - '𝓨'
                - '𝕋'
                - '𝔾'
                - '𝔸'
                - '𝕄'
                - '𝔼'
                - 'ℝ'
              case_sensitive: false
              match_messages: false
              match_embeds: false
              match_visible_names: true
              only_full_words: false
              loose_matching: true
              loose_matching_threshold: 50
          actions:
            #clean: true
            log: true
            #alert:
              #channel: "831498216704049172" #zep channel
              #text: |-
                #Unique nick detected
            #warn:
              #reason: >-
                #Please ensure that your name does not contain any Zalgo text, racial slurs, or anything against the rules of the GTAO discord server.

                #Your nickname has been automatically changed to an empty one. If you believe this action to be in error, please message Modmail (<@698237346537013338>) and explain your reasoning.
            #change_nickname:
              #name: >-
                #Change Nickname | Auto
        invites:
          enabled: false
          triggers:
          - match_invites:
              allow_group_dm_invites: true
              exclude_guilds: []
              match_messages: true
              match_embeds: true
              match_visible_names: false
              exclude_invite_codes:
                - rey #rey server
                - tribegaming #tribegaming server
          actions:
            log: true
            clean: true
            reply:
              text: |-
                <@{user.id}> sent an invite (sample detection)
            add_to_counter:
              counter: "automod"
              amount: 1 # This infraction adds 1 automod infraction points
        non_latin_character_block:
                  enabled: false
                  affects_bots: false
                  triggers:
                  - match_regex:
                      patterns:
                        - "[\u0600-\u06FF]+" # Arabic
                        - "(\u0196|\u0214|\u0220|\u0223|\u0228|\u0246|\u0252)+" # German
                        - "(\u0192|\u0194|\u0196|\u0198|\u0199|[\u0200-\u0204]|\u0206|\u0207|\u0210|\u0212|\u0140|\u0217|\u0219|\u0220|\u0224|\u0226|\u0228|\u0230|\u0231|[\u0232-\u0236]|\u0238|\u0239|\u0244|\u0244|\u0156|\u0249|\u0251|\u0252)+" # French/Italian
                        - "(\u0161|\u0191|\u0193|\u0201|\u0205|\u0209|\u0211|\u0218|\u0220|\u0225|\u0233|\u0237|\u0241|\u0243|\u0250|\u0252)+" #Spanish
                        - "[\u4e00-\u9faf\u3400-\u4dbf]+" # Chinese
                        - "[\u0400-\u04FF]+" # Cryllic (Russian)
                        - "[\u0370-\u03FF]+" # Greek
                        - "[\u1F00-\u1FFF]+" # Greek Extended
                        - "[\u05BE-\u05F4]+" # Hebrew
                        - "(?![ツ])[\u30A0-\u30FF]+" # Japanese (Hiragana)
                        - "(?![ツ])[\u30A0-\u30FF]+" # Japanese (Kana)
                  actions:
                    clean: false
                    add_to_counter:
                      counter: "automod"
                      amount: 1
                    reply:
                      text: |-
                        Non latin detected
        dex_ping:
                  enabled: true
                  affects_bots: false
                  triggers:
                  - match_regex:
                      patterns:
                        - '(?:<@!473868086773153793>)'
                        - '<@473868086773153793>'

                  actions:
                    log: true
                    alert:
                      channel: "831498216704049172" #zep channel
                      text: |-
                        <@{user.id}> pinged zep (detected)
                    reply:
                      text:
                        embed:
                          title: "Sigh."
                          description: "So you pinged me. What did that get you? No seriously, tf did u think was gonna happen. Did u expect me to magically KNOW what you want? Dont i do enough already that I have to take care of your bullshit pings? I am seriously at my limit Timothy."
                          color: 0xFF0000
        nitro_role_remove:
          enabled: false
          triggers:
            - role_removed: ['797739346807226378'] #nitro role
          actions:
            remove_roles:
              - '798505084132524043' #color of the month nitro
            alert:
              channel: "770256340639416320" #testing
              text: >-
                :red_circle: <@!{user.id}> One role removed so other gone as well!
        new_joins:
          enabled: true
          triggers:
          - member_join:
              only_new: true
              new_threshold: 1h
          actions:
              alert:
                channel: "770256340639416320" #home
                text: >-
                  :red_circle: <@{user.id}> is a new account! Be vary
        media:
          enabled: false
          triggers:
          #- match_links:
              #exclude_regex:
                  #- ''
            - match_regex:
                patterns:
                  - '^((?!https?:\/\/\S+\.(gif|jpe?g|png|webp|mov|m4a|mp4|webm)).)*$'
            - match_attachment_type:
                whitelist_enabled: true
                filetype_whitelist:
                  - png
                  - jpg
                  - jpeg
                  - gif
                  - mp4
                  - avi
                  - txt
                  - PNG
                  - JPG
                  - JPEG
                  - GIF
                  - MP4
                  - AVI
                  - TXT
          actions:
            clean: false
            #media only channel when used with override
            alert:
              channel: "831498216704049172" #zep channel
              text: |-
                  Media file detected at {messageLink}
        autorole:
          enabled: false
          affects_bots: false
          triggers:
            - any_message: {}
          actions:
            log: true
            add_roles:
              - "832922355009060894" #dexians
        booster_added_filter:
          enabled: true
          triggers:
          - role_added: ['618663125016641537'] #booster role
          actions:
            alert:
              channel: "808334772102234142" #misc channel
              text: >-
                :green_circle: <@!{user.id}> Just boosted Server! (alert)
        booster_remove_filter:
          enabled: true
          triggers:
          - role_removed: ['618663125016641537'] #booster role
          actions:
            remove_roles:
              - '754619197358604389' #blue
              - '753514538820698133' #red
              - '762207737857703946' #green
              - '762207748732747818' #yellow
              - '762207747592028160' #purple
              - '772424797719625749' #brown
              - '772424620149833748' #white
            alert:
              channel: "572122519616749586" #mod chat
              text: >-
                :red_circle: <@!{user.id}> stopped boosting! Pls check if roles were removed (alert)
        bad_name:
          enabled: false
          triggers:
          - match_regex:
              patterns:
                - fuck
                - retard
                - e-girl
                - boobs
                - asshole
                - dick
                - cnut
                - dick
                - blowjob
                - slut
                - b1tch
                - slut
                - bitch
                - c0ck
                - pussy
                - thot
                - cunt
                - fuk
                - bitches
                - penis
                #- '[^a-zA-Z0-9\s\-_().!?$%*=#,:;\x27"éè$&°#@&øçàœëツï|öä:tm:ù\\/]' #stricter non-alphanumeric regex to make sure its ALWAYS readable. kinda doesnt allow any symbols even
              match_messages: false
              match_embeds: false
              match_visible_names: true
              match_usernames: false
              match_nicknames: false
          actions:
            alert:
              channel: "800887873200193536" #dashboard
              text: |-
                :bust_in_silhouette: **Mention:** <@!{user.id}>
                :credit_card: **ID:** `{user.id}`
                :construction: **Violation:** Bad nickname!
                :warning: **Action:** Warned & Changed name

                :information_source: **Details:** {matchSummary}
        delete_cmds:
          enabled: false
          triggers:
          - match_regex:
              patterns:
                - ^!warn\b
                - ^!mute\b
                - ^!ban\b
              case_sensitive: false
              only_full_words: false
          actions:
            clean: true
            log: false
        role_remove_to_remove_other_roles:
          enabled: false
          triggers:
          - role_removed: ['766917936995762216'] #3 is removed
          actions:
            remove_roles:
              - '766917766699024425' #5
              - '754619197358604389' #blue
              - '753514538820698133' #red
              - '762207737857703946' #green
              - '762207748732747818' #yellow
              - '762207747592028160' #purple
              - '772424797719625749' #brown
              - '772424620149833748' #white
        phonenumber:
          enabled: false
          triggers:
          - match_regex:
              patterns:
                - (?:^|[^0-9])(1[34578][0-9]{9})(?:$|[^0-9])
          actions:
            clean: true
            reply:
              text: >-
                <@!{user.id}> Phone numbers are not allowed!
              auto_delete: 7s
            alert:
              channel: "800887873200193536" #automod channel
              text: |-
                :link: <@!{user.id}>(`{user.id}`) sent a phone number!
                {matchSummary}
                *Automatically Cleaned*
        irl_name_protection:
          enabled: false
          triggers:
          - match_regex:
              patterns:
                - davis mathew|davis
          actions:
            clean: true
            alert:
              channel: "800887873200193536" #automod channel
              text: |-
                :link: <@!{user.id}>(`{user.id}`) said nats name!
                {matchSummary}
                *Automatically Cleaned*
        blocked_links:
          #THIS WILL REMAIN FALSE BECAUSE WE USE CROSSLINK FOR LINK MONITORING
          enabled: false
          triggers:
            - match_words:
                only_full_words: false
                normalize: true
                loose_matching: true
                words:
                  - Libra coin
                  - libra-coin
            - match_links:
                include_subdomains: true
                only_real_links: false # Also match links that don't get highlighted
                include_domains:
                  # Malware
                  - selfbot.cc
                  - catsnthing.com
                  - catsnthings.fun
                  - destyy.com
                  - fortnight.space
                  - särahah.pl
                  - särahah.eu

                  # Porn/NSFW sites
                  - hanime.tv
                  - pornhub.com
                  - 997sexy.com
                  - homefilm.com
                  - 113girl.com
                  - fuq.com

                  #IP loggers/Grabify
                  - stopify.co
                  - iplogger.org
                  - blasze.tk
                  - iplo.ru
                  - iplogger.com
                  - iplogger.ru
                  - yip.su
                  - iplogger.co
                  - iplogger.org
                  - ipgrabber.ru
                  - ipgraber.ru
          actions:
            clean: true
            reply:
              text: >-
                <@!{user.id}> That was a banned link!
            alert:
              channel: "800887873200193536" #automod channel
              text: |-
                :link: <@!{user.id}>(`{user.id}`) sent a bad link!
                {matchSummary}
                *Automatically Cleaned*
        Remove_owner_impersonation: #dont allow same name as owner
          enabled: false
          triggers:
          - match_words:
              words:
                - 'nat ♡'
              case_sensitive: false
              match_messages: false
              match_embeds: false
              match_visible_names: true
              only_full_words: true
              loose_matching: false
              loose_matching_threshold: 50
          actions:
            clean: true
            log: true
            change_nickname:
              name: >-
                Change your name
        message:
          enabled: false
          triggers:
          - message_spam:
              amount: 16
              within: 7s
          actions:
            clean: true
            log: true
            alert:
              channel: "800887873200193536" #dashboard
              text: |-
                :link: <@!{user.id}>(`{user.id}`) was spamming too fast!
                {matchSummary}
                *Automatically Cleaned*
        attachment:
          enabled: false
          triggers:
          - attachment_spam:
              amount: 8
              within: 8s
          actions:
            clean: true
            log: true
            alert:
              channel: "800887873200193536" #dashboard
              text: |-
                :link: <@!{user.id}>(`{user.id}`) was sending too many attachments!
                {matchSummary}
                *Automatically Cleaned*
        mention:
          enabled: false
          triggers:
          - mention_spam:
              amount: 6
              within: 7s
              per_channel: false
          actions:
            clean: false
            log: true
            alert:
              channel: "800887873200193536" #dashboard
              text: |-
                :link: <@!{user.id}>(`{user.id}`) was sending too many mentions!
                {matchSummary}
                *Automatically Cleaned*
        link:
          enabled: false
          triggers:
          - link_spam:
              amount: 5
              within: 30s
              per_channel: false
          actions:
            clean: true
            log: true
            alert:
              channel: "800887873200193536" #dashboard
              text: |-
                :link: <@!{user.id}>(`{user.id}`) was sending too many links!
                {matchSummary}
                *Automatically Cleaned*
        emoji:
          enabled: false
          triggers:
          - emoji_spam:
              amount: 15
              within: 20s
              per_channel: false
          actions:
            clean: true
            log: true
            alert:
              channel: "800887873200193536" #dashboard
              text: |-
                :link: <@!{user.id}>(`{user.id}`) was sending too many emojis!
                {matchSummary}
                *Automatically Cleaned*
        line:
          enabled: false
          triggers:
          - line_spam:
              amount: 14
              within: 26s
              per_channel: false
          actions:
            clean: true
            log: true
            alert:
              channel: "800887873200193536" #dashboard
              text: |-
                :link: <@!{user.id}>(`{user.id}`) was flooding!
                {matchSummary}
                *Automatically Cleaned*
        character:
          enabled: false
          triggers:
          - character_spam:
              amount: 2000
              within: 10s
              per_channel: false
          actions:
            clean: true
            log: true
            alert:
              channel: "800887873200193536" #dashboard
              text: |-
                :link: <@!{user.id}>(`{user.id}`) was sending too many characters!
                {matchSummary}
                *Automatically Cleaned*
        message_med:
          enabled: false
          triggers:
          - message_spam:
              amount: 7
              within: 12s
          actions:
            clean: true
            log: true
            alert:
              channel: "800887873200193536" #dashboard
              text: |-
                :link: <@!{user.id}>(`{user.id}`) was spamming messages!
                {matchSummary}
                *Automatically Cleaned*
        attachment_med:
          enabled: false
          triggers:
          - attachment_spam:
              amount: 5
              within: 20s
          actions:
            clean: true
            log: true
            alert:
              channel: "800887873200193536" #dashboard
              text: |-
                :link: <@!{user.id}>(`{user.id}`) was sending too many attachments!
                {matchSummary}
                *Automatically Cleaned*
        mention_med:
          enabled: false
          triggers:
          - mention_spam:
              amount: 4
              within: 7s
              per_channel: false
          actions:
            clean: false
            log: true
            alert:
              channel: "800887873200193536" #dashboard
              text: |-
                :link: <@!{user.id}>(`{user.id}`) was sending too many mentions!
                {matchSummary}
                *Automatically Cleaned*
        link_med:
          enabled: false
          triggers:
          - link_spam:
              amount: 4
              within: 10s
              per_channel: false
          actions:
            clean: true
            log: true
            alert:
              channel: "800887873200193536" #dashboard
              text: |-
                :link: <@!{user.id}>(`{user.id}`) was sending too many links!
                {matchSummary}
                *Automatically Cleaned*
        emoji_med:
          enabled: false
          triggers:
          - emoji_spam:
              amount: 10
              within: 15s
              per_channel: false
          actions:
            clean: true
            log: true
            alert:
              channel: "800887873200193536" #dashboard
              text: |-
                :link: <@!{user.id}>(`{user.id}`) was sending too many emojis!
                {matchSummary}
                *Automatically Cleaned*
        line_med:
          enabled: false
          triggers:
          - line_spam:
              amount: 10
              within: 7s
              per_channel: false
          actions:
            clean: true
            log: true
            alert:
              channel: "800887873200193536" #dashboard
              text: |-
                :link: <@!{user.id}>(`{user.id}`) was flooding!
                {matchSummary}
                *Automatically Cleaned*
        character_med:
          enabled: false
          triggers:
          - character_spam:
              amount: 1000
              within: 10s
              per_channel: false
          actions:
            clean: true
            log: true
            alert:
              channel: "800887873200193536" #dashboard
              text: |-
                :link: <@!{user.id}>(`{user.id}`) was sending too many characters!
                {matchSummary}
                *Automatically Cleaned*
        message_high:
          enabled: false
          triggers:
          - message_spam:
              amount: 9
              within: 7s
          actions:
            clean: true
            log: true
            alert:
              channel: "800887873200193536" #dashboard
              text: |-
                :link: <@!{user.id}>(`{user.id}`) was spamming too fast!
                {matchSummary}
                *Automatically Cleaned*
        attachment_high:
          enabled: false
          triggers:
          - attachment_spam:
              amount: 3
              within: 10s
          actions:
            clean: true
            log: true
            alert:
              channel: "800887873200193536" #dashboard
              text: |-
                :link: <@!{user.id}>(`{user.id}`) was sending too many attachments!
                {matchSummary}
                *Automatically Cleaned*
        mention_high:
          enabled: false
          triggers:
          - mention_spam:
              amount: 3
              within: 7s
              per_channel: false
          actions:
            clean: false
            log: true
            alert:
              channel: "800887873200193536" #dashboard
              text: |-
                :link: <@!{user.id}>(`{user.id}`) was sending too many mentions!
                {matchSummary}
                *Automatically Cleaned*
        link_high:
          enabled: false
          triggers:
          - link_spam:
              amount: 2
              within: 10s
              per_channel: false
          actions:
            clean: true
            log: true
            alert:
              channel: "800887873200193536" #dashboard
              text: |-
                :link: <@!{user.id}>(`{user.id}`) was sending too many links!
                {matchSummary}
                *Automatically Cleaned*
        emoji_high:
          enabled: false
          triggers:
          - emoji_spam:
              amount: 5
              within: 12s
              per_channel: false
          actions:
            clean: true
            log: true
            alert:
              channel: "800887873200193536" #dashboard
              text: |-
                :link: <@!{user.id}>(`{user.id}`) was sending too many emojis!
                {matchSummary}
                *Automatically Cleaned*
        line_high:
          enabled: false
          triggers:
          - line_spam:
              amount: 7
              within: 15s
              per_channel: false
          actions:
            clean: true
            log: true
            alert:
              channel: "800887873200193536" #dashboard
              text: |-
                :link: <@!{user.id}>(`{user.id}`) was flooding!

                {matchSummary}
        character_high:
          enabled: false
          triggers:
          - character_spam:
              amount: 200
              within: 15s
              per_channel: false
          actions:
            clean: true
            log: true
            alert:
              channel: "800887873200193536" #dashboard
              text: |-
                :link: <@!{user.id}>(`{user.id}`) was sending too many characters!

                {matchSummary}
        auto_kick:
          enabled: false
          triggers:
          - member_join:
              only_new: true
              new_threshold: 6h
          actions:
            kick:
              reason: "Your account is very new and is marked as suspcious so it got kicked, If you think this is a mistake. Please try joining again in some time (like 30 minutes or so?) at discord.gg/nat"
        high_trigger:
          enabled: true
          triggers:
          - member_join_spam:
              amount: 10
              within: 18s
          actions:
            set_antiraid_level: "high"
            alert:
              channel: "572122519616749586" #modchat
              text: |-
                Dear <@&572104727077322763> It seems like 10 people joined within 18 seconds
                Please watch the chat cuz we might be getting raided. I have increased security (you can see in <#774961064646934578>)
                If this was a mistake . Please turn it back to low by doing `!antiraid low`
        badwordc1:
          # COUNTERS BUT AUTOMOD-----------------------------
          triggers:
            - counter_trigger:
                counter: "badword_counter"
                trigger: "silent"
          actions:
            log: true
        badwordc2:
          triggers:
            - counter_trigger:
                counter: "badword_counter"
                trigger: "verbal"
          actions:
            alert:
              channel: "831498216704049172" #zep channel
              text: |-
                <:iconlink:778925231506587668> **Badword** <:singleplayer:831585796409786439> **<@{user.id}>** <:iconid:778924898176466944> `{user.id}` <:iconbuildoverride:815459629869826048> Verbal Warning (Sample)
        badwordc3:
          triggers:
            - counter_trigger:
                counter: "badword_counter"
                trigger: "warning"
          actions:
            alert:
              channel: "831498216704049172" #zep channel
              text: |-
                <:iconlink:778925231506587668> **Badword** <:singleplayer:831585796409786439> **<@{user.id}>** <:iconid:778924898176466944> `{user.id}` <:iconbuildoverride:815459629869826048> Warning Logged! (Test)
            #warn:
              #reason: "**Badwords detected**. Continuing will result in a mute"
        badwordc4:
          triggers:
            - counter_trigger:
                counter: "badword_counter"
                trigger: "mute"
          actions:
            log: true
            clean: true
            #mute:
              #reason: "**Badwords violation**"
              #duration: 10s
              #remove_roles_on_mute: true
              #restore_roles_on_mute: true
            set_counter:
              counter: "badword_counter"
              value: 0
            alert:
              channel: "831498216704049172" #zep channel
              text: |-
                <:iconlink:778925231506587668> **Badword** <:singleplayer:831585796409786439> **<@{user.id}>** <:iconid:778924898176466944> `{user.id}` <:iconbuildoverride:815459629869826048> Mute! (10s test)
        accumulate_xp:
          # XP START----------------------------------------------------------------------
          enabled: true
          triggers:
            - any_message: {}

          actions:
            log: false # Don't spam logs with XP changes
            add_to_counter:
              counter: "xp"
              amount: 1 # Each message adds 1 XP

          cooldown: 1m # Only count 1 message per minute
        add_xp_role_1:
          triggers:
            - counter_trigger:
                counter: "xp"
                trigger: "role_1"

          actions:
            add_roles: ["827840992111099935"] # Role ID for xp role 1 bronze
        add_xp_role_2:
          triggers:
            - counter_trigger:
                counter: "xp"
                trigger: "role_2"

          actions:
            add_roles: ["827841264489725983"] # Role ID for xp role 2 silver
        add_xp_role_3:
          triggers:
            - counter_trigger:
                counter: "xp"
                trigger: "role_3"

          actions:
            add_roles: ["827841321716678698"] # Role ID for xp role 3 gold
        add_xp_role_4:
          triggers:
            - counter_trigger:
                counter: "xp"
                trigger: "role_4"

          actions:
            add_roles: ["827841368374247454"] # Role ID for xp role 4 platinum
        accumulate_activity:
          # ACTIVITY START----------------------------------------------------------------------
          triggers:
            - any_message: {}

          actions:
            log: false # Don't spam logs with activity changes
            add_to_counter:
              counter: "activity"
              amount: 1 # Each message adds 1 to the counter

          cooldown: 1m # Only count 1 message per minute
        grant_activity_role:
          triggers:
            - counter_trigger:
                counter: "activity"
                trigger: "grant_role"

          actions:
            add_roles: ["828659945158737931"] # Role ID for activity role
        remove_activity_role:
          triggers:
            - counter_trigger:
                counter: "activity"
                trigger: "grant_role"
                reverse: true # This indicates we want to use the *reverse* of the specified trigger, see reverse_condition in counters above

          actions:
            remove_roles: ["828659945158737931"] # Role ID for activity role
        accumulate_stars:
          # DEX STARS (ATTENDENCE)----------------------------------------------------------------------
          triggers:
            - match_words:
                words:
                - present
                case_sensitive: false
          actions:
            log: true # Don't spam logs with activity changes
            add_to_counter:
              counter: "stars"
              amount: 1 # Each message adds 1 to the counter

          #cooldown: 30s # Only count 1 message per 30s
        grant_star_role:
          triggers:
            - counter_trigger:
                counter: "stars"
                trigger: "grant_star"

          actions:
            add_roles: ["808718941785554985"] # Role ID for star role
        remove_star_role:
          triggers:
            - counter_trigger:
                counter: "stars"
                trigger: "grant_star"
                reverse: true # This indicates we want to use the *reverse* of the specified trigger, see reverse_condition in counters above

          actions:
            remove_roles: ["808718941785554985"] # Role ID for star role

    overrides:
    - extra:
        antiraid_level: "off"
      config:
        rules:
          invites:
            enabled: false
    - extra:
        antiraid_level: "low"
      config:
        rules:
          message:
            enabled: false
          attachment:
            enabled: false
          mention:
            enabled: false
          link:
            enabled: false
          emoji:
            enabled: false
          line:
            enabled: false
          character:
            enabled: false
          badwords:
            enabled: false
    - level: '>=50'
      config:
        can_view_antiraid: true
        can_set_antiraid: true
        rules:
          delete_cmds:
            enabled: true
    - any:
      - all:
        - level: '<=30'
          #role: "172950000412655616"
        - extra:
            antiraid_level: "low"
        - not:
            level: '100'
      config:
        rules:
          invites:
            enabled: true
            actions:
              warn:
                reason: 'Sending server invite. Continuing will result in mute/ban'
              reply:
                text: >-
                  <@!{user.id}> No server invites pls
                auto_delete: 70s
            alert:
              channel: "800887873200193536" #dashboard channel
              text: |-
                :bust_in_silhouette: **Mention:** <@!{user.id}>
                :credit_card: **ID:** `{user.id}`
                :warning: **Action:** Auto-Warn

                :information_source: **Details:** {matchSummary}

          badwords:
            enabled: false

          bad_name:
            enabled: true
            actions:
              warn:
                reason: "Please change your nickname in the server"
              change_nickname:
                name: "Nickname cleared"
              reply:
                text: >-
                  <@!{user.id}> Your name has been changed. Please check your dms.
                auto_delete: 70s

          phonenumber:
            enabled: false
            actions:
              warn:
                reason: 'Phone numbers are not allowed on server'
              reply:
                text: >-
                  <@!{user.id}> Phone numbers are not allowed!
                auto_delete: 70s

          blocked_links:
            enabled: false
            actions:
              warn:
                reason: 'Blocked Link Detected'
              reply:
                text: >-
                  <@!{user.id}> That link is blocked.
                auto_delete: 70s

          message:
            enabled: false
            actions:
              reply:
                text: >-
                  <@!{user.id}> Oh no! You were spamming too fast!
              mute:
                duration: 5m
                reason: 'Auto-muted for spam'

          attachment:
            enabled: false
            actions:
              reply:
                text: >-
                  <@!{user.id}> Please dont send so many images at once!
              mute:
                duration: 5m
                reason: 'Auto-muted for attachment spam'

          mention:
            enabled: false
            actions:
              reply:
                text: >-
                  <@!{user.id}> Please dont send so many images!
              mute:
                reason: >-
                  Auto-muted for mass ping
                duration: 10m

          link:
            enabled: false
            actions:
              reply:
                text: >-
                  <@!{user.id}> Please dont spam links!
              mute:
                reason: >-
                  Auto-muted for link spam
                duration: 10m

          emoji:
            enabled: false
            actions:
              reply:
                text: >-
                  <@!{user.id}> Please dont send so many images!
              mute:
                reason: >-
                  Antispam Triggered
                duration: 10m

          line:
            enabled: false
            actions:
              reply:
                text: >-
                  <@!{user.id}> Please dont send so many images!
              mute:
                reason: >-
                  Antispam Triggered
                duration: 10m

          character:
            enabled: false
            actions:
              reply:
                text: >-
                  <@!{user.id}> Please dont send so many images!
              mute:
                reason: >-
                  Antispam Triggered
                duration: 10m
    - any:
      - all:
        - level: '<=30'
          #role: "172950000412655616"
        - extra:
            antiraid_level: "medium"
        - not:
            level: '100'
      config:
        rules:
          message_med:
            enabled: false
            actions:
              reply:
                text: >-
                  <@!{user.id}> Oh no! You were spamming too fast!
              mute:
                duration: 5m
                reason: 'Auto-muted for spam'
          attachment_med:
            enabled: false
            actions:
              reply:
                text: >-
                  <@!{user.id}> Please dont send so many images!
              mute:
                duration: 5m
                reason: 'Auto-muted for attachment spam'
          mention_med:
            enabled: false
            actions:
              reply:
                text: >-
                  <@!{user.id}> Please dont send so many images!
              mute:
                reason: >-
                  Antispam Triggered
                duration: 10m
          link_med:
            enabled: false
            actions:
              reply:
                text: >-
                  <@!{user.id}> Please dont send so many images!
              mute:
                reason: >-
                  Antispam Triggered
                duration: 10m
          emoji_med:
            enabled: false
            actions:
              reply:
                text: >-
                  <@!{user.id}> Please dont send so many images!
              mute:
                reason: >-
                  Antispam Triggered
                duration: 10m
          line_med:
            enabled: false
            actions:
              reply:
                text: >-
                  <@!{user.id}> Please dont send so many images!
              mute:
                reason: >-
                  Antispam Triggered
                duration: 10m
          character_med:
            enabled: false
            actions:
              reply:
                text: >-
                  <@!{user.id}> Please dont send so many images!
              mute:
                reason: >-
                  Antispam Triggered
                duration: 10m
    - any:
      - all:
        - level: '<=30'
          #role: "172950000412655616"
        - extra:
            antiraid_level: "high"
        - not:
            level: '100'
      config:
        rules:
          message_high:
            enabled: false
            actions:
              reply:
                text: >-
                  <@!{user.id}> Oh no! You were spamming too fast!
              mute:
                duration: 5m
                reason: 'Auto-muted for spam'

          attachment_high:
            enabled: false
            actions:
              reply:
                text: >-
                  <@!{user.id}> Please dont send so many images!
              mute:
                duration: 5m
                reason: 'Auto-muted for attachment spam'

          mention_high:
            enabled: false
            actions:
              reply:
                text: >-
                  <@!{user.id}> Please dont mass ping people
              mute:
                reason: >-
                  Mention Spam
                duration: 10m

          link_high:
            enabled: false
            actions:
              reply:
                text: >-
                  <@!{user.id}> Please dont send so many images!
              mute:
                reason: >-
                  Link Spam
                duration: 10m

          emoji_high:
            enabled: false
            actions:
              reply:
                text: >-
                  <@!{user.id}> Please dont send so many images!
              mute:
                reason: >-
                  Emoji Spam
                duration: 10m

          line_high:
            enabled: false
            actions:
              reply:
                text: >-
                  <@!{user.id}> Please dont send so many images!
              mute:
                reason: >-
                  Mutiple Line Spam
                duration: 10m

          character_high:
            enabled: false
            actions:
              reply:
                text: >-
                  <@!{user.id}> Please dont send so many images!
              mute:
                reason: >-
                  Character Spam
                duration: 10m
  counters:
    config:
      counters:
        xp:
          per_user: true
          triggers:
            role_1:
              condition: ">=100"
            role_2:
              condition: ">=250"
            role_3:
              condition: ">=500"
            role_4:
              condition: ">=1000"

        activity:
          per_user: true
          triggers:
            grant_role:
              condition: ">=5"
              # We set a separate threshold for when the role should be removed. This is so the decay doesn't remove the activity role immediately.
              # If this value isn't set, reverse_condition defaults to the opposite of the condition, i.e. "<100" in this case.
              reverse_condition: "<1"
          decay:
            amount: 1
            every: 72h

        stars:
          per_user: true
          triggers:
            grant_star:
              condition: ">=7"
              # We set a separate threshold for when the role should be removed. This is so the decay doesn't remove the star role immediately.
              # If this value isn't set, reverse_condition defaults to the opposite of the condition, i.e. "<1" in this case.
              reverse_condition: "<1"
          decay:
            amount: 1
            every: 72h

        badword_counter:
          per_user: true
          triggers:
            silent:
              condition: ">=1"
            verbal:
              condition: ">=2"
            warning:
              condition: ">=3"
            mute:
              condition: ">=4"
          # Remove 1 automod infraction points per 20s
          decay:
            amount: 1
            every: 20s

        antiraid_decay:
          triggers:
            disable:
              condition: "<1"
          decay:
            amount: 1
            every: 1m
      can_view: true
      can_edit: false
      can_reset_all: false
    overrides:
      - level: '>=50'
        config:
          can_view: true
      - level: '>=100'
        config:
          can_edit: true
```
