ungoogled-chromium updater
==========================
Updater for the Ungoogled Chromium binaries of the portable linux version:
https://github.com/clickot/ungoogled-chromium-binaries

It is useful only for the binaries of the portable version of linux, the script can be included with the binaries or run in a separate directory.

## In all cases

The first time you run "updater", it will download the latest version from the repository, regardless of the version you have installed.

It is recommended to make a backup.

## Get started

Create an empty directory to host ungoogled-chromium, e.g. /opt/ungoogled-chromium

Copy "updater" and "chrome-wrapper-updater" files in /opt/ungoogled-chromium

Run: /opt/ungoogled-chromium/updater

The latest version will be downloaded, if you want to periodically check for new versions instead of running /opt/ungoogled-chromium/chrome or /opt/ungoogled-chromium/chrome-wrapper run /opt/ungoogled-chromium/chrome-wrapper-updater

## Existing installation

If you already have Ungoogled Chromium installed in any directory, simply copy scripts "updater" and "chrome-wrapper-updater" to the root directory of your installation, e.g. /opt/ungoogled-chromium

To automatically check periodically for updates, instead of running /opt/ungoogled-chromium/chrome or /opt/ungoogled-chromium/chrome-wrapper run /opt/ungoogled-chromium/chrome-wrapper-updater

## Separate directory

You can have your installation in one directory, e.g. /opt/ungoogled-chromium and the updater in another, e.g. /opt/ungoogled-chromium-updater

In this case you can update manually as follows:

    /opt/ungoogled-chromium-updater/updater -i /opt/ungoogled-chromium

You can create a CRON task with the above command, in this case you may want to add the -f option to force the new update check, default is 2 days, and -s does not show confirmation dialogs.

    /opt/ungoogled-chromium-updater/updater -i /opt/ungoogled-chromium -f true -s true

If you want automatic updates when launching the browser, you will have to modify the "chrome-wrapper-updater" script as follows:

```bash
#!/bin/bash

CURRENT_DIR=$(dirname $0)

# check updates in background
${CURRENT_DIR}/updater >> ${CURRENT_DIR}/updater.log &

# exec ungoogled-chromium
# Commented because it is for the case of the same directory.
# ${CURRENT_DIR}/chrome-wrapper "$@"

# exec ungoogled-chromium
# Include the installation path
/opt/ungoogled-chromium/chrome-wrapper "$@"
```

## Command line options

The following options are available on the command line:

```console

updater [-i /path/to/ungoogled-chromium] [-f <true|false>] [-e <number>] [-s <true|false>] [-t /path/to/tmp]

    -l  ungoogled-chromium installation directory (default current dir)
    -f  Force new version check if true (default false)
    -e  Check for updates every N days (default 2)
    -t  Temporary directory (default "${CURRENT_DIR}/tmp")
    -s  Quiet update, does not show confirmation dialogs (default false)

```

## License

MIT License
