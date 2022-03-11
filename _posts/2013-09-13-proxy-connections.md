---
layout: post
title: Proxy Connections
categories: writing
---

Ever try to reach a dev environment from somewhere off campus (home) and been denied?  Better yet, ever worry about browsing online on an unsecure connection?  You can resolve both by setting up a proxy connection!

The idea behind using a proxy is simple: you ask another computer to help send and receive your traffic for you.  You can SSH to the other computer, usually a server, to ensure your traffic is private and protected.  This guide will show you how to create a tunnel that lets you use a local port to feed traffic to a server like `irc.housing.berkeley.edu`.  It only takes two steps!

## Step 1: Opening the Port

You are free to choose any port you like, as long as it's not being used by other services.  I will use 9002 for this guide.  You will need to keep the terminal open for as long as you're using the proxy.

### Unix and OS X

Hooray for built-in terminals!  Fire up the terminal of your choice and enter in a command like so:

    ssh -D 9002 efung@irc.housing.berkeley.edu

You will be prompted to authenticate, so do that. Essentially, you now just made `localhost:9002` a dynamic (hence `-D`) connection to `irc.housing.berkeley.edu`.  Dynamic connections are mostly used for accessing internet content. Other services, such as remote desktop, are a little trickier and may require manual mapping of local ports to remote ports.

### Windows: PuTTY

I'm sure you're relatively familiar with how to SSH with PuTTY already, so now you just need to add the 'dynamic connection' option.  Under `Connection-> SSH -> Tunnels`, type in the port number at "Source port" and select "Dynamic," then click add.  Now connect to your server as usual.

## Step 2: Make Your Browser Use the Proxy

Now to make your browser utilize the connection you just set up.  Firefox + Foxyproxy plugin works wonders in this step.  The important thing to note here is that you want a *SOCKS proxy*, not HTTP proxy, and it has to point at `localhost` and the port you opened above. Opera fails here. Either way, jump down to your browser for specific instructions and a screenshot.

### Internet Explorer/Google Chrome

IE and Chrome both use Windows' `Control Panel -> Internet Options` for proxies.

### Safari (OS X)

In OS X, you set the proxy for your entire networking device, whether it be Ethernet or the Airport.

### Firefox (without plugins)

Firefox comes with a very basic proxy manager by default.

### Firefox with FoxyProxy (HIGHLY RECOMMENDED)

The problem with all of the above methods is that the configurations are all-or-none. Either you use the proxy for all web traffic or your turn off proxy settings. FoxyProxy, however, gives you the ability to apply proxy settings only to particular websites by adding URL *patterns*. For example, you can add the pattern `*dev-www*.rescomp*` to use the proxy *only* for pages that have `dev-www*.rescomp` somewhere in the URL. Creating the patterns with wildcards is relatively intuitive, but remember to specify the address for the SOCKS proxy.

A note: if you're planning to use your !FoxyProxy settings across Firefox profiles, make sure you check "I am using Portable Firefox" in the "Global Settings" tab so that the settings file (`foxyproxy.xml`) will be located using a relative path.

# References

   * [Proxy Connections with PuTTY](http://www.webhostingtalk.com/showthread.php?t=539067)
