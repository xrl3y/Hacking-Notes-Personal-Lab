
---

Maquina *Linux*


- Puertos

```java
PORT     STATE SERVICE REASON
22/tcp   open  ssh     syn-ack ttl 61
80/tcp   open  http    syn-ack ttl 61
3306/tcp open  mysql   syn-ack ttl 61
```

- Versiones 
- 
```java
PORT     STATE SERVICE VERSION
22/tcp   open  ssh     OpenSSH 7.2p2 Ubuntu 4ubuntu2.10 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   2048 f0:65:b8:42:b7:c3:ba:8e:fe:e4:3c:cd:57:f1:29:2e (RSA)
|   256 42:1e:1b:8f:19:38:99:2e:36:70:cf:0e:b6:31:92:14 (ECDSA)
|_  256 8e:89:43:de:5d:9b:99:66:c4:2a:93:17:f3:0e:e1:f4 (ED25519)
80/tcp   open  http    Apache httpd 2.4.18 ((Ubuntu))
|_http-title: Tryhackme &#8211; Just another WordPress site
|_http-server-header: Apache/2.4.18 (Ubuntu)
|_http-generator: WordPress 5.6.2
3306/tcp open  mysql   MySQL 5.7.33-0ubuntu0.16.04.1
| mysql-info: 
|   Protocol: 10
|   Version: 5.7.33-0ubuntu0.16.04.1
|   Thread ID: 10
|   Capabilities flags: 65535
|   Some Capabilities: SupportsLoadDataLocal, ODBCClient, SupportsTransactions, Support41Auth, SwitchToSSLAfterHandshake, Speaks41ProtocolOld, IgnoreSigpipes, InteractiveClient, Speaks41ProtocolNew, SupportsCompression, LongPassword, FoundRows, IgnoreSpaceBeforeParenthesis, DontAllowDatabaseTableColumn, ConnectWithDatabase, LongColumnFlag, SupportsMultipleStatments, SupportsMultipleResults, SupportsAuthPlugins
|   Status: Autocommit
|   Salt: R\x0201n	4\x08u\x1B\x16\x081k%YF0%B
|_  Auth Plugin Name: mysql_native_password
|_ssl-date: TLS randomness does not represent time
| ssl-cert: Subject: commonName=MySQL_Server_5.7.33_Auto_Generated_Server_Certificate
| Not valid before: 2021-05-26T21:23:31
|_Not valid after:  2031-05-24T21:23:31
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel
```