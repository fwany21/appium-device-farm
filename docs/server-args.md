---
title: Server Arguments
---

These arguments are set when you launch the Appium server with device-farm plugin.

| Argument                                    | Required | Description                                                                                                                                                                                                                                                     | Default | Options                                                                                                                                                  |
| ------------------------------------------- | -------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------- | -------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `--plugin-device-farm-platform`             | Yes      | Platform to run tests against for parallel execution                                                                                                                                                                                                            | None    | `both`,`ios`,`android`                                                                                                                                   |
| `--plugin-device-farm-ios-device-type`      | No       | Types of ios devices to include                                                                                                                                                                                                                                 | `both`  | `both`,`simulated`,`real`, For example: If you want to run only against iOS simulator then specify --plugin-device-farm-ios-device-type=simulated        |
| `--plugin-device-farm-android-device-type`  | No       | Types of android devices to include                                                                                                                                                                                                                             | `both`  | `both`,`simulated`,`real`, For example: If you want to run only against android emulator then specify --plugin-device-farm-android-device-type=simulated |
| `--plugin-device-farm-skip-chrome-download` | No       | Downloads require chromedriver for web testing                                                                                                                                                                                                                  | `true`  | `false` <br/>Setting to false will download required chromedriver for web testing on chrome                                                              |
| `--plugin-device-farm-hub`                  | No       | HUB IP address and port the node should register                                                                                                                                                                                                                | None    | `hub: "http://hubhost:hubport"`, If you want to run tests distributed across remote and local machine                                                    |
| `--plugin-device-farm-max-sessions`         | No       | Limit how many sessions can be active at a time. This is useful when you need limit sessions based on host machine resource availability.                                                                                                                       | None    | `<number>` e.g. `8`                                                                                                                                      |
| `--plugin-device-farm-derived-data-path`    | No       | DriveDataPath of WDA to speed iOS test run.                                                                                                                                                                                                                     | None    | `{'simulator': 'PathtoDrivedDataPath', 'device': 'PathtoDrivedDataPath'}`                                                                                |
| `--plugin-device-farm-adb-remote`           | No       | ADB Remote host and port as array                                                                                                                                                                                                                               | None    | `["remoteMachine1IP:adbPort", "remoteMachine2IP:adbPort"]`                                                                                               |
| `--plugin-device-farm-proxy-ip`             | No       | For remote execution if the node machine is behing proxy                                                                                                                                                                                                        | None    | `http://remoteMachineProxyIP:proxyPort`, For example: 'https://10.x.x.x:3333'                                                                            |
| `--plugin-device-farm-emulators`            | No       | The name of Android emulator to run the test on. The names of currently installed emulators could be listed using avdmanager list avd command. If the emulator with the given name is not running then it is going to be launched on automated session startup. | None    | `[{"avdName": "device1, launchTimeout: 200000 }]` [Refer to Emulator (Android Virtual Device)]()                                                           |
| `--plugin-device-availability-timeout-ms`   | No        | Hub only. How long to wait for free device before giving up (in milliseconds) | `300000` | e.g.: `300000` ms (5 minutes) |
| `--plugin-device-availability-query-interval-ms`   | No        | Hub only. How often to check for free device (in milliseconds) | `10000`  | e.g.: `10000` ms|
| `--plugin-send-node-devices-to-hub-interval-ms`   | No        | Node only. How often to send list of local device to hub (in milliseconds). This event is an addition to real-time event when device get plugged or unplugged (in milliseconds)| `10000`  | e.g.:  `10000` ms |
| `--plugin-check-stale-devices-interval-ms`   | No        | Hub only. How often to check device staleness (in milliseconds). Node(s) may go down without notice. | `10000`  | e.g.: `10000` ms |
| `--plugin-check-blocked-devices-interval-ms`   | No        | Hub only. How often to check device block status (in milliseconds). Sessions may be terminated without notice. | `10000`  | e.g.: `10000` ms|
| `--plugin-new-command-timeout-sec`   | No        | Hub only. When last received command is older than this value (in seconds), device is considered no longer in session and will be unblocked.  | `60`  | e.g.: `60` seconds |

### Emulator (Android Virtual Device)

| Capability Name | Description                                                                                                                                                                                                                                                                |
| --------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| avdName         | The name of Android emulator to run the test on. The names of currently installed emulators could be listed using `avdmanager list avd` command. If the emulator with the given name is not running then it is going to be launched on automated session startup.          |
| launchTimeout   | Maximum number of milliseconds to wait until Android Emulator is started. `60000` ms by default                                                                                                                                                                            |
| readyTimeout    | Maximum number of milliseconds to wait until Android Emulator is fully booted and is ready for usage. `60000` ms by default                                                                                                                                                |
| args            | Either a string or an array of emulator [command line arguments](https://developer.android.com/studio/run/emulator-commandline). If arguments contain the `-wipe-data` one then the emulator is going to be killed on automated session startup in order to wipe its data. |
| env             | Mapping of emulator [environment variables](https://developer.android.com/studio/command-line/variables).                                                                                                                                                                  |

Above cli arguments can also be set from config.json file Refer [here](https://github.com/AppiumTestDistribution/appium-device-farm/blob/main/sample-config.json)

### Proxy configuration for axios

If you need to set proxy for remote and cloud execution, appium-device-farm will use the proxy provided and pass that to HttpAgent and HttpsAgent.

The proxy object definition will be as per the axios documentation available here - https://axios-http.com/docs/req_config

Example:

```
  proxy: {
    protocol: 'https',
    host: '127.0.0.1',
    port: 9000,
    auth: {
      username: 'mikeymike',
      password: 'rapunz3l'
    }
  },
```
