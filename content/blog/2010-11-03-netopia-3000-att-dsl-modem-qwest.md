---
title: Netopia 3000 for Qwest DSL
date: 2010-11-03
id: 256
author: Greg Boggs
guid: http://www.gregboggs.com/?p=256
url: "/netopia-3000-att-dsl-modem-qwest/"
categories:
- Blog
tags:
- Networking
---

Want to use your AT&T DSL Netopia Modem on QWest DSL without having to pay the $99 dollars for a new Qwest DSL modem?

The short version:

  1. Click configure -> WAN -> ATM
  2. Change VPI and VCI to 0 and 32 respectively
  3. Encapsulation is set to PPP over Ethernet and Multiplexing is LLC/SNAP
  4. Click submit, then click the little yellow exclaimation in the top right and reboot your modem

### What it took to discover those steps

We've just moved from California to Oregon, and we were shocked to discover that AT&T doesn't provide service to Portland. It took me a couple hours to figure out that Qwest is a phone company that provides DSL to my area. I did some comparision shopping between cable, DSL and various options in Portland and found Qwest slightly cheaper than Comcast.

Qwest charges $99 dollars for a modem while Comcast gives one out for free. I already had a Netopia 3000 DSL modem/router, so Qwest seemed like the smart choice. When my service was turned on, I called Qwest and they gave me my username and password.

I struggled for several hours to get my Netopia 3000 modem to connect to Qwest DSL. I knew Qwest wasn't going to be very helpful configuring my AT&T modem, so I went through every setting my modem had figuring I'd get it eventually.

I didn't.

So, I called back and explained the problem with great patience, &#8220;I'm trying to connect a Netopia 3000 ATT modem to your Qwest DSL service. Can you tell me what settings your DSL uses?&#8221; The service rep couldn't help me, but we spent 25 minutes rebooting my router, listing my operating system, and talking about my wireless Ubuntu loving laptop. At the end of the call she put me on hold for a few minutes before telling me that she can't help me because I have an AT&T modem and they are only trained in Qwest modems. I got a list of Qwest supported hardware from her figuring I'd have to purchase one.

She then gave me my account user name and password (again) and told me that Qwest uses PPOE (I think she meant PPPOE), with a customer VPI VCI of 0/32. Later that day after some careful searching for Netopia Qwest DSL, I found the answer. Change VCI from 35 that AT&T uses to 32 which Qwest uses.

I got out of paying the $99 dollar idiot fine. But, Qwest made it damn hard to do.

On the phone with AT&T to cancel service now and I've already been transfered twice in 5 minutes&#8230; Wow, that's never happened before. Amazing customer service, very friendly, service canceled and AT&T is cutting down my bill $35 dollars.
