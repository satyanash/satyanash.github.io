---
layout: post
title: "Thunderbird Mail Merge addon Quirks"
date: 2017-01-18T19:28:56+05:30
tag: software
---

Just decided to put this out there and save an hour for anybody trying to figure out why the Mail Merge addon won't work for them.

I recently had to send about two thousand customized emails from a CSV. 
I could've written a script, but who's going to maintain that? :P

Enter [Mail Merge](https://addons.mozilla.org/en-us/thunderbird/addon/mail-merge/), an add-on for Thunderbird by Alexander Bergmann.
It's a very simple to use mail merge UI that just works and comes with a few nicely configurable options.
It worked fine the first time I tried it, and then I promptly forgot about it.

Later when I had a thousand more emails to send out, it simply wouldn't work.
I would type out the template, click on **`File -> Mail Merge`**. Fill in all my options just like I did the last time and click on **OK**.
The progress bar would appear and disappear in a glimpse and the generated emails were nowhere to be found in my outbox or drafts folder.
I double checked the encoding for my input CSV files and made sure the encoding setting matched the actual encoding of the file.
It still refused to generate the emails.
There were also no errors in the Thunderbird *Error Console* ( `Ctrl + Shift + J`).
It kept telling me that everything was fine.

After about 45 minutes of searching, cursing and trying various input combinations, I found the problem.

Compare the following email templates:

### won't work
{% raw %}
~~~
To: {{ EMAIL }}
Subject: Hi {{ NICK_NAME }}, what's up?

Hello {{ FIRST_NAME }},

How was your {{ HOLIDAY }}?

My Diwali was awesome. Expecting a reply.

Your friend,
satyanash
~~~
{% endraw %}

### works
{% raw %}
~~~
To: {{EMAIL}}
Subject: Hi {{NICK_NAME}}, what's up?

Hello {{FIRST_NAME}},

How was your {{HOLIDAY}}?

My Diwali was awesome. Expecting a reply.

Your friend,
satyanash
~~~
{% endraw %}

Can you tell the difference?
Neither could I. Being a programmer you're used to ignoring any extra whitespace.
You might even pepper in extra spaces just to improve readability.
Any decent parser will treat `a = 30` and `a=30` equally.
That doesn't seem to be the case for whatever parsing code is used by this add-on.

Turns out that the extra whitespace before and after the CSV column name in the double braces cause the problem.
{% raw %}`{{EMAIL}}` is the correct way to refer to your `'EMAIL'` column in the CSV.{% endraw %}

I really hope this blog saves time for atleast one other person on this planet.
