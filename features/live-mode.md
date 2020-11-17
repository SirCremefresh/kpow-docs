---
description: Monitor Kafka Resources in Real-Time
---

# Live Mode

Live Mode provides a real-time view of your Kafka Resources.

## Configuration

**Live mode is enabled by default**.

 Configure further with the following environment variables:

* `LIVE_MODE_ENABLED` - \(bool\) Default: true
* `LIVE_MODE_PERIOD_MS` - \(long\) period \(in ms\) that live mode will run for. Default: 60000
* `LIVE_MODE_INTERVAL_MS` - \(long\) the interval \(in ms\) between snapshots. Default: 3500
* `LIVE_MODE_MAX_CONCURRENT_USERS` - \(long\) the maximum number of concurrent sessions. Default 2

## Usage

Enter Live Mode by clicking the 'play' button in the top right hand corner of the kPow UI.

Exit Live Mode by clicking the spinning 'stop' button. 

Live Mode runs for a configurable period of time after which the user is presented with an option to continue or exit back to normal operation.

Live Mode is available in since v48. See the release video for a quick demonstration:

{% embed url="https://www.youtube.com/watch?v=q8l1rR7Vfcg" %}



