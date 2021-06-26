# Tips & Tricks

## Override Tip

Overrides are always calculated top down

For example:
If you want to have mods messages not be deleted, your overrides would need to be in this order:

1. Enable in channel xyz
2. Disable for mods
If you have it the other way round it'll delete everything, even from mods.
```yml
    overrides:

    - role: "766285827612999752" #disable rule once role is given
      config:
        rules:
          autorole:
            enabled: false

    - level: '>=50'
      config:
        can_view_antiraid: true
        can_set_antiraid: true
        rules:
          badwords:
            enabled: false
          copypasta:
            enabled: false
```
