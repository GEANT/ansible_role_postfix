# CHANGELOG

## [v2.2.0] - 2022-02-15

### Added

- Extra `login` auth mechanism. This makes it possible for nagios to monitor if the credentials are working, since the `check_smtp` plugin [only supports LOGIN](https://doc.dovecot.org/configuration_manual/authentication/authentication_mechanisms/#plaintext-authentication) as auth mechanism.

## [v2.1.0] - 2022-02-08

### Added

- New feature flag `postfix_relay_server_enable`. When enabled it will deploy an SMTP relay server. Most of this was backported from the GÉANT internal ansible code that is used to deploy `relay.geant.org`.

## [v2.0.2] - 2022-01-08

### Changed

- Prepared configuration for ansible-lint v4

## [v2.0.1] - 2020-10-14

### Fixed

- Fix errors like `warning: /etc/aliases, line 2: record is in "key: value" format; is this an alias file?`, caused by incorrect use of `postmap` for alias files.
