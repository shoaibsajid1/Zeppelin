# COMPANION CHANNELS

Set up 'companion channels' between text and voice channels. Once set up, any time a user joins one of the specified voice channels, they'll get channel permissions applied to them for the text channels.


`permissions` This number can be calculated using  https://discordapi.com/permissions.html which allows you to set the behaviour of the linked channel (e.g read only channel, visible only on vc join etc.)


**NOTE**

> The companion channels plugin doesn't currently look at member-related information for overrides, so level overrides don't work

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
          permissions: 52224
          enabled: true
```
