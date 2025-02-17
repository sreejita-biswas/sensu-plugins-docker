## Sensu-Plugins-docker

[![Build Status](https://travis-ci.org/sensu-plugins/sensu-plugins-docker.svg?branch=master)](https://travis-ci.org/sensu-plugins/sensu-plugins-docker)
[![Gem Version](https://badge.fury.io/rb/sensu-plugins-docker.svg)](http://badge.fury.io/rb/sensu-plugins-docker)
[![Code Climate](https://codeclimate.com/github/sensu-plugins/sensu-plugins-docker/badges/gpa.svg)](https://codeclimate.com/github/sensu-plugins/sensu-plugins-docker)
[![Test Coverage](https://codeclimate.com/github/sensu-plugins/sensu-plugins-docker/badges/coverage.svg)](https://codeclimate.com/github/sensu-plugins/sensu-plugins-docker)
[![Dependency Status](https://gemnasium.com/sensu-plugins/sensu-plugins-docker.svg)](https://gemnasium.com/sensu-plugins/sensu-plugins-docker)
[![Sensu Bonsai Asset](https://img.shields.io/badge/Bonsai-Download%20Me-brightgreen.svg?colorB=89C967&logo=sensu)](https://bonsai.sensu.io/assets/sensu-plugins/sensu-plugins-docker)

## Sensu Asset
The Sensu assets packaged from this repository are built against the Sensu Ruby runtime environment. When using these assets as part of a Sensu Go resource (check, mutator or handler), make sure you include the corresponding Sensu Ruby runtime asset in the list of assets needed by the resource. The current ruby-runtime assets can be found [here](https://bonsai.sensu.io/assets/sensu/sensu-ruby-runtime) in the [Bonsai Asset Index](bonsai.sensu.io).

## Functionality
This check supports docker versions >= 1.18. Check docker-engine API for more information  

## Files
 * check-container.rb
 * check-container-logs.rb
 * check-docker-container.rb
 * metrics-docker-container.rb
 * metrics-docker-stats.rb
 * metrics-docker-info.rb

## Usage

### Default docker host
By default, all the checks will try to use a default docker host if a specific docker host is not provided to the check on the command line (-H <docker_host> / --docker-host <docker_host>).

Those paramaters will be tried in this order as default docker host :

    DOCKER_URL environnement variable
    DOCKER_HOST environnement variable
    /var/run/docker.sock file

## Installation

[Installation and Setup](http://sensu-plugins.io/docs/installation_instructions.html)

## Notes
[docker-engine API](https://docs.docker.com/engine/api/v1.29/#section/Versioning)
