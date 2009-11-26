---
layout: post
title: Yasnippet example for ssh hosts configuration
tags: [yasnippets, emacs, ssh]
---
I manage or help managing a lot of unix servers around the net, they all have one thing in common: _they use **ssh**_, but several different _hostnames_, _IP address_ and _usernames_. Sometimes I have two or three usernames for a single box, for example: personal username, deploy and root.

To avoid having to remember all those different configurations I do a heavy use of the `~/.ssh/config` file, to define host aliases. Here are some examples:

{% highlight bash %}

# Defined in ~/.ssh/config
Host example
    Hostname   example.com
    User       root

Host example-deploy
    Hostname      example.com
    User          deploy
    FordwardAgent yes

Host example-admin-console
    Hostname      192.168.100.230
    User          admin
    Port          2330

{% endhighlight %}

Then I can type in console:

{% highlight sh %}
$ ssh example
$ ssh example-deploy
$ ssh example-admin-console
{% endhighlight %}

Here is a simple yasnippet to add new host aliases in `~/.ssh/config` file when using emacs.

{% highlight bash %}
  # -*- mode: snippet -*-
  # contributor: Jorge Calás Lozano <calas@railsdog.com>
  # name: ssh-host
  # key: host
  # group: ssh
  # expand-env: ((yas/indent-line 'fixed) (yas/wrap-around-region 'nil))
  # --
  Host ${1:short-name}
       Hostname           ${2:hostname}
       User               ${3:username}
       ForwardAgent       ${4:$$(yas/choose-value '("yes" "no"))}
       ${5:Port               ${6:22}}
  ${7:host}$0
{% endhighlight %}

This is very small set of the options you can set. If you want to see what else you can configure in you ssh config file go ahead and type `man ssh-config` in your console.
