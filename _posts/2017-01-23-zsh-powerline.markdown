---
layout: post
title:  "Enhance your shell using zsh and much more"
img: 61047262
img_type: png
comments: true
tag: non-ACG
date:   2017-01-23 16:23:32 -0500
outline: This tutorial shows you the installation and some confgiurations of zsh, which I believe is a enhanced version of bash.
---
This tutorial shows you the installation and some confgiurations of the `zsh`, which I believe is a enhanced version of `bash` and other small yet powerful plugins to make your cmd interface more beautiful and efficient to use. Here is a preview picture.
![alt text]({{ site.url }}/assets/images/zsh/preview.JPG "Preview picture")

## Prerequisite
---
* OS: Debian GNU/Linux 8 (jessie)
* `Git` Installed
* Python v2.6+ except 3.2
* `pip` installed

For windows users, you may refer to [Bash on Ubuntu on Windows](https://msdn.microsoft.com/en-us/commandline/wsl/about) for more detailed information. Currently there is no native support for `zsh` on Windows. For Mac users, `zsh` is alrady embedded in the system, but we may add more plugins to make it even more powerful, please refer to [Configure zsh](## Configure zsh) 

If you don't have `Git` (which you should have one if you are a programmer), refer to [Installing Git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git).

If you don't have Python or `pip`, please refer to [Download Python](https://www.google.co.jp/?gws_rd=ssl#q=python+install) or [Download pip](https://pip.pypa.io/en/stable/installing/)

## Install zsh
---
There are two ways to install `zsh`, one is to get the native version using

```
$ apt-get install zsh
```

Then run `zsh` on your terminal will do the job. When you first run it, it will let you configure `.zshrc` or leave it blank. To make `zsh` your default shell prompt, run

```
$ chsh -s /bin/zsh
```

Notice that `sudo` is not needed in the command. If you add `sudo`, then it will change the default for the root user, not current user.

The second approach is more recommanded, which uses a well-known project on Github called [oh-my-zsh](https://github.com/robbyrussell/oh-my-zsh). To install it via this project, just run 

```
$ sh -c "$(curl -fsSL https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"
```

There are several reaons why I prefer `oh-my-zsh`. First it already gives you a well-defined `~/.zshrc` . You can customize there for things like enabling auto-correction for commands, adding the timestamp for `history` command and so on. Second is that it has many beautiful themes that you can choose, the default is 

{% highlight bash %}
ZSH_THEME="robbyrussell"
{% endhighlight %}

you may find various screenshots [here](https://github.com/robbyrussell/oh-my-zsh/wiki/themes). 

## Enhance zsh
---
Well, to be honest the default `zsh` may not be so exciting. However, after some configurations it will be better than you can imagine.

The most exciting thing about `oh-my-zsh` is that it gives us a wide range of useful plugins for `zsh`. To install them, just add the names in `.zshrc`, and you may look for many other good pugins [here](https://github.com/robbyrussell/oh-my-zsh/wiki/Plugins)

{% highlight bash %}
plugins=(git)                                                              
plugins=(... osx) 
{% endhighlight %}

Of course, just like `bash`, you can add your alias to type fewer words. Like mine,

{% highlight bash %}
alias grep="grep --color=auto"
alias vi='vim'
alias clr='clear'
alias -s c=vi
alias -s h=vi
alias -s java=vi
alias -s py=vi
alias zshconfig="vi ~/.zshrc"
alias ohmyzsh="vi ~/.oh-my-zsh"
alias ll="ls -al"
{% endhighlight %}

Here `alias -s c=vi` let you just type in a document with the suffix `.c`, then it will open it in `vim`. Very efficient, isn't it?

Besides, many other tools can be integrated in `zsh` to make it even better, and I will introduce two of them, `autojump` and `powerline`

### autojump

[autojump](https://github.com/wting/autojump) is a very powerful tool to quickly search for accessed folders. It supports fuzzy search in a great way. For example, if you have accessed a folder named `abcdefghh-log-2017-1-23`, and you run `$ j 2017-1-23`, it will directly point you to the right directory. 

`autojump` is written in Python and can be integrated in `zsh`. The documentation of it can be found at [autojump documentation](https://github.com/wting/autojump)To intall and enable it, run 

```
$ apt-get install autojump
```
and add 

```
[[ -s ~/.autojump/etc/profile.d/autojump.sh ]] && . ~/.autojump/etc/profile.d/autojump.sh
```

to your `.zshrc` and restart the shell session to make it in effect.

### powerline

[powerline](https://github.com/powerline/powerline) is a tool that enhances the interface of the shell. You can make your `zsh` provide more information on the terminal, like time, battery usage, even weather. To install `powerline`, run

```
$ pip install --user powerline-status
```

Next you _MUST_ install the font needed for `powerline`, otherwise you have strage-looked symbol in your shell. you may refer to [font installation](https://powerline.readthedocs.io/en/latest/installation/linux.html) or just run the command below, if you don't want to know what they mean...

```
$ wget https://github.com/powerline/powerline/raw/develop/font/PowerlineSymbols.otf
$ wget https://github.com/powerline/powerline/raw/develop/font/10-powerline-symbols.conf
$ mv PowerlineSymbols.otf ~/.fonts/
$ fc-cache -vf ~/.fonts/
$ mv 10-powerline-symbols.conf ~/.config/fontconfig/conf.d/
```

Then you need to know `{ powerline_dir }`, which can be found under location tab if you run `$ pip show --user powerline-stauts`, then add the these lines to `.zshrc` to make `powerline` work.

{% highlight bash %}
PATH=~/.local/bin:$PATH
. { powerline_dir }/powerline/bindings/zsh/powerline.zsh
{% endhighlight %}

To customize `powerline`, like you want to see the weather at the right end of your shell prompt, you may refer [here](https://powerline.readthedocs.io/en/latest/configuration.html)

## Wrap up
---
Most of the plugins and tools I mentioned above can also be embedded in other tools like `bash` or `vim`. Maybe I will write another tutorial about these things. See you soon.