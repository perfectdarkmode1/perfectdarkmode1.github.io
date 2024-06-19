---
title: Logging
date: 2023-11-06T06:20:36-07:00
draft: true
---
System Logging

\- log data usually kept in /var

\- service called syslog sends info to system logger

syslog components

syslogd

\- daemon

\- new distros use rsyslogd

\- waits for event messages and filters them

\- send to file, console, or do nothing with it.

/var/log/syslog

\- view logs

syslog

\- manages and sends logs to system logger

\- rsyslog (new version)

\- output found at /var/log/syslog

\- except auth messages

/etc/rsyslog.d

\- files maintained by your system logger

\- denoted by selector on left and action on righjt

action= where to send log information

$ logger -s Hello

manually send a log

General logging

\- important logs found under /var/log

/var/log/messages

\- non critical and non debug messages

bootup logs (dmesg)

auth

cron

daemon

etc

/var/log/syslog

\- everything except auth messages

\- useful to debug errors

Kernel logging

/var/log/dmesg

\- info about kernel ring buffer (logged on boot)

\- hardware drivers, kernel info, bootup status, etc.

\- gets reset on every boot

$ dmesg (view dmesg log)

/var/log/kern.log

\- kernel info

\- system events

\- dmesg output

Authentication logging

/var/log/auth.log

\- useful if you have trouble logging in

\- contains system authorization logs

\- user login and authorization method

Managing log files

logrotate

\- log management

\- has config file to specify how many and what logs to keep

\- how to compress logs to save space etc.

\- run out of cron once per day

\- config file found in /etc/logrotate.d
