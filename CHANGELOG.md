# Change Log
This project adheres to [Semantic Versioning](http://semver.org/).

This CHANGELOG follows the format listed at [Our CHANGELOG Guidelines ](https://github.com/sensu-plugins/community/blob/master/HOW_WE_CHANGELOG.md).
Which is based on [Keep A Changelog](http://keepachangelog.com/)

## [Unreleased]
### Breaking Changes
- Bump `sensu-plugin` dependency from `~> 2.0` to `~> 4.0` you can read the changelog entries for [4.0](https://github.com/sensu-plugins/sensu-plugin/blob/master/CHANGELOG.md#400---2018-02-17), [3.0](https://github.com/sensu-plugins/sensu-plugin/blob/master/CHANGELOG.md#300---2018-12-04), and [2.0](https://github.com/sensu-plugins/sensu-plugin/blob/master/CHANGELOG.md#v200---2017-03-29)

### Added
- Travis build automation to generate Sensu Asset tarballs that can be used n conjunction with Sensu provided ruby runtime assets and the Bonsai Asset Index
- Require latest sensu-plugin for [Sensu Go support](https://github.com/sensu-plugins/sensu-plugin#sensu-go-enablement)

## [3.2.0] - 2018-11-22
### Fixed
 - metrics-docker-stats.rb: fix #16 -n option causes metrics-docker-stats.rb to fail, in case containers are linked together

## [3.1.1] - 2018-06-29
### Fixed
 - check-container-logs.rb: fix nil.gsub condition on empty log lines

## [3.1.0] - 2018-05-07
### Added
 - intergration test for container check (@antonidabek)
 - check-container.rb: -x (--allow-exited) to avoid raising alerts when container exited without error, useful for task oriented containers monitoring. (@antonidabek)

## [3.0.0] - 2018-02-17
### Breaking Changes
- Default docker host defined by DockerApi Class ( ENV[DOCKER_URL] => ENV[DOCKER_HOST] => /var/run/docker.sock )
- check-container-logs.rb: -N (--container-name) instead of -n for container name. Now a 'CRITICAL' is trigger if a container doesn't exist (previously, a 'OK' was trigger)
- check-docker-container.rb: -H (--docker-host) instead of -h (--host) for docker Host
- check-container.rb: -H (--docker-host) for docker Host instead of -h (--host) for docker host, -N (--container-name) instead of -c (--container) for container name
- metrics-docker-stats.rb: -N (--container-name) instead of -c (--container) for Container name

### Added
- client_helpers.rb: Add a simple DockerApi class. Add parse_json method.
- metrics-docker-container.rb: Friendly names option added
- check-container-logs.rb: Add an option to check logs from stopped containers if all containers are checked. Add an option to don't check stderr logs. Add an option to don't check stdout logs. Add timestamp in logs output. Add the possibility to use -n multiple times to check multiple containers at once.

### Changed
- metrics-docker-stats.rb: Make use of DockerApi class. Default docker_host defined by DockerApi class. Remove docker_api method.
- metrics-docker-info.rb: Make use of DockerApi class. Default docker_host defined by DockerApi class. Remove docker_api method.
- metrics-docker-container.rb: Make use of DockerApi class. Re-enable rubocop for container_metrics method.
- check-container.rb: Make use of DockerApi class.
- check-docker-container.rb: Make use of DockerApi class.
- check-container-logs.rb: Make use of DockerApi class. Check only logs generated with the 8 bits control to prevent to check logs generated in interactive mode. Check the newest logs rows first instead the oldest. Option -n is not required anymore, if -n option is not provided, the check will be applied to all running containers. Changed the messages displayed with ok and critical

### Fixed
- metrics-docker-stats.rb: Remove trailing / in name value.

### Removed
- Remove unnecessary `docker_api` dependency
- check-container-logs.rb: Logs generated in interactive mode are not checked anymore
- metrics-docker-stats.rb: option -p (--protocol) have been removed because new DockerApi don't use it
- metrics-docker-info.rb: option -p (--protocol) have been removed because new DockerApi don't use it

## [2.0.0] - 2017-11-06
### Fixed
- metrics-docker-stats.rb:: Fix gsub on nil docker environment variable (@epierotto)

### Breaking Change
- bumped dependency of `sensu-plugin` to 2.x you can read about it  [here](https://github.com/sensu-plugins/sensu-plugin/blob/master/CHANGELOG.md#v145---2017-03-07) (@majormoses)

## [1.5.0] - 2017-09-09
### Added
- metrics-docker-stats.rb: Include metric with cpu usage percentage calculated based on docker stats (@alcasim)

### Changed
- updated CHANGELOG guidelines location (@majormoses)

## [1.4.0] - 2017-08-08
### Added
- metrics-docker-info.rb: general information metrics from docker (@alcasim)
- metrics-docker-stats.rb: Added to include environment variables values as part of the metric. Added I/O stats option (@alcasim)

### Added
- Ruby 2.4.1 testing

## [1.3.1] - 2017-06-12
### Fixed
- check-container.rb: fixes to work with docker >= 1.17 (@israelriibeiro)

## [1.3.0] - 2017-06-04
### Added
- metrics-docker-stats.rb: Add an option to ouput a portion of the docker
  container name using by splitting on a delimiter of the users choice.

### Fixed
- check-container.rb: Fix support for docker versions >= 1.18. The key-pair [State][Status] was replaced with [State][Running] and also logic was updated (#45)

## [1.2.0] - 2017-02-08
### Added
- check-container.rb: add an option to test image's tag (@obazoud)

## [1.1.5] - 2016-11-26
### Changed
- Loosen `sensu-plugin` dependency to `~> 1.2` (#44)

## [1.1.4] - 2016-11-26
### Changed
- metrics-docker-stats.rb: Fix JSON parse error if there is more than one chunk
  of response data needed to result in valid JSON because of large datasets.
  (#18)

## [1.1.3] - 2016-08-11
### Changed
- dependencies: use net\_http\_unix = 0.2.2

## [1.1.2] - 2016-06-20
### Changed
- dependencies: use sensu-plugin ~> 1.2.0, docker-api = 1.21.0

## [1.1.1] - 2016-06-10
### Fixed
- metrics-docker-stats.rb: Fix error from trying to collect stats with multiple values. Stats that return array values are now excluded. (#29)

### Changed
- improved help messages
- check-container.rb: issue a critical event if container state != running

## [1.1.0] - 2016-06-03
### Added
- check-container-logs.rb: added `-s|--seconds-ago` option to be able to set time interval more precisely

## [1.0.0] - 2016-05-24
Note: this release changes how connections are made to the Docker API and also
changes some options. Review your check commands before deploying this version.

### Added
- Added check-container-logs.rb to check docker logs for matching strings
- Support for Ruby 2.3.0
- metrics-docker-container.rb: add option to override the default path to cgroup.proc

### Removed
- Support for Ruby 1.9.3

### Changed
- check-docker-container.rb: output the number of running containers
- Refactor to connect to the Docker API socket directly instead of using the `docker` or `docker-api` gems
- Update to rubocop 0.40 and cleanup

## [0.0.4] - 2015-08-10
### Changed
- updated dependencies (added missing dependency `sys-proctable`)
- added docker metrics using docker api

## [0.0.3] - 2015-07-14
### Changed
- updated sensu-plugin gem to 1.2.0

## [0.0.2] - 2015-06-02
### Fixed
- added binstubs

### Changed
- removed cruft from /lib

## 0.0.1 - 2015-04-30
### Added
- initial release

[Unreleased]: https://github.com/sensu-plugins/sensu-plugins-docker/compare/3.1.1...HEAD
[3.1.1]: https://github.com/sensu-plugins/sensu-plugins-docker/compare/3.1.0...3.1.1
[3.1.0]: https://github.com/sensu-plugins/sensu-plugins-docker/compare/3.0.0...3.1.0
[3.0.0]: https://github.com/sensu-plugins/sensu-plugins-docker/compare/2.0.0...3.0.0
[2.0.0]: https://github.com/sensu-plugins/sensu-plugins-docker/compare/1.5.0...2.0.0
[1.5.0]: https://github.com/sensu-plugins/sensu-plugins-docker/compare/1.4.0..1.5.0
[1.4.0]: https://github.com/sensu-plugins/sensu-plugins-docker/compare/1.3.1...1.4.0
[1.3.1]: https://github.com/sensu-plugins/sensu-plugins-docker/compare/1.3.0...1.3.1
[1.3.0]: https://github.com/sensu-plugins/sensu-plugins-docker/compare/1.2.0...1.3.0
[1.2.0]: https://github.com/sensu-plugins/sensu-plugins-docker/compare/1.1.5...1.2.0
[1.1.5]: https://github.com/sensu-plugins/sensu-plugins-docker/compare/1.1.4...1.1.5
[1.1.4]: https://github.com/sensu-plugins/sensu-plugins-docker/compare/1.1.3...1.1.4
[1.1.3]: https://github.com/sensu-plugins/sensu-plugins-docker/compare/1.1.2...1.1.3
[1.1.2]: https://github.com/sensu-plugins/sensu-plugins-docker/compare/1.1.1...1.1.2
[1.1.1]: https://github.com/sensu-plugins/sensu-plugins-docker/compare/1.1.0...1.1.1
[1.1.0]: https://github.com/sensu-plugins/sensu-plugins-docker/compare/1.0.0...1.1.0
[1.0.0]: https://github.com/sensu-plugins/sensu-plugins-docker/compare/0.0.4...1.0.0
[0.0.4]: https://github.com/sensu-plugins/sensu-plugins-docker/compare/0.0.3...0.0.4
[0.0.3]: https://github.com/sensu-plugins/sensu-plugins-docker/compare/0.0.2...0.0.3
[0.0.2]: https://github.com/sensu-plugins/sensu-plugins-docker/compare/0.0.1...0.0.2
