---
layout: post
date: 2019-10-30 07:00
title:  "Angular w/ Bootstrap from WSL"
mood: happy
category: 
- wsl
- angular
---


<figure class="aligncenter">
        <img class="small" src="/assets/images/posts/angular-bootstrap-750x460.jpg"  width="auto" height="300" />
</figure>
Install Node & Angular
{% highlight shell %}
sudo apt-get update
sudo apt-get upgrade
curl -sL https://deb.nodesource.com/setup_12.x | sudo -E bash -
sudo apt-get install -y nodejs
sudo npm install -g @angular/cli
{% endhighlight %}

Make Project
{% highlight shell %}
mkdir /path/to/working/dir
cd /path/to/working/dir
ng new my-app
cd my-app
npm install --save bootstrap
code .
{% endhighlight %}

Configure VS Code
* Extensions: <code>Angular Essentials</code> by John Papa
* Configure Chrome Launch:  <code>localhost:4200</code>
* Set Terminal Default: <code>WSL</code>
* Open WSL & Run: <code>ng serve</code>
