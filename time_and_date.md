# TIME AND DATE

Allows controlling the displayed time/date formats and timezones

## PERMISSIONS

`can_set_timezone`

## USAGE

Moderators can also set their own timezone with the `!timezone` command.
This affects the output of several commands when ran by that moderator

**To view timezone**

`!timezone`

**To set timezone**

`!timezone <timezone>`

> For example `!timezone Europe/Helsinki`

**To reset**

`!timezone reset`


**TIPS**

**Timezone example:**
```yml
timezone: Europe/Helsinki
```
See <https://en.wikipedia.org/wiki/List_of_tz_database_time_zones> for a list of supported timezones ("TZ database name" column in the table).

**Date format example:**
```yml
date_formats:
  date: "MM/DD/YYYY"
  time: "h:mm A"
  pretty_datetime: "MM/DD/YYYY [at] h:mm A z"
```
See <https://momentjs.com/docs/#/displaying/format/> for a list of values you can use!

#### PLUGIN CODE

```yaml
  time_and_date:
    replaceDefaultOverrides: true #replaces default settings if true
    config:
      timezone: Asia/Karachi
      date_formats:
        date: 'MMM D, YYYY'
        time: 'H:mm'
        pretty_datetime: 'MMM D, YYYY [at] H:mm z'
    overrides:
      - level: '>=50' #level 50 and above
        config:
          can_set_timezone: true
```
