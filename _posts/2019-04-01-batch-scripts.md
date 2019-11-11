---
layout: post
date: 2019-04-01 07:00
title:  "Batch Scripts"
mood: happy
category: 
- batch
---

<figure class="aligncenter">
        <img class="small" src="/assets/images/posts/bash.png" width="375" height="158" />
        <figcaption>Angular</figcaption>
</figure>

## Looping FTP
Example usage would be to push a file to a set of clients

**updt.bat**
Main executable
{% highlight batch linenos %}
@echo off
FOR /F "tokens=3 delims=|" %%i in (list) DO ftp -s:updt %%i >> updt.out
{% endhighlight %}

**ftpCmds.txt**
FTP Commands to run once connected
{% highlight linenos %}
sys_username
sys_password
bin
cd desired/path
put filename.exe
bye
{% endhighlight %}

**ftpServers.txt**
Servers and any other info you may need later
{% highlight batch linenos %}
token 1|token 2|192.168.0.1 |token 4|token 5|
token 1|token 2|192.168.0.2 |token 4|token 5|
token 1|token 2|192.168.0.3 |token 4|token 5|
...
{% endhighlight %}

**filename.exe**
This can be a uuencoded install script or really anything

## Looping Excecutable
Similar to bash's xargs, this allows you to iterate over each file in a directory and execute/modify

**printFiles.bat**
{% highlight batch linenos %}
@ECHO OFF
SETLOCAL
set file=.\*
FOR %%i IN ("%file%") DO (
ECHO filedrive=%%~di
ECHO filepath=%%~pi
ECHO filename=%%~ni
ECHO fileextension=%%~xi
)
{% endhighlight %}

**Create XSDs**
{% highlight batch linenos %}
for %%i in (.\*) DO xsd %%i  /c /n:myNamespace.XSD.%%~ni /o:..\..\MyProject\GeneratedClasses\
{% endhighlight %}

[MS Docs - batch for](https://docs.microsoft.com/en-us/windows-server/administration/windows-commands/for)

## Create Shortcut
Creates a shortcut to a given file
{% highlight batch linenos %}
rem Creating the File Shortcut
@echo off
set SCRIPT="%TEMP%\%RANDOM%-%RANDOM%-%RANDOM%-%RANDOM%.vbs
echo Set oWS = WScript.CreateObject("WScript.Shell") >> %SCRIPT%
echo sLinkFile = "\Path\To\Shortcut.lnk" >> %SCRIPT%
echo Set oLink = oWS.CreateShortcut(sLinkFile) >> %SCRIPT%
echo oLink.TargetPath = "\\Path\To\File.exe" >> %SCRIPT%
echo oLink.Save >> %SCRIPT%
cscript /nologo %SCRIPT%
del %SCRIPT%
{% endhighlight %}

