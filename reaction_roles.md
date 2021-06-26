# REACTION ROLES


**REACTION ROLE TIP**
"auto refresh interval" for reaction roles sets how often the reactions are "refreshed", i.e. removed and re-added. This is done because high-volume reactions like reaction roles can become very glitchy after some time if they're not reset.

you can also do this manually with `!reaction_roles refresh MESSAGE_ID`


**PLUGIN CODE**

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
