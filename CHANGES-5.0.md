# 5.0.3

## Bug fixes

* Websocket listener failed to read headers `X-Forwared-For` and `X-Forwarded-Port` [8415](https://github.com/emqx/emqx/pull/8415)

# 5.0.2

Announcemnet: EMQX team has decided to stop supporting relup for opensouce edition.
Going forward, it will be an enterprise only feature.

Main reason: relup requires carefully crafted upgrade instructions from ALL previous versions.

For example, 4.3 is now at 4.3.16, we have `4.3.0->4.3.16`, `4.3.1->4.3.16`, ... 16 such upgrade paths in total to maintain.
This had been the biggest obstacle for EMQX team to act agile enought in deliverying enhancements and fixes.

## Enhancements

## Bug fixes

* Fixed a typo in `bin/emqx` which affects MacOs release when trying to enable Erlang distribution over TLS [8398](https://github.com/emqx/emqx/pull/8398)
* Ristricted shell was accidentally disabled in 5.0.1, it has been added back. [8396]{https://github.com/emqx/emqx/pull/8396)

# 5.0.1

5.0.1 is built on [Erlang/OTP 24.2.1-1](https://github.com/emqx/otp/tree/OTP-24.2.1-1). Same as 5.0.0.

5.0.0 (like 4.4.x) had Erlang/OTP version number in the package name.
This is because we wanted to release different flavor packages (on different Elixir/Erlang/OTP platforms).

However the long package names also causes confusion, as users may not know which to choose if there were more than
one presented at the same time.

Going forward, (starting from 5.0.1), packages will be released in both default (short) and flavored (long) package names.

For example: `emqx-5.0.1-otp24.2.1-1-ubuntu20.04-amd64.tar.gz`,
but only the default one is presented to the users: `emqx-5.0.1-ubuntu20.04-amd64.tar.gz`.

In case anyone wants to try a different flavor package, it can be downlowded from the public s3 bucket,
for example:
https://s3.us-west-2.amazonaws.com/packages.emqx/emqx-ce/v5.0.1/emqx-5.0.1-otp24.2.1-1-ubuntu20.04-arm64.tar.gz

Exceptions:

* Windows package is always presented with short name (currently on Erlang/OTP 24.2.1).
* Elixir package name is flavored with both Elixir and Erlang/OTP version numbers,
  for example: `emqx-5.0.1-elixir1.13.4-otp24.2.1-1-ubuntu20.04-amd64.tar.gz`

## Enhancements

* Removed management API auth for prometheus scraping endpoint /api/v5/prometheus/stats [8299](https://github.com/emqx/emqx/pull/8299)
* Added more TCP options for exhook (gRPC) connections. [8317](https://github.com/emqx/emqx/pull/8317)
* HTTP Servers used for authentication and authorization will now indicate the result via the response body. [8374](https://github.com/emqx/emqx/pull/8374) [8377](https://github.com/emqx/emqx/pull/8377)
* Bulk subscribe/unsubscribe APIs [8356](https://github.com/emqx/emqx/pull/8356)
* Added exclusive subscription [8315](https://github.com/emqx/emqx/pull/8315)
* Provide authentication counter metrics [8352](https://github.com/emqx/emqx/pull/8352) [8375](https://github.com/emqx/emqx/pull/8375)
* Do not allow admin user self-deletion [8286](https://github.com/emqx/emqx/pull/8286)
* After restart, ensure to copy `cluster-override.conf` from the clustered node which has the greatest `tnxid`. [8333](https://github.com/emqx/emqx/pull/8333)

## Bug fixes

* A bug fix ported from 4.x: allow deleting subscriptions from `client.subscribe` hookpoint callback result. [8304](https://github.com/emqx/emqx/pull/8304) [8347](https://github.com/emqx/emqx/pull/8377)
* Fixed Erlang distribution over TLS [8309](https://github.com/emqx/emqx/pull/8309)
* Made possible to override authentication configs from environment variables [8323](https://github.com/emqx/emqx/pull/8309)
* Made authentication passwords in Mnesia database backward compatible to 4.x, so we can support data migration better. [8351](https://github.com/emqx/emqx/pull/8351)
* Fix plugins upload for rpm/deb installations [8379](https://github.com/emqx/emqx/pull/8379)
* Sync data/authz/acl.conf and data/certs from clustered nodes after a new node joins the cluster [8369](https://github.com/emqx/emqx/pull/8369)
* Ensure auto-retry of failed resources [8371](https://github.com/emqx/emqx/pull/8371)
* Fix the issue that the count of `packets.connack.auth_error` is inaccurate when the client uses a protocol version below MQTT v5.0 to access [8178](https://github.com/emqx/emqx/pull/8178)

## Others

* Rate limiter interface is hidden so far, it's subject to a UX redesign.
* QUIC library upgraded to 0.0.14.
* Now the default packages will be released withot otp version number in the package name.
* Renamed config exmpale file name in `etc` dir.
