# REACTION ROLES

Allows you to add reaction roles to a given message.

## PERMISSIONS

`can_manage` is needed to use this plugin and its commands


## USAGE

**ADDING REACTION ROLES**

To add reaction roles, use the format below!

If the message you specify is not found, use `!save_messages_to_db <channelId> <messageId>`
to manually add it to the stored messages database permanently and try again!

```yaml
!reaction_roles messageid
emoji1 = roleid1
emoji2 = roleid2
```

Example
```yaml
!reaction_roles 800865377520582687
👍 = 556110793058287637
👎 = 558037973581430785
```


**CLEAR**

`!reaction_roles clear MESSAGEID` to clear reaction roles. Incase this does not work, save to database and try again! *see below*

STEPS:

1. `!save_messages_to_db 534722948246929429-858626287895314472`

2. `!reaction_roles clear 858626287895314472`


**REACTION ROLE TIP**

`auto_refresh_interval` for reaction roles sets how often the reactions are "refreshed", i.e. removed and re-added. This is done because high-volume reactions like reaction roles can become very glitchy after some time if they're not reset. To fix this, you can refresh them!

**REFRESH**

`!reaction_roles refresh MESSAGEID` to refresh reaction roles. Incase this does not work, save to database and try again! *see below*

STEPS:

1. `!save_messages_to_db 534722948246929429-858626287895314472`

2. `!reaction_roles refresh 858626287895314472`

#### PLUGIN CODE

```yaml
  reaction_roles:
    replaceDefaultOverrides: true #replaces default settings if true
    config:
      auto_refresh_interval: 900000 #re-adds reactions after x seconds
      remove_user_reactions: true #remove user reaction or let it stay
    overrides:
      - level: '>=100'
        config:
          can_manage: true #only level 100 can manage
```
