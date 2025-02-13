<!--startmeta
custom_edit_url: "https://github.com/netdata/netdata/edit/master/src/collectors/python.d.plugin/litespeed/README.md"
meta_yaml: "https://github.com/netdata/netdata/edit/master/src/collectors/python.d.plugin/litespeed/metadata.yaml"
sidebar_label: "Litespeed"
learn_status: "Published"
learn_rel_path: "Collecting Metrics/Web Servers and Web Proxies"
most_popular: False
message: "DO NOT EDIT THIS FILE DIRECTLY, IT IS GENERATED BY THE COLLECTOR'S metadata.yaml FILE"
endmeta-->

# Litespeed


<img src="https://netdata.cloud/img/litespeed.svg" width="150"/>


Plugin: python.d.plugin
Module: litespeed

<img src="https://img.shields.io/badge/maintained%20by-Netdata-%2300ab44" />

## Overview

Examine Litespeed metrics for insights into web server operations. Analyze request rates, response times, and error rates for efficient web service delivery.

The collector uses the statistics under /tmp/lshttpd to gather the metrics.

This collector is supported on all platforms.

This collector only supports collecting metrics from a single instance of this integration.


### Default Behavior

#### Auto-Detection

If no configuration is present, the collector will attempt to read files under /tmp/lshttpd/.

#### Limits

The default configuration for this integration does not impose any limits on data collection.

#### Performance Impact

The default configuration for this integration is not expected to impose a significant performance impact on the system.


## Metrics

Metrics grouped by *scope*.

The scope defines the instance that the metric belongs to. An instance is uniquely identified by a set of labels.



### Per Litespeed instance

These metrics refer to the entire monitored application.

This scope has no labels.

Metrics:

| Metric | Dimensions | Unit |
|:------|:----------|:----|
| litespeed.net_throughput | in, out | kilobits/s |
| litespeed.net_throughput | in, out | kilobits/s |
| litespeed.connections | free, used | conns |
| litespeed.connections | free, used | conns |
| litespeed.requests | requests | requests/s |
| litespeed.requests_processing | processing | requests |
| litespeed.cache | hits | hits/s |
| litespeed.cache | hits | hits/s |
| litespeed.static | hits | hits/s |



## Alerts

There are no alerts configured by default for this integration.


## Setup

### Prerequisites

No action required.

### Configuration

#### File

The configuration file name for this integration is `python.d/litespeed.conf`.


You can edit the configuration file using the `edit-config` script from the
Netdata [config directory](https://github.com/netdata/netdata/blob/master/docs/netdata-agent/configuration.md#the-netdata-config-directory).

```bash
cd /etc/netdata 2>/dev/null || cd /opt/netdata/etc/netdata
sudo ./edit-config python.d/litespeed.conf
```
#### Options

There are 2 sections:

* Global variables
* One or more JOBS that can define multiple different instances to monitor.

The following options can be defined globally: priority, penalty, autodetection_retry, update_every, but can also be defined per JOB to override the global values.

Additionally, the following collapsed table contains all the options that can be configured inside a JOB definition.

Every configuration JOB starts with a `job_name` value which will appear in the dashboard, unless a `name` parameter is specified.


<details><summary>Config options</summary>

| Name | Description | Default | Required |
|:----|:-----------|:-------|:--------:|
| update_every | Sets the default data collection frequency. | 5 | no |
| priority | Controls the order of charts at the netdata dashboard. | 60000 | no |
| autodetection_retry | Sets the job re-check interval in seconds. | 0 | no |
| penalty | Indicates whether to apply penalty to update_every in case of failures. | yes | no |
| name | Job name. This value will overwrite the `job_name` value. JOBS with the same name are mutually exclusive. Only one of them will be allowed running at any time. This allows autodetection to try several alternatives and pick the one that works. |  | no |
| path | Use a different path than the default, where the lightspeed stats files reside. | /tmp/lshttpd/ | no |

</details>

#### Examples

##### Set the path to statistics

Change the path for the litespeed stats files

```yaml
localhost:
 name: 'local'
 path: '/tmp/lshttpd'

```


## Troubleshooting

### Debug Mode

To troubleshoot issues with the `litespeed` collector, run the `python.d.plugin` with the debug option enabled. The output
should give you clues as to why the collector isn't working.

- Navigate to the `plugins.d` directory, usually at `/usr/libexec/netdata/plugins.d/`. If that's not the case on
  your system, open `netdata.conf` and look for the `plugins` setting under `[directories]`.

  ```bash
  cd /usr/libexec/netdata/plugins.d/
  ```

- Switch to the `netdata` user.

  ```bash
  sudo -u netdata -s
  ```

- Run the `python.d.plugin` to debug the collector:

  ```bash
  ./python.d.plugin litespeed debug trace
  ```


