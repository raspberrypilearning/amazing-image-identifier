## Share

--- collapse ---
---
title: Sharing your work on GitHub
---

COMING SOON — AN INGREDIENT
--- /collapse ---

--- collapse ---
---
title: Sharing your web app in a coding club
---

You can share your Flask web app with other computers on the same Wi-Fi or network. To do this, you will need to find your IP address, which you can do from the command line.


### What is an IP address?
An IP address is a set of numbers that uniquely identify your computer on a network, and can be used to have one computer talk to another. An IP address is four sets of numbers, broken up by dots, like this: `192.168.86.229`.

The whole internet works based on computers using IP addresses to talk to each other — IP actually stands for Internet Protocol. Domain names like raspberrypi.org are just used to look up the right IP address, although they are a lot easier for people to remember!

The IP address you're using here is called your **private IP address**, because it only works inside your local network. The entire network usually shares a single IP address for connecting to other computers over the internet.

### Finding your IP address on Windows

In your command prompt, run this command:

```batch
ipconfig
```

You will get a lot of information back, but just find the line that begins with `IPv4 Address` — the number on that line is what you need.

### Finding your IP address on Mac OS

In your terminal, run this command:

```bash
ipconfig getifaddr en1
```

The response is your IP address.

### Finding your IP address on Linux (including Raspberry Pi)

In your terminal, run this command:

```bash
hostname -I
```

The response is your IP address.

### Sharing your app

Once you have your IP address, all other people on your network need to do is open their web browser and type your IP address followed by `:5000` into the address bar. For example `192.168.86.229:5000` would work for a computer with that IP address.
--- /collapse ---