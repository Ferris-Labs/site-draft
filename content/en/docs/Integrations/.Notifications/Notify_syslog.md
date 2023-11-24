## Syslog Notifications
* **Source**: https://tools.ietf.org/html/rfc5424
* **Icon Support**: No
* **Message Format**: Text
* **Message Limit**: 32768 Characters per message

Syslog is a way for network devices to send event messages to a logging server – usually known as a Syslog server. The Syslog protocol is supported by a wide range of devices and can be used to log different types of events.

### Syntax
Valid syntaxes are as follows:
* `syslog://`
* `syslog://{facility}`
* `syslog://{host}`
* `syslog://{host}:{port}`
* `syslog://{host}/{facility}`
* `syslog://{host}:{port}/{facility}`

One might change the facility from it's default like so:
* `syslog://local5`

One might change the facility on a remote syslog (rsyslog) server from it's default like so:
* `syslog://localhost/local5`

### Parameter Breakdown
| Variable    | Required | Description
| ----------- | -------- | -----------
| host        | No       | Query a remote Syslog server (rsyslog) by optionally specifying the hostname
| port        | No       | The remote port associated with your rsyslog server provided.  By default if this value isn't sent port **514** is used by default.
| facility    | No       | The facility to use, by default it is `user`. Valid options are **kern**, **user**, **mail**, **daemon**, **auth**, **syslog**, **lpr**, **news**, **uucp**, **cron**, **local0**, **local1**, **local2**, **local3**, **local4**, **local5**, **local6**,  and **local7**
| logperror  | No       | Additionally send the log message to _stderr_.  This method is ignored when preforming a remote query.
| logpid     | Yes      | Include PID as part of the log output.
| mode       | No       | This is automatically detected if not specified.  The mode determines if we're using `rsyslog` (Remote SysLog) vs `syslog` (Local).  Hence the mode value can be either `remote` or `local`. The Apprise URL introduces some ambiguity between `syslog://{facility}` vs `syslog://{hostname}`.  This flag allows you to specifically identify what your intentions are if the internal detection is wrong.

### Example
Send a Syslog notification
```bash
# The following sends a syslog notification to the `user` facility
apprise -vv -t "Test Message Title" -b "Test Message Body" \
   syslog://
```

## RSysLog Testing
To test the remote server, the following can be performed:
```bash
# Setup a simple docker file that will run our our rsyslog server for us:
cat << _EOF > dockerfile.syslog
FROM ubuntu
RUN apt update && apt install rsyslog -y
RUN echo '\$ModLoad imudp\n \\
\$UDPServerRun 514\n \\
\$ModLoad imtcp\n \\
\$InputTCPServerRun 514\n \\
\$template RemoteStore, "/var/log/remote/%\$year%-%\$Month%-%\$Day%.log"\n \\
:source, !isequal, "localhost" -?RemoteStore\n \\
:source, isequal, "last" ~ ' > /etc/rsyslog.conf
ENTRYPOINT ["rsyslogd", "-n"]
_EOF

# build it:
docker build -t mysyslog -f dockerfile.syslog .

# Now run it:
docker run  --cap-add SYSLOG --restart always \
  -v $(pwd)/log:/var/log \
  -p 514:514 -p 514:514/udp --name rsyslog mysyslog

# In another terminal window, you can look into a directory
# relative to the location you ran the above command for a directory
# called `log`
You may need to adjust it's permissions, the log file will only get
created after you send an apprise notification.
```