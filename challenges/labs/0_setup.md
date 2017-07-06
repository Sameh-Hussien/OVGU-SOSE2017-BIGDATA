* Create the group `barca`

```
	$ sudo groupadd barca
```

* Create the group `merengues`

```
	$ sudo groupadd merengues
```
	
* Add User `neymar` with a UID of `2010`

```
	$ sudo useradd -u 2010 neymar
```

* Add User `ronaldo` with a UID of `2016`

```
	$ sudo useradd -u 2016 ronaldo
```
	
* Add user `ronaldo` to group `barca`

```
	$ sudo usermod -g barca ronaldo
```

* Add user `neymar` to group `merengues`

```
	$ sudo usermod -g merengues neymar
```

* List the `/etc/passwd` entries for `neymar` and `ronaldo`

```
$ grep 'ronaldo\|neymar' /etc/passwd

	neymar:x:2010:502::/home/neymar:/bin/bash
	ronaldo:x:2016:501::/home/ronaldo:/bin/bash
```

* List the `/etc/group` entries for `barca` and `merengues`

```
$ grep 'merengues\|barca' /etc/group

	barca:x:501:
	merengues:x:502:
```