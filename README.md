# Hak5-CloudC2-OpenRC

This repo contains the files required to setup Hak5's Cloud C2 as a
daemon on Alpine Linux

## Setup

To set things up, once you download the Cloud C2 zip file from the
Hak5 website, and create the directory `/opt/cloudc2/` on your Alpine
Linux system. Then extract the files and copy `c2_community-linux-32`
(or whichever matches your architecture) to the newly created
`/opt/cloudc2/`.

NOTE: `c2_community-linux-64` will not work on Alpine Linux. It's
dynamically linked to `/lib64/ld-linux-x86-64.so.2`, which doesn't
exist on musl libc machines.

Then copy the files from this repo onto your system, placing the
`init.d/cloudc2` into your system's `/etc/init.d/` directory, and
`conf.d/cloudc2` into your system's `/etc/conf.d/` directory.

You'll then want to open `/etc/conf.d/cloudc2` in your editor of
choice and modify the variables to match your setup.

If you want to set the reverse proxy options, you'll have to add them
to the `C2_OPTS` variable like this:

```
C2_OPTS="-reverseProxy -reverseProxyPort XXX"
```

NOTE: You MUST set `C2_HOSTNAME` for the daemon to launch.

## Starting the daemon

After following the setup, all you have to do to launch CloudC2 in the
background is run

```
rc-service cloudc2 start
```

You can then set it to run at boot.

```
rc-update add cloudc2
```

## Signing up

When registering your CloudC2 instance, you'll need a setup
token. This token gets outputted from `cloudc2` the first time it
runs. This should appear in `/var/log/cloudc2.log` a couple seconds after
the first time it gets launched.
