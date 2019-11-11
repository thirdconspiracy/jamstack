---
layout: post
date: 2019-03-30 07:00
title:  "Bash Scripts"
mood: happy
category: 
- bash
---

## Redirect stdout/stderr

**redirect stdout/stderr**
{% highlight bash linenos %}
a.out 0<input.txt 1>out.txt 2>&1
{% endhighlight %}

* **a.out** is executable
* **input.txt** replaces standard input (0)
* **out.txt** receives the redirected standard output (1) that would have gone to the screen
* **&1** (location of stdout) receives the redirected stderr (2) that would have gone to the screen

**Ignore stdout**
{% highlight bash linenos %}
a.out 1>/dev/null
{% endhighlight %}


**Ignore stderr**
{% highlight bash linenos %}
a.out 2>/dev/null
{% endhighlight %}

## Chaining Commands

{% highlight bash linenos %}
$ true; echo "sup"
sup
$ false; echo "sup"
sup

$ true && echo "sup"
sup
$ false && echo "sup"

$ true || echo "sup"
$ false || echo "sup"
sup
{% endhighlight %}

## Awk a CSV Column

{% highlight bash linenos %}
awk -F "'*,'*" '{print $3}' filename.csv | uniq | wc -l
{% endhighlight %}

## Trim Alias

{% highlight bash linenos %}
alias trim="awk '{\$1=\$1;print}'"
{% endhighlight %}
Usage:
{% highlight bash linenos %}
grep --no-filename 'xsd:restriction' *.xsd | trim | sort | uniq
{% endhighlight %}


## SSH With Expect

{% highlight bash linenos %}
#!/bin/expect -f
set timeout 15
set force_conservative 1
set addr [lindex $argv 0]
set storenum [lindex $argv 1]

spawn ssh my_id@$addr
set session $spawn_id
expect "Password:"
send "my_password\r"
expect -exact "\$ "
send "...
{% endhighlight %}

## FTP With Expect

{% highlight bash linenos %}
    #!/usr/bin/expect -f

    set addr [lindex $argv 0]
    set timeout -1
    spawn ftp $addr
    expect {
    "):" { send "my_username\r" }
    "timed" exit
    }
    expect {
    "d:" { send "my_password\r" }
    "ftp>" { send "\r" }
    }
    expect "ftp>"
    send "bin\r"
    expect "ftp>"
    send "hash\r"
    expect "ftp>"
    send "cd my_directory\r"
    expect "ftp>"
    send "put myfile\r"
    expect "ftp>"
    send "by\r" 
{% endhighlight %}

## Threading Script

{% highlight bash linenos %}
mkdir locations
uudecode $0
chmod 777 filename.exe
for entry in $LIST
do
ip=`echo $entry | awk -F \: '{print $2}'`
loc=`echo $entry | awk -F \: '{print $1}'`
logfile="./locations/$loc.log"
./filename.exe $ip > $logfile &
count=`ps -ef | grep -i exp | wc -l | awk '{print $1}'`
while [ $count -gt 100 ]
do
count=`ps -ef | grep -i exp | wc -l | awk '{print $1}'`
echo "waiting for process to finish"
done
sleep 2
done
exit 0
begin 777 check_stores.exp
###... UUENCODED CODE GOES HERE ...###
###... filename.exe is here ...###
###... in this case ...###
...
end
{% endhighlight %}

* The & after executing allows you to continue without waiting for completion.
* filename.exe executed can be any program type (sh, exp, c, cpp, py, etc) but should be uniq.
* filename.exe doesn't need to be uuencoded into the script but it's useful if execution isn't on your box.

## Default Shell

Set
{% highlight bash linenos %}
chsh -s /bin/bash
{% endhighlight %}
Verify
{% highlight bash linenos %}
ps -p $$
{% endhighlight %}

## Bash Alternative
Using tcsh instead of bash?

**Use vi on command line**

bash
{% highlight bash linenos %}
set -o vi
{% endhighlight %}

tcsh
{% highlight bash linenos %}
bindkey -v
{% endhighlight %}


**Adding an alias**

bash
{% highlight bash linenos %}
alias vi='vim'
{% endhighlight %}
tcsh
{% highlight bash linenos %}
alias vi 'vim'
{% endhighlight %}
