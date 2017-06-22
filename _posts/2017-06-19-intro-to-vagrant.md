---
layout: single
title: Getting started with VirtualBox and Vagrant
header:
    teaser: assets/images/vagrant.png
category: tutorial
---

## Intro to Vagrant

If you've been attending our MSBA optional sessions you've definitely noticed that there is a challenge getting our dev tools to work consistently across everyone's computers. Most noticeably, Windows users have had a tough time due to the fact that most developer tools we've covered aren't really designed to work well with Windows.

Our standard solution is to make use of VMs, or virtual machines. VMs are a vital tool in the developer world as it solves a significant problem... getting everyone's systems in a consistent state. Not only does this allow our Windows using friends to practice their bash/Linux skills but it also allows us to do some other neat things, like spin up database servers with the push of a button.

While there are many different VM/Container solutions, we're going to make use of [Vagrant](https://www.vagrantup.com/) as it is flexible, easy to use, and easy to set up.

## Installation

Vagrant is a tools used to help create and manage VMs, but doesn't actually do the work of running the VM. For that, we will need [Virtualbox.](https://www.virtualbox.org/wiki/VirtualBox)


### OSX via Homebrew

If you are using OSX then you can handle the entire installation process with homebrew. Simply fire up a terminal and enter the following commands:

```
brew cask install virtualbox
brew cask install vagrant
```

**Note:** This assumes you have set up homebrew. Refer to the [website](https://brew.sh/) for more info.
{: .notice--warning}

### Manual Installation

For Windows users, or for OSX users who don't want to muck around in homebrew, you can manually download and install each program the 'old fashioned way':

1. [Download](https://www.virtualbox.org/wiki/Downloads) and install Virtualbox
2. [Download](https://www.vagrantup.com/downloads.html) and install Vagrant

## Up and running

Vagrant is all about streamlining the setup and management of VMs. Vagrant makes use of "boxes", predefined minimal machine images that can be used to spin up VMs very quickly. The box we'll be using for all of our VM projects is ubuntu/trusty64. We can easily install it with the following command:

```
vagrant box install ubuntu/trusty64
```

**Note:** This could take a little while. Make sure you have a good internet connection and a snack.
{: .notice--info}

Once the installation is done we are ready to rock. Vagrant uses a special config file called a `Vagrantfile` to manage how a VM is spun up. This makes "sharing" VMs as easy as sharing a single text file. In fact, I've got one for you right [here.](https://github.com/JCPistell/msba_vagrantfile) Alternatively, you can have Vagrant create a standard one for you. Simply create a directory in which you want to store your VM and make use of `vagrant init`. For example:

```
mkdir vagrant_test_directory
cd vagrant_test_directory
vagrant init ubuntu/trusty64
```

Vagrant will create a Vagrantfile for you, configured to use our ubuntu/trusty64 box. We can spin up our VM like so:

```
vagrant up
```

Vagrant will now go through two steps - booting your VM and provisioning it. Wait for the process to finish. You're done! you can confirm your machine is up and running with the following command:

```
vagrant global-status
```

## Hooray! ...now what?

How do we actually use our VM? If we're on OSX we can simply ssh in:

```
vagrant ssh
```

A shell should open in our new VM. Hack away! When you're ready to exit you can type `exit` to return to your native shell.

Windows users have an additional problem: Windows does not come with an ssh client. You have a few options, nicely outlined in [this blog post.](http://tech.osteel.me/posts/2015/01/25/how-to-use-vagrant-on-windows.html) If you haven't installed git yet I'd pursue that option. Once you're done, you should be able to `vagrant ssh` normally.

## Halt and Destroy

When you are done working with your VM you'll want to turn it off so it doesn't continue to consume system resources. You can shut it down with the following command:

```
vagrant halt
```

This will turn off your VM, but maintain the image on your system. This means you will be able to quickly boot it back up with a `vagrant up` command. The nice thing is Vagrant will not need to provision your VM after the first boot up, so starting up again will be much faster.

Alternatively, you may want to completely erase your VM... removing all traces it ever existed. For that you can use:

```
vagrant destroy
```

This will remove the VM and any files and directories that were on it.

Note that the Vagrantfile remains, so you can easily create the exact same VM again, but Vagrant will need to reprovision the box, so the initial boot will take longer.

## Enjoy

Vagrant can be used to create as many sandbox environments as you want where you can safely play around without fear of damaging your native system. If you hopelessly ruin your VM, simply destroy it and reboot... this is a great way to learn the ins and outs of Linux in a consequence-free environment.

There's a lot more to Vagrant than just spinning up simple sandboxes. I encourage you to read the [documentation](https://www.vagrantup.com/docs/index.html) for more information. Next time, we'll use Vagrant to easily spin up a self contained mysql server that will let us mess around with databases without those pesky AWS fees.