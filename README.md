# Lighthouse Custom Configuration

Requirements:

- node > 18
- lighthouse cli `npm install -g lighthouse`

Run lighthouse test for Mobile:

`bash performance google_store`

Run lighthouse test for Desktop:

`bash performance google_store desktop`

## Simulated Slowdown

Tweak the slowdown in `config/config.cfg`.
Pagespeed uses a simulated slowdown of 4x for mobile tests, and no slowdown for desktop.

The approximate hardware difference between the pagespeed and a M3 Pro processor is near 10x so by adjusting the config to:

```
# Adds 10 to slowdown
mobile_slowdown=14
desktop_slowdown=10
```

The lighthouse scores become similar to Pagespeed

## Blocking Assets

We can block assets by adding them to the `blocked_patterns` list in `config/config.cfg`.

For example we can block trackingware by adding:

```
blocked_patterns+=(
    "googletagmanager"
    "doubleclick.net"
)
```

## Pagespeed Default Settings

### Mobile

```
{
    "onlyCategories": [
        "performance"
    ],
    "channel": "lr",
    "formFactor": "mobile",
    "locale": "en-US",
    "screenEmulation": {
        "deviceScaleFactor": 1.75,
        "height": 823,
        "mobile": true,
        "width": 412
    },
    "throttling": {
        "downloadThroughputKbps": 1474.5600000000002,
        "requestLatencyMs": 562.5,
        "rttMs": 150,
        "throughputKbps": 1638.4,
        "uploadThroughputKbps": 675,
        "cpuSlowdownMultiplier": 4
    },
    "throttlingMethod": "simulate"
}
```

### Desktop

```
{
    "extends": "lighthouse:default",
    "settings": {
        "onlyCategories": [
            "performance"
        ],
        "channel": "lr",
        "formFactor": "desktop",
        "locale": "en-US",
        "screenEmulation": {
            "deviceScaleFactor": 1,
            "height": 940,
            "width": 1350,
            "mobile": false
        },
        "throttling": {
            "rttMs": 40,
            "throughputKbps": 10240,
            "cpuSlowdownMultiplier": 1
        },
        "throttlingMethod": "simulate"
    }
}
```
