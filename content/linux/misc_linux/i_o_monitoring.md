---
title: IO Monitoring
date: 2023-11-06T06:20:36-07:00
draft: true
---
$ iostat

\- cpu and disk usage

cpu info section

%user:utilization at user level

%nice: user level w/ nice priority & cpu utilization with nice priorities

%system: system level (kernel)

%iowait: time(s) cpu was idle when system had outstandingdisk i/o request

%steal: involuntary wait time by cpu while hypervisor was servicing another virtual processor

%idle: cpu idle time w/ no outstanding disk i/o request

Disk utilization section (2nd part)

tps: transfers per second issued to device

transfers= i/o request to device

\- indeterminate size

\- multiple logical requests combined into a single i/o request

kB_read/s: amount of data read from device

kB_wrtn/s: amount of data written to device

kB_read: total # read

kB_wrtn: total # written

Memory monitoring

$ vmstat

\- monitor memory

Feilds

Procs

r: # of processes for run time

b: # of processes in uninterruptible sleep

Memory

swpd: how much virtual memory used

free: how much free memory

buff: how much buffer memory

cache: how much cache memory

Swap

si: amount of memory swapped in from disk

so: amount of memory swapped out to disk

io

bi: blocks received in from block device

bo: blocks sent out to block device

system

in: interrupts per second

cs: context switches per second

CPU (time spent)

us: user time

sy: kernel; time

id: idle

wa: waiting for io

Continuous Monitoring

\- collect, report, and save system activity information

Installing sar

\- used for historical analysis

$ sudo apt install sysstat

Setting up data collection

if sar doesn't automatically start collecting data

\- modify the ENABLED field in

/etc/default/sysstat

\- then restart the service

$ etc/init.d/sysstat restart

Using sar

$ sudo sar -q

\- lists details from start of the day

$ sudo sar -r

\- list memory usage details from start of day

$ sar -q /var/log/sysstat/sa02 (day)

\- view certain day

cron jobs

\- used to schedule tasks (run programs)

30 08 *** /home/pete/scripts/change_wallpaper

(minute hour day month day of week)

$ crontab -e

\- create a cron job by editing crontab file
