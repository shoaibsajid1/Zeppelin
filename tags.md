# TAGS


💡 **TAG TIP**


`user_tag_cooldown`is the cooldown per user per tag

`global_tag_cooldown` is the global cooldown (server wide) per tag

`user_cooldown` is the cooldown per user (not tag specific)

`global_cooldown` is the global cooldown (server wide) (not tag specific)



🌡 **TEMPERATURE TAG**

**CtoF** `{if(args.0, if(or(eq(args.0, "0"), not(eq(add(args.0, 1), 1))), concat(add(mul(args.0, div(9, 5)), 32), "**°F**"), ":warning: Temperature must be a number"),":warning: Please provide a temperature to convert")}`

**FtoC** `{if(args.0, if(or(eq(args.0, "0"), not(eq(add(args.0, 1), 1))), concat(mul(sub(args.0, 32), div(5, 9)), "**°C**"), "⚠️ Temperature must be a number"),"⚠️ Please provide a temperature to convert")}`

**HEALTH TAG**

A useful tag for users on your server.

![Health Tag](/assets/health.png)

<details>
  <summary>Click to view code!</summary>

```yaml
tags:
  replaceDefaultOverrides: true #replaces default settings if true
  config:
    prefix: '!'
    categories:
      "mental":
        tags:
          "health":
            embed:
              title: "Mental Health Resources"
              color: 0xFF0000
              footer:
                text: "Remember, You Matter <3, created by DEX#0001"
                icon_url: https://media.discordapp.net/attachments/770256340639416320/854689949193076737/Medical_31-60_974.jpg?width=523&height=523
              #image:
                #url: https://i.pinimg.com/originals/f6/f6/e6/f6f6e629e0bb1ab4ef763c12b5457074.png
              thumbnail:
                url: https://media.discordapp.net/attachments/770256340639416320/854690141279748096/PngItem_4479310.png?width=523&height=523
              fields:
              -  name: "**National Suicide Prevention Hotline (U.S.):**"
                 value: |
                  **Call:** 1-800-273-8255, available 24/7 for emotional support
                  **Text: HOME** to 741741
                  https://suicidepreventionlifeline.org/chat/

                  Outside the U.S: Find a supportive resource on [this Wikipedia list of worldwide crisis hotlines](https://en.wikipedia.org/wiki/List_of_suicide_crisis_lines)
                 inline: false
              -  name: "**More Support**"
                 value: |
                  For Substance Abuse Support, Eating Disorder Support & Child Abuse and Domestic Violence:
                  [Click to go to Discord's Health & Safety Page](https://discord.com/safety/360044103771-Mental-health-on-Discord#h_01EGRGT08QSZ5BNCH2E9HN0NYV)
```
</details>


**TAGS RESOURCES**


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





**PLUGIN CODE**

```yaml
  tags:
    replaceDefaultOverrides: true #replaces default settings if true
    config:
      prefix: '!!'
      #delete_with_command would delete the bot response when the original message is deleted
      delete_with_command: true
      #user_tag_cooldown is the cooldown per user per tag
      user_tag_cooldown: null
      #global_tag_cooldown is the global cooldown (server wide) per tag
      global_tag_cooldown: null
      #user_cooldown is the cooldown per user (not tag specific)
      user_cooldown: null
      #allow tags to ping?, Can be enabled conditionally via overrides for e.g. only moderators
      allow_mentions: false
      #global_cooldown is the global cooldown (server wide) (not tag specific)
      global_cooldown: null
      #When turned on, the message triggering a tag will be automatically deleted after the tag is posted
      auto_delete_command: false
      categories:
        "general":
          tags:
            "id":
              embed:
                description: |-
                  User id: {user.id}
        "support":
          tags:
            "lost":
              embed:
                title: "Hey there, it seems like you're lost!"
                description: |-
                  This server is the support server for the site **[discord.io](https://discord.io/)**.

                  Through us, anyone can create a custom invite link for free. However, when those links expire, people often get confused and stumble here.

                  We are not the server you intended to join. If you can, please let the person who gave you the link know that it has expired. Thank you!

                  Click for translation: [🇹🇷](https://translate.google.com/?sl=en&tl=tr&text=This%20server%20is%20the%20support%20server%20for%20the%20site%20discord.io.%0A%0AThrough%20us%2C%20anyone%20can%20create%20a%20custom%20invite%20link%20for%20free.%20However%2C%20when%20those%20links%20expire%2C%20people%20often%20get%20confused%20and%20stumble%20here.%0A%0AWe%20are%20not%20the%20server%20you%20intended%20to%20join.%20If%20you%20can%2C%20please%20let%20the%20person%20who%20gave%20you%20the%20link%20know%20that%20it%20has%20expired.%20Thank%20you!&op=translate) [🇵🇹](https://translate.google.com/?sl=en&tl=pt&text=This%20server%20is%20the%20support%20server%20for%20the%20site%20discord.io.%0A%0AThrough%20us%2C%20anyone%20can%20create%20a%20custom%20invite%20link%20for%20free.%20However%2C%20when%20those%20links%20expire%2C%20people%20often%20get%20confused%20and%20stumble%20here.%0A%0AWe%20are%20not%20the%20server%20you%20intended%20to%20join.%20If%20you%20can%2C%20please%20let%20the%20person%20who%20gave%20you%20the%20link%20know%20that%20it%20has%20expired.%20Thank%20you!&op=translate) [🇷🇺](https://translate.google.com/?sl=en&tl=ru&text=This%20server%20is%20the%20support%20server%20for%20the%20site%20discord.io.%0A%0AThrough%20us%2C%20anyone%20can%20create%20a%20custom%20invite%20link%20for%20free.%20However%2C%20when%20those%20links%20expire%2C%20people%20often%20get%20confused%20and%20stumble%20here.%0A%0AWe%20are%20not%20the%20server%20you%20intended%20to%20join.%20If%20you%20can%2C%20please%20let%20the%20person%20who%20gave%20you%20the%20link%20know%20that%20it%20has%20expired.%20Thank%20you!&op=translate)
                color: 0xae7aef
        "tips":
          tags:
            "foo":
              embed:
                title: "Reminder"
                description: |-
                  Bar

                color: 0xae7aef
                image:
                  url: https://media.discordapp.net/attachments/799195773408903188/830388041608593438/Screen_Shot_2021-04-10_at_3.25.26_PM.png

            "!reminder":
              embed:
                title: "Reminder"
                #color: 0xae7aef
                image:
                  url: https://media.discordapp.net/attachments/799195773408903188/830389173210972160/Screen_Shot_2021-04-10_at_3.29.45_PM.png

            "!avatar":
              embed:
                title: "Avatar"
                #color: 0xae7aef
                image:
                  url: https://media.discordapp.net/attachments/770256340639416320/830444957654843413/Screen_Shot_2021-04-10_at_7.11.36_PM.png

            "!jumbo":
              embed:
                title: "Jumbo"
                #color: 0xae7aef
                image:
                  url: https://cdn.discordapp.com/attachments/832964085976530964/834393774426816552/Screen_Shot_2021-04-21_at_4.40.37_PM.png

            "!follow":
              embed:
                title: "Follow"
                #color: 0xae7aef
                image:
                  url: https://media.discordapp.net/attachments/770256340639416320/834398760854618122/Screen_Shot_2021-04-21_at_5.02.26_PM.png
            "gg":
                description: |-
                  Bar
    overrides:
      - level: '>=50'
        config:
          #can user use the tags ?
          can_use: true
          #can user create tags?
          can_create: true
          #can user view the tags list
          can_list: true
          #only level 50 and up will a tag ping
          allow_mentions: false
```
