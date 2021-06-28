# LOCATE USER

## PERMISSIONS

`can_where` (see below)

`!where / !w` - Posts an instant invite to the voice channel that member is in
Usage: `!w 108552944961454080` where `108552944961454080` is the member ID

`can_alert` (see below)

`!follow / !f` - Sets up an alert that notifies you any time `<member>` switches or joins voice channels
Usage: `!f @DEX#0001 -d 9999h reminder message`

**HOW TO GET ALERTED WHEN SOMEONE JOINS VC USING FOLLOW COMMAND**

`!f @DEX#5006 -d 9999h reminder message` everytime user joins/leaves vc, zep will ping u

`!fs` shows a list of all your alerts you set up
example output:

`1.` Target: @banana

`2.` Target: @pear

`!fs d 1` deletes the first alert from the list

![Follow User](https://media.discordapp.net/attachments/770256340639416320/834398760854618122/Screen_Shot_2021-04-21_at_5.02.26_PM.png)

#### PLUGIN CODE

```yaml
  locate_user:
    replaceDefaultOverrides: true #replaces default settings if true
    config:
      can_where: true
      can_alert: true
```
