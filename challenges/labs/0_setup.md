$ sudo groupadd barca

$ sudo groupadd merengues

$ sudo useradd -u 2010 neymar

$ sudo useradd -u 2016 ronaldo

$ sudo usermod -g barca ronaldo

$ sudo usermod -g merengues neymar

$ grep 'ronaldo\|neymar' /etc/passwd

```
neymar:x:2010:502::/home/neymar:/bin/bash
ronaldo:x:2016:501::/home/ronaldo:/bin/bash
```

$ grep 'merengues\|barca' /etc/group

```
barca:x:501:
merengues:x:502:
```