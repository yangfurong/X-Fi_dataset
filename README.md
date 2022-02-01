# X-Fi_dataset
X-Fi dataset

# Requirement
mysql  Ver 14.14 Distrib 5.7.25, for Linux (x86_64) using  EditLine wrapper

# How to import dataset into MySQL database
1. Merge all .sql files in a subfolder named by city into one .sql file. 
```
cat macao/macao.sql* > macao/macao.sql
```
2. Create a database in MySQL for a .sql file, e.g. paris.sql
```
mysql -u root -p
# Input your passwd
# mysql cli
> create database carfi_paris;
> exi
```

3. Import .sql file into the database
`mysql -u root -p carfi_paris < paris.sql`

# The table structure of each database

1. APTCPInfoFails: this table contains all WiFi association attempts.
```
+----------------------+---------------------------+------+-----+---------+----------------+
| Field                | Type                      | Null | Key | Default | Extra          |
+----------------------+---------------------------+------+-----+---------+----------------+
| id                   | bigint(20)                | NO   | PRI | NULL    | auto_increment |
| interface            | varchar(32)               | YES  |     | NULL    |                | # the network interface name
| avg_speed            | decimal(64,10)            | YES  |     | NULL    |                | # the average driving speed of the assoc.
| dist_km              | decimal(64,10)            | YES  |     | NULL    |                | # the driving of the assoc.
| l2_avg_signal        | decimal(64,10)            | YES  |     | NULL    |                | # the average AP signal level during the assoc.
| l2_stderr_signal     | decimal(64,10)            | YES  |     | NULL    |                | # the standard deviation of the AP signal level during the assoc.
| l2_essid             | varchar(128)              | YES  |     | NULL    |                | # the essid of the AP corresponding to the assoc.
| l2_bssid             | varchar(128)              | YES  |     | NULL    |                | # the bssid ...
| l2_freq              | int(11)                   | YES  |     | NULL    |                | # the channel frequency of the AP ...
| l2_signal_lv         | decimal(64,10)            | YES  |     | NULL    |                | # the intial signal level of the assoc.
| l2_assoc_type        | enum('NEW','REASSOC')     | YES  |     | NULL    |                | # the type of association: new or reassociated
| l2_auth_t_s          | decimal(64,10)            | YES  |     | NULL    |                | # the time of authentication start
| l2_auth_t_e          | decimal(64,10)            | YES  |     | NULL    |                | # the time of authentication end
| l2_assoc_t_s         | decimal(64,10)            | YES  |     | NULL    |                | # the time of association start
| l2_assoc_t_e         | decimal(64,10)            | YES  |     | NULL    |                | # the time of association end
| l2_hs_t_s            | decimal(64,10)            | YES  |     | NULL    |                | # the time of 4WAY handshake start
| l2_hs_t_e            | decimal(64,10)            | YES  |     | NULL    |                | # the time of 4WAY handshake end
| l2_conn_t_s          | decimal(64,10)            | YES  |     | NULL    |                | # the time of L2 connectivity start
| l2_conn_t_e          | decimal(64,10)            | YES  |     | NULL    |                | # the time of L2 connectivity end
| l3_dhcp_t_s          | decimal(64,10)            | YES  |     | NULL    |                | # the time of DHCP start
| l3_dhcp_t_e          | decimal(64,10)            | YES  |     | NULL    |                | # the time of DHCP end
| l3_ip_t_s            | decimal(64,10)            | YES  |     | NULL    |                | # the time of IP connectivity start
| l3_ip_t_e            | decimal(64,10)            | YES  |     | NULL    |                | # the time of IP connectivity end
| l3_ip                | varchar(32)               | YES  |     | NULL    |                | # the IP address of the assoc.
| l3_ip_prefix         | int(11)                   | YES  |     | NULL    |                | # the IP prefix
| l3_ip_gw             | varchar(32)               | YES  |     | NULL    |                | # the IP adress of the gateway
| l3_dhcp_server       | varchar(32)               | YES  |     | NULL    |                | # the IP address of the DHCP server
| l3_dns_servers       | blob                      | YES  |     | NULL    |                | # the IP address of the DNS server
| tcp_t_s              | decimal(64,10)            | YES  |     | NULL    |                | # the time of TCP connectivity start (from TCP application logs)
| tcp_t_e              | decimal(64,10)            | YES  |     | NULL    |                | # the time of TCP connectivity end (from TCP application logs)
| tcp_t_s_pcap         | decimal(64,10)            | YES  |     | NULL    |                | # the time of TCP connectivity start (from pcap file)
| tcp_t_e_pcap         | decimal(64,10)            | YES  |     | NULL    |                | # the time of TCP connectivity end (from pcap file)
| tcp_direction        | enum('UPLOAD','DOWNLOAD') | YES  |     | NULL    |                | # the transmission direction
| tcp_cc               | varchar(32)               | YES  |     | NULL    |                | # the congestion control scheme
| tcp_flow_nb          | int(11)                   | YES  |     | NULL    |                | # the concurrent flow number
| tcp_flows            | blob                      | YES  |     | NULL    |                | # the list of 4-tuples of concurrent flows
| tcp_total_bytes_app  | bigint(20)                | YES  |     | NULL    |                | # the total bytes transferred (from application logs)
| tcp_total_bytes_pcap | bigint(20)                | YES  |     | NULL    |                | # the total bytes transferred (from pcap file)
| tcp_goodput_app      | decimal(64,10)            | YES  |     | NULL    |                | # the average goodput (from application logs)
| tcp_goodput_pcap     | decimal(64,10)            | YES  |     | NULL    |                | # the average goodput (from pcap logs)
| tcp_test_local_id    | int(11)                   | YES  |     | NULL    |                | # 
| tcp_loss_rate        | decimal(64,10)            | YES  |     | NULL    |                | # the loss rate
| tcp_rxmt_pkts        | decimal(64,10)            | YES  |     | NULL    |                | # the number of retransmitted packets
| tcp_total_pkts       | decimal(64,10)            | YES  |     | NULL    |                | # the total number of all packets
+----------------------+---------------------------+------+-----+---------+----------------+
```
2. APTCPInfo: this table has the same structure as APTCPInfoFails, but, it only contains all successful WiFi association attempts.
3. Experiment: this table contains the information of all experiments.
```
+------------+----------------+------+-----+---------+----------------+
| Field      | Type           | Null | Key | Default | Extra          |
+------------+----------------+------+-----+---------+----------------+
| id         | bigint(20)     | NO   | PRI | NULL    | auto_increment |
| start_time | decimal(64,10) | YES  |     | NULL    |                |
| end_time   | decimal(64,10) | YES  |     | NULL    |                |
+------------+----------------+------+-----+---------+----------------+
```
4. GPS: this table contains all GPS coordinates recorded during our experiments. We use time to associate GPS coordiantes with associations and experiments.
```
+-----------+----------------+------+-----+---------+----------------+
| Field     | Type           | Null | Key | Default | Extra          |
+-----------+----------------+------+-----+---------+----------------+
| id        | bigint(20)     | NO   | PRI | NULL    | auto_increment |
| latitude  | decimal(64,10) | YES  |     | NULL    |                |
| longitude | decimal(64,10) | YES  |     | NULL    |                |
| elevation | decimal(64,10) | YES  |     | NULL    |                |
| time      | decimal(64,10) | YES  |     | NULL    |                |
+-----------+----------------+------+-----+---------+----------------+
```
5. Link, ScanAP, CarFiScanAP: these tables are not used.


# The raw data

Link to the raw data: <URL>  

## Description of the raw data

The tarball includes the raw data collected from four cities. In the directory of each city, there are many tarballs named as <city>-<start_time>-<end_time>.tar.gz. In each tarball, the data including association logs, DHCP logs, and TCP performance data are archived.

In each experiment tarball, there are some log files and a directory, e.g. `gps.log  linkmon.log  roamingd.log  tester.data  wpa_supplicant.log`. `gps.log` stores the GPS coordinates during the experiment. `wpa_supplicant.log` stores the WiFi association logs. `roamingd.log` stores the DHCP logs. The `tester.data` directory contains the data of all TCP performance tests. The data of each TCP performance test are stored in the sub-directory named as the number of that TCP test. 
  
In each TCP test sub-directory, there are two key files, `tcp_tester.profile` and `flows.pcap`. The first one includes the information as follows.
  
```
1579131540.566103 (TCP connections start time) 
1579131622.562806 (TCP connections end time)
upload (tranmission direction)
bbr (congestion control scheme)
41689088 (total bytes transferred)
1 (number of concurrent flows)
100.64.250.250 44918 149.248.15.30 5001 (the list of the 4-tuple of all TCP flows)
```

The `flows.pcap` file stores the packet traces of the TCP test.
