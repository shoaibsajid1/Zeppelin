# AUTO REACTIONS

Allows setting up automatic reactions to all new messages on a channel

It is managed by `can_manage` permission

## USAGE

**To enable this plugin**

 ``!auto_reactions <channel> <reactions...>``

For example

 ``!auto_reactions 629990160477585428 👍 👎``

**To disable this plugin**

`!auto_reactions disable <channelId>`

For example

`!auto_reactions disable 629990160477585428`

#### DEFAULT PLUGIN

In the default settings only level 100 can run the auto reaction commands, if you would like to use the default settings, just copy paste below, otherwise you the version below it for customization

```yaml
  auto_reactions: {}
  ```

#### PLUGIN CODE

```yaml
  auto_reactions:
    replaceDefaultOverrides: true #replaces default settings
    overrides:
      - level: '>=50'
        config:
          can_manage: true
          #only managable by level 50 and above
```
