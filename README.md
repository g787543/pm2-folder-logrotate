
## Description

PM2 module to automatically rotate logs of processes managed by PM2.

## Install

    pm2 install pm2-folder-logrotate

**NOTE:** the command is `pm2 install` NOT `npm install`

## Configure

- `max_size` (Defaults to `10M`): When a file size becomes higher than this value it will be rotated (its possible that the worker checks the file after it actually passes the limit). You can specify the unit at then end: `10G`, `10M`, `10K`
- `retain` (Defaults to `30` file logs): This number is the number of rotated logs to keep at any one time. If you have retain = 7, then you will have at most 7 rotated logs and your current one.
- `compress` (Defaults to `false`): Enable compression via gzip for all rotated logs
- `dateFormat` (Defaults to `YYYY-MM-DD_HH-mm-ss`) : Format of the data used the name the file of log
- `rotateModule` (Defaults to `true`) : Rotate the log of pm2's module like other apps
- `folderModule` (Defaults to `false`) : Save the log to the folder, and the folder name is like `dateFormat`.
- `workerInterval` (Defaults to `30` in secs) : You can control at which interval the worker checks the log size (minimum is `1`)
- `TZ` (Defaults to system time): This is the standard [tz database timezone](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones) used to offset the log file saved. For instance, a value of `Etc/GMT+1`, with an hourly log, will save a file at hour `14` GMT with hour `13` (GMT+1) in the log name.
- `rotateInterval` (Defaults to `0 0 * * *` everyday at midnight): This cron is used to a force rotate when executed.
We are using [node-schedule](https://github.com/node-schedule/node-schedule) to schedule cron, so all valid cron for [node-schedule](https://github.com/node-schedule/node-schedule) is valid cron for this option. Cron style :

```
*    *    *    *    *    *
┬    ┬    ┬    ┬    ┬    ┬
│    │    │    │    │    |
│    │    │    │    │    └ day of week (0 - 7) (0 or 7 is Sun)
│    │    │    │    └───── month (1 - 12)
│    │    │    └────────── day of month (1 - 31)
│    │    └─────────────── hour (0 - 23)
│    └──────────────────── minute (0 - 59)
└───────────────────────── second (0 - 59, OPTIONAL)
```

### How to set these values ?

 After having installed the module you have to type :
`pm2 set pm2-folder-logrotate:<param> <value>`

e.g:
- `pm2 set pm2-folder-logrotate:max_size 1K` (1KB)
- `pm2 set pm2-folder-logrotate:compress true` (compress logs when rotated)
- `pm2 set pm2-folder-logrotate:rotateInterval '*/1 * * * *'` (force rotate every minute)
