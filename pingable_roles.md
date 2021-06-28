#PINGABLE ROLES

## PERMISSIONS

`can_manage` allows you to use this plugin and its commands

#### PLUGIN CODE

```yaml
  pingable_roles: #makes a role pingable when you start typing in a specific channel
    replaceDefaultOverrides: true #replaces default settings if true
    overrides:
      - level: '>=100'
        config:
          #Usage: !pingable_role <channelId> <role>
          #To disable: !pingable_role disable <channelId> <role>
          can_manage: true #only level 100 can run that ^
```
