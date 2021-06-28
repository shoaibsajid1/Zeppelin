# SELF GRANTABLE ROLES

## PERMISSIONS

`can_use` allows you to use this plugin and its commands

`can_ignore_cooldown` - Ping dragory and say DEX is asking him to tell what it does so i too can update these cursed docs.

#### PLUGIN CODE

```yaml
  self_grantable_roles:
    replaceDefaultOverrides: true #replaces default settings if true
    config:
      entries:
        basic: #you can have many entries and name them as u like
          roles:
            "851867945760194600": ["test", "tt"] #can have options too!
          can_use: true #can use this entry? since we can have multiple!
          can_ignore_cooldown: false
          max_roles: 1 #maximum no of roles user can pick from the list
      mention_roles: true #mentions the role itself (but no ping)
```
