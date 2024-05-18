# Lighthouse Custom Configuration

Requirements:

- node > 18

#### Instructions:

- [npm install -g lighthouse]([https://github.com/GoogleChrome/lighthouse](https://github.com/GoogleChrome/lighthouse?tab=readme-ov-file#using-the-node-cli)
- Copy `example_project.cfg` configuration file in `./config`, rename and change settings

## Run lighthouse test for Mobile:

`bash performance example_project`
or
`npm run performance example_project`

## Run lighthouse test for Desktop:

`bash performance example_project desktop`
or
`npm run performance example_project desktop`

## Simulated Slowdown

Tweak slowdown factor in `config/{project}.cfg`.
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
