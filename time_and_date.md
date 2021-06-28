# TIME AND DATE

Allows controlling the displayed time/date formats and timezones

## PERMISSIONS

`can_set_timezone`

## USAGE

**To view timezone**

 `!timezone`

 **To set timezone**

  `!timezone <timezone>`

  To set `<timezone>` You can refer this link https://en.wikipedia.org/wiki/List_of_tz_database_time_zones for list of all the various time zones

**To reset**

`!timezone reset`


#### PLUGIN CODE

```yaml
  time_and_date:
    replaceDefaultOverrides: true #replaces default settings if true
    config:
      timezone: Asia/Karachi
      can_set_timezone: true #set your own timezone via !timezone <timezone>, reset with !timezone reset and view with !timezone
      date_formats:
        date: 'MMM D, YYYY'
        time: 'H:mm'
        pretty_datetime: 'MMM D, YYYY [at] H:mm z'
```
