# Zabbix Server の停止手順

## service コマンドの実行

>[!CAUTION]
> [FreeBSD](https://www.freebsd.org) での事例を記述しています。
> 

* root 権限にて以下コマンド実行

```bash
# service zabbix_server status
zabbix_server is running as pid 32826.
# service zabbix_server stop
# service zabbix_server status
zabbix_server is not running.
```

* 以下コマンドで、「停止状態」を確認。

```bash
# ps ax | grep zabbix_server
61767  6  S+J  0:00.00 grep zabbix_server
```

* 停止できていない場合は以下の通り：

```bash
# service zabbix_server status
zabbix_server is running as pid 62591.
# ps ax | grep zabbix_server
62591  -  SJ   0:00.04 /usr/local/sbin/zabbix_server -c /usr/local/etc/zabbix7/zabbix_server.conf
62698  -  SJ   0:00.01 zabbix_server: ha manager (zabbix_server)
62883  -  SJ   0:00.01 zabbix_server: service manager #1 [processed 0 events, updated 0 event tags,
62947  -  SJ   0:00.13 zabbix_server: configuration syncer [synced configuration in 0.019088 sec, i
63138  -  SJ   0:00.01 zabbix_server: alert manager #1 [sent 0, failed 0 alerts, idle 5.022586 sec 
63186  -  IJ   0:00.00 zabbix_server: alerter #1 started (zabbix_server)
63300  -  IJ   0:00.00 zabbix_server: alerter #2 started (zabbix_server)
63374  -  IJ   0:00.00 zabbix_server: alerter #3 started (zabbix_server)
63422  -  SJ   0:00.30 zabbix_server: preprocessing manager #1 [queued 43, processed 305 values, id
63532  -  SJ   0:00.01 zabbix_server: lld manager #1 [processed 3 LLD rules, idle 5.478537sec durin
63645  -  SJ   0:00.07 zabbix_server: lld worker #1 [processed 6 LLD rules, idle 13.166843 sec duri
63768  -  SJ   0:00.03 zabbix_server: lld worker #2 [processed 1 LLD rules, idle 7.000536 sec durin
63891  -  IJ   0:00.00 zabbix_server: housekeeper [startup idle for 30 minutes] (zabbix_server)
64043  -  SJ   0:00.00 zabbix_server: timer #1 [updated 0 hosts, suppressed 0 events in 0.000899 se
64167  -  SJ   0:00.00 zabbix_server: http poller #1 [got 0 values in 0.000022 sec, idle 5 sec] (za
64302  -  SJ   0:00.00 zabbix_server: browser poller #1 [got 0 values in 0.000030 sec, idle 5 sec] 
64395  -  SJ   0:00.02 zabbix_server: discovery manager #1 [processing 0 rules, 0 unsaved checks] (
64419  -  SJ   0:00.12 zabbix_server: history syncer #1 [processed 3 values, 3 triggers in 0.036761
64432  -  SJ   0:00.01 zabbix_server: history syncer #2 [processed 0 values, 0 triggers in 0.000022
64506  -  SJ   0:00.01 zabbix_server: history syncer #3 [processed 0 values, 0 triggers in 0.000027
64605  -  SJ   0:00.01 zabbix_server: history syncer #4 [processed 0 values, 0 triggers in 0.000033
64702  -  SJ   0:00.01 zabbix_server: escalator #1 [processed 0 escalations in 0.001577 sec, idle 3
64787  -  SJ   0:00.00 zabbix_server: proxy poller #1 [exchanged data with 0 proxies in 0.000029 se
64864  -  SJ   0:00.00 zabbix_server: self-monitoring [processed data in 0.000032 sec, idle 1 sec] 
64903  -  SJ   0:00.00 zabbix_server: task manager [processed 0 task(s) in 0.000447 sec, idle 5 sec
64996  -  SJ   0:00.02 zabbix_server: poller #1 [got 0 values in 0.000031 sec, idle 5 sec] (zabbix_
65368  -  SJ   0:00.02 zabbix_server: poller #2 [got 0 values in 0.000029 sec, idle 5 sec] (zabbix_
65496  -  SJ   0:00.03 zabbix_server: poller #3 [got 0 values in 0.000056 sec, getting values] (zab
65514  -  SJ   0:00.06 zabbix_server: poller #4 [got 0 values in 0.000027 sec, idle 5 sec] (zabbix_
65537  -  SJ   0:00.03 zabbix_server: poller #5 [got 0 values in 0.000031 sec, idle 5 sec] (zabbix_
65717  -  SJ   0:00.00 zabbix_server: unreachable poller #1 [got 0 values in 0.000031 sec, idle 5 s
65849  -  SJ   0:00.01 zabbix_server: trapper #1 [processed data in 0.000062 sec, waiting for conne
66174  -  SJ   0:00.01 zabbix_server: trapper #2 [processed data in 0.000062 sec, waiting for conne
66193  -  SJ   0:00.01 zabbix_server: trapper #3 [processed data in 0.000057 sec, waiting for conne
66298  -  SJ   0:00.01 zabbix_server: trapper #4 [processed data in 0.000077 sec, waiting for conne
66402  -  SJ   0:00.01 zabbix_server: trapper #5 [processed data in 0.000065 sec, waiting for conne
66501  -  SJ   0:00.01 zabbix_server: icmp pinger #1 [got 3 values in 2.006164 sec, idle 5 sec] (za
66519  -  SJ   0:00.01 zabbix_server: alert syncer [queued 0 alerts(s), flushed 0 result(s) in 0.00
66604  -  SJ   0:00.00 zabbix_server: history poller #1 [got 0 values in 0.000028 sec, idle 5 sec] 
66626  -  SJ   0:00.01 zabbix_server: history poller #2 [got 0 values in 0.000029 sec, idle 5 sec] 
66796  -  SJ   0:00.00 zabbix_server: history poller #3 [got 0 values in 0.000024 sec, idle 5 sec] 
66940  -  SJ   0:00.01 zabbix_server: history poller #4 [got 0 values in 0.000026 sec, idle 5 sec] 
67072  -  SJ   0:00.01 zabbix_server: history poller #5 [got 0 values in 0.000026 sec, idle 5 sec] 
67180  -  SJ   0:00.01 zabbix_server: availability manager #1 [queued 1, processed 0 values, idle 4
67318  -  SJ   0:00.00 zabbix_server: trigger housekeeper [deleted 0 problems records in 0.004277 s
67421  -  SJ   0:00.00 zabbix_server: odbc poller #1 [got 0 values in 0.000025 sec, idle 5 sec] (za
67517  -  SJ   0:00.02 zabbix_server: http agent poller #1 [got 0 values, queued 0 in 5 sec, awaiti
67582  -  SJ   0:00.11 zabbix_server: agent poller #1 [got 34 values, queued 34 in 5 sec, awaiting 
67789  -  SJ   0:00.06 zabbix_server: snmp poller #1 [got 0 values, queued 0 in 5 sec, awaiting 0] 
67859  -  SJ   0:00.00 zabbix_server: configuration syncer worker [synced 0, updated 0 item names i
67971  -  SJ   0:00.01 zabbix_server: internal poller #1 [got 3 values in 0.000114 sec, idle 1 sec]
68270  -  SJ   0:00.01 zabbix_server: proxy group manager #1 started (zabbix_server)
#

```

