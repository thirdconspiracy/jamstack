---
layout: post
date: 2019-03-16 08:34
title: "Installation"
category: 
- docs
- help
tags:
- installation
- jekyll
---

<figure class="aligncenter">
    <img src="https://snipcartweb-10f3.kxcdn.com/media/all/9570/snipcart-static-site-ecommerce-jekyll.png" />
</figure>

I assume you have already downloaded and installed Ruby. Here's what you need to do next:

1. Run <code>gem install jekyll bundler</code>.
2. Copy the theme in your desired folder.
3. Enter into the folder by executing <code>cd name-of-the-folder</code>.
4. Run <code>bundle install</code>.
5. If you want to access and customize the theme, use <code>bundle exec jekyll serve</code>. This way it will be accessible on <code>http://localhost:4000</code>.
6. Upload the content of the compiled <code>_site</code> folder on your host server.

If something goes wrong, it's likely you're missing a package or on a wrong version.  This may help.
{% highlight shell %}
sudo apt-get update
sudo apt-get autoremove
sudo apt-get autoclean
sudo apt-get upgrade
sudo apt-get install ruby-full build-essential zlib1g-dev
echo '# Install Ruby Gems to ~/gems' >> ~/.bashrc
echo 'export GEM_HOME="$HOME/gems"' >> ~/.bashrc
echo 'export PATH="$HOME/gems/bin:$PATH"' >> ~/.bashrc
source ~/.bashrc
sudo gem install jekyll bundler
sudo bundle install
sudo gem update --system
bundle exec jekyll serve
{% endhighlight %}
