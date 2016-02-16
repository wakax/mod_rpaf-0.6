## mod_rpaf - reverse proxy add forward

This module gets values of host and remote address from an reverse proxy,
sets host and remote addresss to httpd.
This module was originally written by Thomas Eibner <thomas@stderr.net>.

The differences from the original module are:
* Feature: Support for partial IP address as '10.1.' for RPAFproxy_ips. The author of this patch is unknown.
* Feature: Recursive ip extraction with RPAFrecursive directive.
* Bugfix: In the case of APR_HAVE_IPV6-enabled build, access control of Order/Allow/Deny does not work correctly.
* Bugfix: A wrong remote_addr is set.
* Support of httpd 1.3 was deleted.

## Compile and Install

```
apxs -i -c -n mod_rpaf-2.0.so mod_rpaf-2.0.c
or simply try:
make; make install
```

## Configuration Directives

```
RPAFenable On
# Enable reverse proxy add forward
RPAFproxy_ips 127.0.0.1 10.0.0.1 172.16. 192.168.
# which ips are forwarding requests to us
RPAFsethostname On
# let rpaf update vhost settings
# allows to have the same hostnames as in the "real"
# configuration for the forwarding Apache
RPAFheader X-Forwarded-For
# Allows you to change which header mod_rpaf looks
# for when trying to find the ip the that is forwarding
# our requests
RPAFrecursive On
# If recursive search is disabled, remote address is replaced by the
# last address in RPAFheader directive. If recursive search is
# enabled, remote address is replaced by the last non-trusted address
# in RPAFheader directive.
```

## Author

* Thomas Eibner <thomas@stderr.net> (The original author)
* Takashi Takizawa <taki@cyber.email.ne.jp>
* Taiki Sugawara <buzz.taiki@gmail.com> (RPAFrecursive)
* Geoffrey McRae <gnif@xbmc.org> (rpaf_looks_like_ip() and the related code were ported from https://github.com/gnif/mod_rpaf )

## License
This software is licensed under the [Apache License](http://www.apache.org/licenses/LICENSE).

## Distribution
Latest version available from https://github.com/ttkzw/mod_rpaf-0.6
