#### What is this

This fail2ban setup will allow a website, which you want to be restricted by default, to allow dynamically an IP to access it, for a predefined period of time.

#### Usage:

 - Copy the folders/files into your fail2ban setup
 - Update the log path in `jail.d/nginx-magicurl.conf`
 - Update `website.conf` path in nginx within `action.d/iptables-magicurl.conf`
 - Update the magic GET url within `filter.d/nginx-magicurl.conf` Example in file: `mu=thisismagic`

Within `website.conf` in nginx config you will want to have one or few places where you *deny* access *by default* to the website you want to protect.

Example:
```
allow 127.0.0.1;
deny all;
```

The script will search for `deny all;`, and add the whitelisted IP visiting the magic URL before that line. Upon expiration it will delete the line containing the whitelisted IP.

It also adds an iptables entry with `ACCEPT` rule, but this is only for tracking easily who is allowed, and does not affect the allow logic.
