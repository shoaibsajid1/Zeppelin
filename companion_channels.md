# COMPANION CHANNELS

Set up 'companion channels' between text and voice channels. Once set up, any time a user joins one of the specified voice channels, they'll get channel permissions applied to them for the text channels.



`permissions` This number can be calculated using  https://discordapi.com/permissions.html which allows you to set the behaviour of the linked channel (e.g read only channel, visible only on vc join etc.)


#### PLUGIN CODE

```yaml
  companion_channels:
    replaceDefaultOverrides: true #replaces default settings if true
    config:
      entries:
        public_vcs: #name of the entry, could be anything
          voice_channel_ids:
            - "851845471587926086" #vc channel
            #- *vc1
          text_channel_ids:
            - "851845490298454026" #text channel
            #- *text1
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
```
