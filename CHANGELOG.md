# CHANGELOG

## [v2.4.9] - 2026-01-08

### Fixed

- Forward compatibility issues

## [v2.4.8] - 2025-11-19

### Fixed

- Stabilise sorting of values that are space separated lists

## [v2.4.7] - 2025-11-13

### Security

- Fixed permissions test for password related maps file, this resulted in world readable password maps file if those were used

## [v2.4.6] - 2025-10-07

### Added

- Support for Debian 13
- Support for ansible 2.19

### Fixed

- Linting

### Changed

- `.gitignore` ignores more

## [v2.4.5] - 2024-04-17

### Changed

- Use FQCNs in tasks
- Use current version as `compatibility_level`, instead of static `2`

## [v2.4.4] - 2022-11-28

### Removed

- Removed MR 23. There is already a dedicated task

## [v2.4.3] - 2022-11-28

### Added

- `libsasl2-modules` to default packages

## [v2.4.2] - 2022-08-04

### Fixed

- The `restart postfix` handler used the `postfix reload` command, which is sufficient for most configuration changes to take effect. It turns out there are two exceptions, if those parameters change then postfix needs to fully stop and start for them to be effective:
  - [inet_interfaces](https://www.postfix.org/postconf.5.html#inet_interfaces)
  - [inet_protocols](https://www.postfix.org/postconf.5.html#inet_protocols)

  The handler now uses the service module to restart postfix, but because of the way [Debian handles multiple instances](https://salsa.debian.org/postfix-team/postfix-dev/-/blob/debian/bullseye/debian/README.Debian), the service name to use is `postfix@-`:

  > In order to support multiple postfix instances, postfix uses multiple systemd unit files.  The overall postfix unit is for overall operations on all instances and individual unit files are available for each instance named
  > postfix@${INSTANCE_NAME}.  The primary instance is named "-", so it can be directly addressed with systemctl using the name postfix@- (e.g. systemctl status postfix@-).  Wild cards work and so systemctl status postfix* will show the status of all active postfix units.

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
