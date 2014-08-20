---
layout: page
title: "Maven - Settings"
tags: [maven]
group: build
---
{% include JB/setup %}

# Prerequisites

To build eXo projects you need to install

* [Apache Maven](http://maven.apache.org) 3.0.4+
* [JDK](http://www.oracle.com/technetwork/java/javase/downloads/index.html) 6+

# Install and configure Maven

You need to add a system environment variable `MAVEN_OPTS` (it could be in a .profile startup script on Linux/MacOS operating systems or in the global environment variables panel on Windows).

* Windows:

{% highlight sh %}
set MAVEN_OPTS=-Xshare:auto -Xms128M -Xmx1G -XX:MaxPermSize=256M
{% endhighlight %}

* Linux/MacOS:

{% highlight sh %}
export MAVEN_OPTS="-Xshare:auto -Xms128M -Xmx1G -XX:MaxPermSize=256M"
{% endhighlight %}

Since Platform 4, to build eXo projects no specific Maven settings are required.

If you are using a repository manager you'll have to reference in it our [public repository](http://repository.exoplatform.org/public) to retrieve our dependencies required to build.
