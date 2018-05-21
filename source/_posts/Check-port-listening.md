---
title: Check port listening
categories: Linux
abbrlink: 54995
date: 2015-09-23 14:31:29
tags:
    - Linux
---
If you’re troubleshooting a service that you know is running normally the next step is to ensure it’s listening on the correct network port.

The netstat command shows the services listening to ports on a Linux server and the details of any connections currently made to them. The connection details to consider during basic network daemon troubleshooting are the addresses that the daemon is listening on (including the port number), the daemon’s process identifier (PID), and the program name.

You need to run netstat on the server that is running the service. Netstat is not affected by your firewall configuration.

Note: You can also use the isof and ss commands to check ports. Many of the command flags contained in this article are the same when you run the isof and ss commands. However, the output returned when you use these commands might not resemble the output of the netstat tool. For more information about both commands, see the isof and ss command manuals.

Check ports
To list the TCP ports that are being listened on, and the name of each listener’s daemon and its PID, run the following command:

```bash
sudo netstat -plnt
```

The following example shows the output for three common programs that are listening on three different sockets.

```bash
$ sudo netstat -plnt
Active Internet connections (only servers)
Proto Recv-Q Send-Q Local Address               Foreign Address             State       PID/Program name
tcp        0      0 0.0.0.0:3306                0.0.0.0:*                   LISTEN      3686/mysqld
tcp        0      0 :::443                      :::*                        LISTEN      2218/httpd
tcp        0      0 :::80                       :::*                        LISTEN      2218/httpd
tcp        0      0 :::22                       :::*                        LISTEN      1051/sshd
```

Filter the list
If the list of listening daemons is long you can use grep to filter it. For example, to filter out everything except the default web server port, 80, run the following command:

```bash
$ sudo netstat -plnt | grep ':80'
tcp        0      0 :::80                       :::*                        LISTEN      8448/httpd
```


Analyze the results
Common outcomes are as follows:

Nothing is listening on the port. Check the service configuration files, and then restart the service.
The correct service is listening on the correct port. In this case you need to test the service more thoroughly. Skip to the article on testing the listening service for response using netcat.
Something other than the expected service appears to be listening on the port.
Note: A super-server, such as xinetd, might be listening on the port. Check your xinetd configuration to ensure that this behavior is acceptable.

If something else is listening on the port, you can disable the program by running sudo service httpd stop, or change its configuration so that it no longer listens on the port. When netstat shows the port is free, enable the correct service (for example sudo service vsftpd start).

If you make any changes because the incorrect service is listening, run the netstat command again. If netstat doesn’t show the program listening on the correct port, you need to address its configuration before you go any further.

If you make changes at this point, be sure to test your setup; you might have resolved your issue.

If using the netstat did not resolve your port issues, continue to test connections to the service by using the netcat command.