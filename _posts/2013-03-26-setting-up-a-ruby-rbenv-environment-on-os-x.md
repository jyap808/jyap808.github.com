---
layout: post
title: Setting up a Ruby rbenv environment on OS X
date: 2013-03-26 21:52
post-link:
---

rbenv is the best way to set up a Ruby environment.  It's pretty essential since you can test your stack against different versions of Ruby and gems such as Rails.

... It's pretty much like virtualenv for Python.

I don't always use Ruby but when I do I use rbenv (said in the Dos Equis man voice).

Install rbenv and ruby-build via brew

{% highlight bash %}
brew update
brew install rbenv
brew install ruby-build
{% endhighlight %}

Add rbenv init to your shell to enable shims and autocompletion.

{% highlight bash %}
echo 'eval "$(rbenv init -)"' >> ~/.bash_profile
{% endhighlight %}

Select the version of Ruby to install.  First list all the available versions

{% highlight bash %}
rbenv install -l
{% endhighlight %}

For example, let's install the latest version in the 1.9.3 branch

{% highlight bash %}
export VERSION=1.9.3-p392
{% endhighlight %}

Build and install Ruby without documentation (saves time)

{% highlight bash %}
CONFIGURE_OPTS="--disable-install-doc" rbenv install $VERSION
{% endhighlight %}

Set the global Ruby version

{% highlight bash %}
rbenv global $VERSION
{% endhighlight %}

Disable ri and rdoc documentation for Gems.  Add to ~/.gemrc

{% highlight bash %}
install: --no-rdoc --no-ri
update: --no-rdoc --no-ri
{% endhighlight %}

Or:

{% highlight bash %}
cat << EOT > ~/.gemrc
install: --no-rdoc --no-ri
update: --no-rdoc --no-ri
EOT
{% endhighlight %}

Bonus points.  Install Rails

{% highlight bash %}
gem install rails
{% endhighlight %}


