---
title: "Maven - Settings"
tags: [maven]
group: build
---

# Prerequisites

To build eXo projects you need to install a Java [JDK](http://www.oracle.com/technetwork/java/javase/downloads/index.html) 6 or 7 depending of the Platform version you are targetting :

* Platform 4.1+ : Java 7
* Platform 4.0.x : Java 6 / Java 7

# Install Apache Maven

The version **3.2.3** of [Apache Maven](http://maven.apache.org/download.cgi) is currently recommended to build eXo projects. _The minimal version required is 3.0.4. The version 3.2.2 must be avoided due to [MNG-5663](https://jira.codehaus.org/browse/MNG-5663)._

1. Download a fresh and clean copy of [Apache Maven](http://maven.apache.org/download.cgi). It is critical to take a fresh copy to be sure that the file `apache-maven-X.Y.Z/conf/settings.xml` isn't modified !!
2. Unzip the distribution archive, i.e. apache-maven-X.Y.Z-bin.(zip|tar.gz) to the directory you wish to install Maven. The subdirectory `apache-maven-X.Y.Z` will be created from the archive. It is recommended to not store it under a path with spaces.
3. Add the path of `apache-maven-X.Y.Z/bin` in your `PATH` environment variable.
    * On Windows use the preferences screen of "Environment Variables"
    * On Linux/MacOS export the variable PATH from a startup script like .bash_profile (it depends of the OS and the shell you are using)
4. Add a system environment variable `MAVEN_OPTS` (it could be in a .profile startup script on Linux/MacOS operating systems or in the global environment variables panel on Windows)with the value `-Xshare:auto -Xms128M -Xmx1G -XX:MaxPermSize=256M`
5. Run `mvn --version` to verify that it is correctly installed.

<div class="panel panel-info">
  <div class="panel-heading">
    <h3 class="panel-title"><i class="fa fa-info-circle"></i> Additional documentations</h3>
  </div>
  <div class="panel-body">
    <ul>
      <li><a href="http://www.sonatype.com/books/mvnref-book/reference/installation.html">Maven: The Complete Reference - Chapter 2. Installing Maven</a></li>
      <li><a href="http://maven.apache.org/download.html">Maven website - Installing Maven</a></li>
    </ul>
  </div>
</div>

<div class="panel panel-danger">
  <div class="panel-heading">
    <h3 class="panel-title"><i class="fa fa-minus-circle"></i> Maven and MacOSX</h3>
  </div>
  <div class="panel-body">
    <p>Apple provides for several years now, Maven as a standard tool in MacOSX distributions. You can see the version provided with <tt>mvn --version</tt>. You can find where the <tt>mvn</tt> script is located with <tt>which mvn</tt> (in theory in <tt>/usr/bin</tt>). It recommended to deactivate the one provided with MacOS X to use the one you'll define yourself. Take care if you upgrade your system, because Apple can restore the default version on your system. To deactivate the Maven version bundled in OSX, just remove the symlink : <tt>sudo rm /usr/bin/mvn</tt></p>
  </div>
</div>

# Configure Apache Maven

## Basic setup

Since Platform 4, no specific settings are required to build eXo public projects. Just clone any project and launch `mvn install`

<div class="alert alert-warning">
  <i class="fa fa-exclamation-triangle"></i> <strong>Warning!</strong> If you are behind a repository manager that avoids you to use repositories declared in our projects you'll have to add a proxy to our <a href="https://repository.exoplatform.org/public">public repository</a>.
</div>

<a name="Advanced"></a>
## Advanced setup

If you need to release a project or to build a project relying on private or staging binaries you'll need to customize your maven settings.

<div class="panel panel-warning">
  <div class="panel-heading">
    <h3 class="panel-title"><i class="fa fa-exclamation-triangle"></i> Home Directory</h3>
  </div>
  <div class="panel-body">
    <p>In Unix (and OSX), your home directory will be referred to using a tilde (i.e. <tt><sub>~/bin</sub></tt> refers to <tt>/home/USER/bin</tt>). In Windows, we will also be using ~ to refer to your home directory. In Windows XP, your home directory is <tt>C:\Documents and Settings\USER</tt>, and in Windows Vista, your home directory is <tt>C:\Users\USER</tt>. From this point forward, you should translate paths such as <tt>~/.m2</tt> to your operating system's equivalent.</p>
  </div>
</div>

Using [our template](/resources/build/maven/settings.xml) create a file `settings.xml` in your `home directory` under a directory called `.m2` (if you already launched maven this directory must already exist and it should contain a subdirectory `repository` where Maven stores all artifacts it processes).

{% gist exo-swf/a05132085d70c7541acb settings.xml %}

In the `~/.m2/settings.xml` configuration file you have to fill your credentials to access to protected binaries or to publish artifacts on repository.exoplatform.org. For a better security, you can encrypt passwords in your settings file, however you must first configure a master password. For more information on both server passwords and the master password, see the [Guide to password encryption](http://maven.apache.org/guides/mini/guide-encryption.html) and the dedicated chapter in the [Maven Reference Guide](http://www.sonatype.com/books/mvnref-book/reference/appendix-settings-sect-encrypting-passwords.html). To release a project you have also to define the GPG key to use and its passphase (see [the GPG setup guide](#GPG)).

When your setup is done you can activate the following profiles :

  * `-Pexo-release` : Automatically activated while releasing projects. This profile is also activated on our CI server. Your GPG key must be configured (see [the GPG setup guide](#GPG)).
  * `-Pexo-private` : To access to private binaries on repository.exoplatform.org (eXo employees only).
  * `-Pexo-staging` : To access to staging binaries (releases in validation) on repository.exoplatform.org (eXo employees only). **TAKE CARE TO ACTIVATE IT ONLY IF REQUIRED.** These repositories are delivering binaries considered by maven as released but allowed to be replaced. Maven never updates released binaries thus you have to cleanup your local repository to grab an updated version.
  * `-Pexo-cp` : To access to custom projects binaries on repository.exoplatform.org (eXo employees only).
  * `-Pjboss-staging` : To access to staging binaries on repository.jboss.org. **TAKE CARE TO ACTIVATE IT ONLY IF REQUIRED.** These repositories are delivering binaries considered by maven as released but allowed to be replaced. Maven never updates released binaries thus you have to cleanup your local repository to grab an updated version.

<a name="GPG"></a>
## Maven and GPG

### Install gnupg for your OS.

#### MacOS

For [homebrew](http://brew.sh/) users :

{% highlight sh %}
brew install gnupg
{% endhighlight %}

For [macport](https://www.macports.org/) users :

{% highlight sh %}
sudo port install gnupg
{% endhighlight %}

Others, you can use the [native package](http://macgpg.sourceforge.net/).

#### Ubuntu

{% highlight sh %}
sudo aptitude install gnupg
{% endhighlight %}

#### Windows
TBD

### Validate your installation

{% highlight sh %}
$ gpg --version
gpg (GnuPG) 1.4.10
Copyright (C) 2008 Free Software Foundation, Inc.
License GPLv3+: GNU GPL version 3 or later <http://gnu.org/licenses/gpl.html>
This is free software: you are free to change and redistribute it.
There is NO WARRANTY, to the extent permitted by law.

Home: ~/.gnupg
Supported algorithms:
Pubkey: RSA, RSA-E, RSA-S, ELG-E, DSA
Cipher: 3DES, CAST5, BLOWFISH, AES, AES192, AES256, TWOFISH, CAMELLIA128, 
        CAMELLIA192, CAMELLIA256
Hash: MD5, SHA1, RIPEMD160, SHA256, SHA384, SHA512, SHA224
Compression: Uncompressed, ZIP, ZLIB, BZIP2
{% endhighlight %}

### Generate your private GPG Key

#### Configure GPG

Enforce the level of encryption. Edit `~/.gnupg/gpg.conf`

{% highlight sh %}
$ vi .gnupg/gpg.conf
{% endhighlight %}

At the end of the file add :

{% highlight sh %}
personal-digest-preferences SHA512
cert-digest-algo SHA512
default-preference-list SHA512 SHA384 SHA256 SHA224 AES256 AES192 AES CAST5 ZLIB BZIP2 ZIP Uncompressed
{% endhighlight %}

#### Generate the key

Launch the key generation 

{% highlight sh %}
$ gpg --gen-key
{% endhighlight %}

**ALWAYS SELECT DEFAULT CHOICES AND DON'T USE AN EMPTY PASSPHRASE**

Enter your personal information like here :

  * Real Name : Arnaud Héritier
  * Comment : eXo Platform CODE SIGNING KEY
  * Email Address : arnaud.heritier@exoplatform.com

Your key is created.

You can list the key you just generated with :

{% highlight sh %}
$ gpg --list-key
/Users/arnaud/.gnupg/pubring.gpg
--------------------------------
pub   4096R/2CF0CC82 2009-11-17
uid                  Arnaud Héritier (eXo Platform CODE SIGNING KEY) <arnaud.heritier@exoplatform.com>
sub   4096R/37540EAE 2009-11-17
{% endhighlight %}

You send your key to a PGP server (you use the ID from the "pub" line)

{% highlight sh %}
gpg --keyserver hkp://pgp.mit.edu --send-keys 2CF0CC82
{% endhighlight %}

Your GPG key is now ready to be used

### Configure your GPG Key for Maven

Fill the GPG keyname and passphrase in the exo-release profile of your maven settings like described in [Advanced settings](#Advanced)

{% highlight sh %}
    <profile>
      <id>exo-release</id>
      <properties>
        <gpg.keyname>2CF0CC82</gpg.keyname><!-- This is the public ID is displayed with the gpg list-key command described above -->
        <gpg.passphrase>My awesome passphrase</gpg.passphrase>
      </properties>
    </profile>
{% endhighlight %}

### Test it

Clone this project : `git@github.com:exodev/maven-sandbox-project.git`

Launch the command : `mvn install -Pexo-release`

You should see .asc files installed along others artifacts in the `target` directory of the project

To end tests, try to release this project : `mvn release:prepare` followed by `mvn release:perform`.

**You are ready. Your environment is setup to do a release with GPG signature.**

Don't forget to logon into [https://repository.exoplatform.org](https://repository.exoplatform.org) and drop your staging repository

### More info
  * [http://www.sonatype.com/people/2010/01/how-to-generate-pgp-signatures-with-maven/](http://www.sonatype.com/people/2010/01/how-to-generate-pgp-signatures-with-maven/)
  * [http://www.apache.org/dev/release-signing.html](http://www.apache.org/dev/release-signing.html)
  * [http://www.apache.org/dev/publishing-maven-artifacts.html#gpg](http://www.apache.org/dev/publishing-maven-artifacts.html#gpg)
  * [http://maven.apache.org/plugins/maven-gpg-plugin](http://maven.apache.org/plugins/maven-gpg-plugin)