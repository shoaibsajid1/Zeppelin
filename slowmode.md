# SLOWMODE

## PERMISSIONS

`can_manage` allows you to use the plugin and its commands

`is_affected` if `true`, you are affected by slowmode

## USAGE

`use_native_slowmode` uses discord built in slowmode instead of Zeppelins own slowmode. Note that maxmium time is `6h` before bot switches the slowmode from native to Zeppelins version

`!slowmode`

`!slowmode -mode <time>` (mode is optional)

`!slowmode -mode <channel> <time>` (mode is optional)

`!slowmode clear -force <channel> <user>` (force is optional)

`!slowmode disable <channel>`

`!slowmodes` - Shows list of places where slowmode is active

#### PLUGIN CODE

```yaml
  slowmode:
    replaceDefaultOverrides: true #replaces default settings if true
    config:
      use_native_slowmode: true #use discord's built in slowmode (till 6h)
      is_affected: true #everyone except those in override are affected
    overrides:
      - level: '>=50'
        config:
          can_manage: true #can set and manage slowmode commands
          is_affected: false #level 50 and up arent affected by slowmode
```
