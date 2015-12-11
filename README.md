bgctl
=====

Control for forked processes without save-pid-to-file feature.
Tool used feature of environment inheritance of forked process in linux to watching for it.

Getting started
---------------
To watching for your daemons you need to add it in bgctl file with prefix:
```sh
bgctl -- 
```

### Usage
```sh
bgctl [-m marker] [-p pidfile] [-P prefix] [-k] -- <cmd> [cmd-args]
```

##### Arguments description:
`-P <prefix>`      - prefix used for processes grouping. Default: <empty>
`-m <marker>`      - used to by default it initialized with md5 hash of "<cmd> [cmd-args]".
                     A <marker> initialized with prefix "<prefix>_" if <prefix> isn't empty.
`-p <pidfile>`     - file to save PID of watched process. Default: /tmp/.<marker>.pid
`-k`               - kill the forked process. 
`--`               - tell to bgctl stop parsing arguments.

### Usage examples
Control ssh with -f argument
```sh
bgctl -P SSHTUNNEL   -p /tmp/.overvpn_tunnel.pid -- /usr/bin/ssh -f -N -R 127.0.0.1:10022:10.0.0.5:22 username@192.168.1.1
```

Alternative usage openconnect
```sh
bgctl -P OPENCONNECT      -- openconnect -b --no-cert-check openconnect.mycompany.com 
```

