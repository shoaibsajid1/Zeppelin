# AUTO DELETE

Allows Zeppelin to auto-delete messages from a channel after a delay

**TIP**

- Maximum deletion delay is 5 minutes

- Time can be in **s** (seconds) or **m** (minutes)

#### PLUGIN CODE

```yaml
  auto_delete:
    replaceDefaultOverrides: true #replaces default settings
    overrides:
      - channel: "851537569644675092" #auto_delete channel
      #- channel: *autodelete
        config:
          enabled: true #auto_delete enabled in only 1 channel
          delay: 1s #deletes 1s after posting
      - level: '>=50'
        config:
          enabled: false #lvl 50 and up are exempt from deletion
```
