# AUTOMOD RULES

**BADWORDS**

<details>
  <summary>Click to view code</summary>

```yaml
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
```
</details>


**COPYPASTA**

<details>
  <summary>Click to view code</summary>

```yaml
copypasta: #copy paste spam
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
    reply:
      text:
        content: "<@{user.id}> No copypasta please"
      auto_delete: 10s

```
</details>

**INVITES**

<details>
  <summary>Click to view code</summary>

```yaml
invites:
  enabled: true
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
      text:
        content: "<@{user.id}> Server invites are not allowed"
      auto_delete: 6s
    add_to_counter:
      counter: "spam"
      amount: 1 # This infraction adds 1 automod infraction points
```
</details>

**SPAM**

<details>
  <summary>Click to view code</summary>

```yaml
spam:
  enabled: true
  triggers:
  - message_spam:
      amount: 10
      within: 7s
  - mention_spam:
      amount: 7
      within: 10s
  - link_spam:
      amount: 6
      within: 20s
      per_channel: false
  - attachment_spam:
      amount: 5
      within: 10s
  - emoji_spam:
      amount: 8
      within: 10s
  - line_spam:
      amount: 7
      within: 8s
  - character_spam:
      amount: 4000
      within: 10s
  - sticker_spam:
      amount: 5
      within: 10s
  actions:
    log: true
    clean: false
    reply:
      text:
        content: "<@{user.id}> Spam Detected"
      auto_delete: 6s
    add_to_counter:
      counter: "spam"
      amount: 1 # This infraction adds 1 automod infraction points
```
</details>

**OWNER IMPERSONATION**

<details>
  <summary>Click to view code</summary>

```yaml
owner:
  enabled: true
  triggers:
  - match_words:
      words:
        - 'DEX'
      case_sensitive: false
      match_messages: false
      match_embeds: false
      match_visible_names: true
      only_full_words: true
      loose_matching: false
      loose_matching_threshold: 50
  actions:
    clean: false
    log: true
    reply:
      text:
        content: "<@{user.id}> You can't have the same name as Server Owner"
      auto_delete: 10s
    change_nickname:
      name: >-
        Change your name
```
</details>

**PINGING SOMEONE SPECIFIC VIOLATION**

<details>
  <summary>Click to view code</summary>

```yaml
natping:
  enabled: true
  triggers:
  - match_regex:
      patterns: ['<@!?237661249335328768>']
  actions:
    clean: false
    log: true
    reply:
      text:
        content: "<@{user.id}> One nat ping is fine, continued pings will result in action"
      auto_delete: 10s
    add_to_counter:
      counter: "natping_c"
      amount: 1 # This infraction adds 1 automod infraction points
```
</details>

**ENGLISH ONLY FILTER**

<details>
  <summary>Click to view code</summary>

```yaml
nonenglish: #non english filter
  enabled: true
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
    reply:
      text:
        content: "<@{user.id}> Lets try to keep it english only"
```
</details>
