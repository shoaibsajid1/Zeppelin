# POST

## PERMISSIONS

`can_post`is what allows users to use this plugin and its commands

## COMMANDS

`!edit <message> <content>`


`!edit_embed <message> -title "Title Here" -color #FFFFFF <maincontent>`

`!post <channel> <content>` where optional flags include `-enable-mentions` `-schedule` `-repeat` `-repeat-until` and `-repeat-times`

... something something THIS IS INCOMPLETE OK LET ME LIVE

📮 **SCHEDULED POSTS**

scheduled posts are messages that are scheduled to be posted later, using the `-schedule` option for `!post`,

 e.g. `!post -schedule="2021-02-01 12:00" Some message that is posted on Feb 1 at 12pm`

#### PLUGIN CODE

```yaml
  post:
    replaceDefaultOverrides: true #replaces default settings if true
    overrides:
      - level: '>=100'
        config:
          can_post: true #only level 100 can post (use this plugin)
```
