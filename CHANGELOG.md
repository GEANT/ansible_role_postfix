# CHANGELOG

## [v2.4.1] - 2022-05-09

### Fixed

- More thorough check for `smtp_sasl_auth_enable` postfix setting

## [v2.4.0] - 2022-05-04

### Added

- Task to install the SASL package when the configuration requires it.

### Fixed

- The list of Berkeley DB files to generate is now based on the list of source files that have actually changed.
- Output of various tasks is now more correct

## [v2.3.0] - 2022-03-04

### Added

- Feature to allow removing entries from the defaults of `master.cf`. This can be used to disable a postfix service, for instance the standard SMTP service on port 25.

### Changed

- The restart handler was changed to use the native postfix command.

### Removed

- Superfluous spacing in keys. 

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
