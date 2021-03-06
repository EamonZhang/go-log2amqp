go-log2amqp
===========

A simple daemon that reads a file (tail -f style)
and sends every line to an AMQP exchange.

Uses https://github.com/ActiveState/tail and https://github.com/streadway/amqp

Intended for nginx and apache access logs -- so it does some special character
encoding/escaping for that format (because `\xXX` is not valid JSON).

```
Usage of ./go-log2amqp:
  -uri="amqp://user:password@broker.example.com:5672/vhost": AMQP URI
  -exchange="logtest": Durable AMQP exchange name
  -exchange-type="fanout": Exchange type - direct|fanout|topic|x-custom
  -key="nginxlog": AMQP routing key
  -file="/var/log/syslog": filename to watch
  -n=false: Quit after file is read, do not wait for more data, do not read/write state
  -v=false: Verbose output
```

Package example
---------------

The `ubuntu` directory contains an example how to package this tool:
`build.sh` will fetch all sources, compile them, and use
[fpm](https://github.com/jordansissel/fpm) to build a Debian package
containing the binary, the configuration, and the upstart config.

Config examples
---------------

The `example` directory contains configuration snippets for Apache, nginx, and varnishncsa.
