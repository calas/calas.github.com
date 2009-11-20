---
layout: post
title: Using yasnippets in markdown mode.
tags: [yasnippets, elisp, markdown]
---
I've found that when using markdown-mode yasnippets's `TAB` completion doesn't work. It's just because `TAB` key is bind to `markdown-cycle` function. To change this behaviour I use the [following snippet](http://snipplr.com/view/7970/test/) in my `.emacs` file:

{% highlight cl %}
;; This goes into my .emacs file
(defun markdown-unset-tab ()
  "markdown-mode-hook"
  (define-key markdown-mode-map (kbd "<tab>") nil))
(add-hook 'markdown-mode-hook '(lambda() (markdown-unset-tab)))
{% endhighlight %}

Now I can expand yasnippets using `TAB` inside markdown-mode.
