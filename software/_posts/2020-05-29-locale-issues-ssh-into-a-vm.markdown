---
layout: post
title: "Locale issues when SSHing into a VM"
date: 2020-05-29T20:42:53+0530
tags: [software, linux, osx]
categories: [software]
---

I recently had an issue with the `LC_CTYPE` locale variable being set to an invalid value.
I searched the complete machine for where it could be set, but was unable to find the configuration location.
Further investigation led to the revelation that my local OSX machine config was causing the error on the remote host.

The initial error was from a Python3 program that I was trying to get to run on a remote linux host.
The helpful but unexpected error was as follows:

```
RuntimeError: Click will abort further execution because
Python 3 was configured to use ASCII as encoding for the
environment. Consult https://click.palletsprojects.com/python3/
for mitigation steps.

This system supports the C.UTF-8 locale which is recommended.
You might be able to resolve your issue by exporting
the following environment variables:

    export LC_ALL=C.UTF-8
    export LANG=C.UTF-8

Click discovered that you exported a UTF-8 locale but the
locale system could not pick up from it because it does not exist.
The exported locale is 'en_US.UTF-8' but it is not supported
```

The most obvious workaround was to simply follow what the error recommended and perform:
```
export LC_ALL=C.UTF-8
export LANG=C.UTF-8
```

This causes the locale to be set to predictable values, and allows you to get on.
However, I still wanted to understand what was causing the incorrect locale to be configured in the first place.

## Observations

There were a few odd things I noticed in this case.
Once I logged into the box, becoming `root` or any other user fixed this problem.
This was useful information for debugging, later on.

Running `locale` printed along with the output, the following errors:

```
locale: Cannot set LC_CTYPE to default locale: No such file or directory
locale: Cannot set LC_ALL to default locale: No such file or directory
LANG=en_US.UTF-8
LANGUAGE=
LC_CTYPE=UTF-8
LC_NUMERIC="en_US.UTF-8"
LC_TIME="en_US.UTF-8"
LC_COLLATE="en_US.UTF-8"
LC_MONETARY="en_US.UTF-8"
LC_MESSAGES="en_US.UTF-8"
LC_PAPER="en_US.UTF-8"
LC_NAME="en_US.UTF-8"
LC_ADDRESS="en_US.UTF-8"
LC_TELEPHONE="en_US.UTF-8"
LC_MEASUREMENT="en_US.UTF-8"
LC_IDENTIFICATION="en_US.UTF-8"
LC_ALL=
```

Running any `apt-get` command, also printed this error from `perl`:
```
perl: warning: Please check that your locale settings:
	LANGUAGE = (unset),
	LC_ALL = (unset),
	LC_CTYPE = "UTF-8",
	LANG = "en_US.UTF-8"
    are supported and installed on your system.
perl: warning: Falling back to a fallback locale ("en_US.UTF-8").
```

I also noticed in the output of `locale`, that `LC_ALL` was not set.
This meant that the issue had to lie with the remaining `LC_CTYPE`.

As mentioned before, `root` was correctly configured and working fine.
So I decided to compare the environment values for the two users:

```
$ echo $LC_CTYPE
UTF-8
$ locale | grep CTYPE
LC_CTYPE=UTF-8

# echo $LC_CTYPE`

# locale | grep CTYPE
LC_CTYPE="en_US.UTF-8"
```

In the above output, I saw that `LC_CTYPE` was unset for `root` and
was being defaulted to a valid value of `en_US.UTF-8`.
However, for the `ssh` user, it was _set_ to the invalid value `UTF-8`,
which caused `locale` to complain when it was run.

## Root Cause

* This issue was a combination of using OSX, a terminal emulator and SSHing into a remote Linux host.
* Unlike Linux, OSX allows non-locale strings as a valid value for the `LC_CTYPE` and other locale environment variables.
* By default, most terminal emulators including iTerm2 and Terminal.app will set this value to `UTF-8` on startup.
* These variables are then forwarded to the remote host by `ssh` whenever a new connection is established.
* You can verify this by running `locale` on your local and remote machines.
  In my specific case, `LC_CTYPE=UTF-8` was the invalid value and causing the above errors.
* This also explained why changing the user to become `root` or some other user worked,
  as that did not carry-forward the environment and it's associated variables.

## Mitigation

The best solution is to disable forwarding of these variables on the server itself. To do so, you must have access to change the `sshd` config file at `/etc/ssh/sshd_config`.
Change or remove the `AcceptEnv` directive which is set to the below value, by default:
```
# remove/change/comment this line:
AcceptEnv LANG LC_*
```

You will of course, need to reload the `sshd` daemon for the changes to take effect.
This is the ideal solution, as it allows you complete control over what default locales are used by your users and is also isolated from the the behaviour of individual ssh clients.

If for some reason, you're unable to change the setting on the server, you can instead fix this for yourself, on the client side.
The first approach in this case is to configure your terminal emulator to not set the locale values on startup. This should make all these values default to `C` which stands for “computer” and is valid across both OSX and Linux.

For iTerm2, you can uncheck "Set locale variables automatically" by going to "Preferences > Profiles > Terminal > Environment".

![Disabling locale setup on startup - iTerm2](/img/disable-locale-iterm2.png)

For Terminal.app you need to uncheck "Set locale environment variable on startup", by going to "Preferences > Profiles > Advanced > International":

![Disabling locale setup on startup - Terminal.app](/img/disable-locale-terminal-app.png)

If you want do want your terminal to set locale variables, you can instead disable forwarding these in your ssh client configuration.
Change your `/etc/ssh/ssh_config` or `~/.ssh/ssh_config` file to comment out the `SendEnv` option as follows:
```
Host *
    ...
    # Comment/Remove this line.
    SendEnv LANG LC_*
    ...
```

## Afterthoughts

Ideally, you should never ignore warnings/messages related to the locale, unless you know what you're doing.
Often these are indicative of other issues in the system that may not be immediately apparent.

Like most interesting bugs, the cause and effect in this case were so far apart that it took more than a few hops before we got to the root cause.
Usually, when facing an error in a remote machine, one would never suspect one's local machine to be the problem.
I still look at the `LC_CTYPE=UTF-8` environment variable on my machine and wonder at how harmless it appears.
