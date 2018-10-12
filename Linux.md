
No line-wrapping:
```
less -eS  # -S for --chop-long-lines
cut -c1-80
```

Performance:
```
$ sar
12:30:01 PM     CPU     %user     %nice   %system   %iowait    %steal     %idle
12:40:01 PM     all      4.29      0.00      4.26      3.54      0.00     87.91
12:50:02 PM     all      4.40      0.00     12.53     11.15      0.00     71.92
01:00:02 PM     all      4.41      0.00     26.22     19.03      0.00     50.33
01:10:02 PM     all      4.52      0.00     28.33     15.89      0.00     51.26
01:20:01 PM     all      4.52      0.00     11.58     15.98      0.00     67.92
```

```
$ dstat
----total-cpu-usage---- -dsk/total- -net/total- ---paging-- ---system--
usr sys idl wai hiq siq| read  writ| recv  send|  in   out | int   csw 
  4   3  89   3   0   0|6873k   14M|  11M   28k|   0     0 |6996  4552 
```
