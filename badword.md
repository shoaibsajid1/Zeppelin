Badword filter

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
    add_to_counter:
      counter: "badword_counter"
      amount: 1 # This infraction adds 1 automod infraction points```
