# Bouncer
Tool to enforce firewall rules based on web logs.

## Setup
```
git clone https://github.com/paralucid/Bouncer.git

mv Bouncer/bouncer /usr/bin/bouncer

sudo bouncer setup

mv Bouncer/rules.json /etc/bouncer

CRONTAB ENTRY: */1  * * *   root  bouncer enforce
```

## Interface
Bouncer works through modular rules based on attributes within a given request.

Below are examples of attribute rules. If `request` contains `/.env` block the associated IP address, etc.
```
sudo bouncer block request /.env
sudo bouncer block ip 1.2.3.4
```

You can also chain rules together for improved control. For example, the following rulechain will only block the associated IP address if *both* attributes are matched.
I.e. if `request` contains `/wp-admin.php` AND `user_agent` contains `curl` block the associated IP address.
```
bouncer block request /wp-admin.php and user_agent curl
```
You can chain these are far as you like, Bouncer doesn't limit you. But 2-3 attributes should be more than enough to keep the peace.
