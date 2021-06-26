  companion_channels:
    replaceDefaultOverrides: true #replaces default settings if true
    config:
      entries:
        public_vcs: #name of the entry, could be anything
          voice_channel_ids:
            - "851845471587926086" # c1 vc
          text_channel_ids:
            - "851845490298454026" #v1 text
          #the permissions number are the permissions the user will get in the text channel when they join the voice channel
          #for example u can make it such that a user can only see the text channel when they join the vc
          #this can be calculated using https://discordapi.com/permissions.html
          permissions: 52224
          enabled: true
    overrides:
      - level: '>=50'
        config:
          entries:
            public_vcs:
              enabled: false #disabled for level 50 and up because they likely have perms already so not needed
