# systemd input plugin for [Fluentd](http://github.com/fluent/fluentd)

[![Build Status](https://travis-ci.org/reevoo/fluent-plugin-systemd.svg?branch=master)](https://travis-ci.org/reevoo/fluent-plugin-systemd) [![Code Climate GPA](https://codeclimate.com/github/reevoo/fluent-plugin-systemd/badges/gpa.svg)](https://codeclimate.com/github/reevoo/fluent-plugin-systemd) [![Gem Version](https://badge.fury.io/rb/fluent-plugin-systemd.svg)](https://rubygems.org/gems/fluent-plugin-systemd)

# Requirements <a name="requirements"></a>


|fluent-plugin-systemd|fluentd|ruby|
|----|----|----|
| 0.1.x | >= 0.14.11, < 2 | >= 2.1 |
| 0.0.x | ~> 0.12.0 | >= 1.9  |

## WARNING
this is the maintenance branch for the **0.0.x** series that supports fluentd
v0.12.x we plan to backport commits from master at least until td-agent is
based on fluentd v0.14

please install the [0.1.x release](https://github.com/reevoo/fluent-plugin-systemd)
if you are using fluentd v0.14 for the latest and greatest features

## Overview

**systemd** input plugin reads logs from the systemd journal

## Installation

Simply use RubyGems:

    gem install fluent-plugin-systemd -v 0.0.11

    or

    td-agent-gem install fluent-plugin-systemd -v 0.0.11

## Configuration

    <source>
      @type systemd
      path /var/log/journal
      filters [{ "_SYSTEMD_UNIT": "kube-proxy.service" }]
      pos_file kube-proxy.pos
      tag kube-proxy
      read_from_head true
    </source>

**path**

Path to the systemd journal, defaults to `/var/log/journal`

**filters**

Array of filters, see [here](http://www.rubydoc.info/gems/systemd-journal/Systemd%2FJournal%2FFilterable%3Afilter) for further
documentation, defaults to no filtering.

**pos file**

Path to pos file, stores the journald cursor. File is created if does not exist.

**read_from_head**

If true reads all available journal from head, otherwise starts reading from tail,
 ignored if pos file exists (and is valid). Defaults to false.

**strip_underscores**

If true strips underscores from the beginning of systemd field names.
May be useful if outputting to kibana, as underscore prefixed fields are unindexed there.

**tag**

_Required_ A tag that will be added to events generated by this input.

## Example

For an example of a full working setup including the plugin, [take a look at](https://github.com/assemblyline/fluentd)

## Dependencies

This plugin depends on libsystemd

## Running the tests

To run the tests with docker on several distros simply run `rake`

For systems with systemd installed you can run the tests against your installed libsystemd with `rake test`

## Licence etc

[MIT](LICENCE)

Issues and pull requests welcome

## Contributors

Many thanks to our brilliant contributors

* [jescarri](https://github.com/jescarri)
* [mikekap](https://github.com/mikekap)
