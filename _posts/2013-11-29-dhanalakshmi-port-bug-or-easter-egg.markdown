---
layout: post
title: "Dhanalakshmi Port? Bug or Easter Egg?"
date: 2013-11-29T12:00:00+05:30
tags: software
---

Recently when I was writing a PostgreSQL app, I took a look at `lsof`‘s output to look at the number of active database connections and I saw something weird:

```
java       2588 satyanash   59u  IPv6 1217875      0t0  TCP localhost.localdomain:34565->localhost.localdomain:postgresql (ESTABLISHED)
java       2588 satyanash   60u  IPv6 1216931      0t0  TCP localhost.localdomain:34566->localhost.localdomain:postgresql (ESTABLISHED)
java       2588 satyanash   61u  IPv6 1216932      0t0  TCP localhost.localdomain:**dhanalakshmi**->localhost.localdomain:postgresql (ESTABLISHED)
java       2588 satyanash   62u  IPv6 1218025      0t0  TCP localhost.localdomain:34569->localhost.localdomain:postgresql (ESTABLISHED)
java       2588 satyanash   63u  IPv6 1218026      0t0  TCP localhost.localdomain:34570->localhost.localdomain:postgresql (ESTABLISHED)
```

Apparently, somebody has assigned port 34567 or 34568 as **‘dhanalakshmi‘**.

I don’t know if any other ports exist by such weird names. But it’s something worth noting.

**UPDATE**: More digging reveals that port 34567 has been registered by a Dhanalakshmi EDI Service that offers some kind of banking managing software. lol :D
