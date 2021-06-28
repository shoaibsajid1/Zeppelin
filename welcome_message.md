# WELCOME MESSAGE


**WELCOME PLUGIN VARIABLES**


`member`, `user`, and `guild`

Usage:

welcome `{user.username}` to `{guild.name}!`

welcome `<@{user.id}>!`

![welcome message](assets/welcome.png)

#### PLUGIN CODE

```yaml
  welcome_message:
    replaceDefaultOverrides: true #replaces default settings if true
    config:
      send_dm: true
      send_to_channel: "851851771717353512" #welcome channel
      #send_to_channel: *welcome
      message: |-
              **WELCOME TO DEX's DASHBOARD**

              Invite others with
              https://discord.gg/JCZf3sHYpE
```
