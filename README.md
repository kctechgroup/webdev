# KC Tech Group WebDev Image
This repository contains a Vagrantfile that can be used to setup your own development environment custom-tailored for our Hexo-based deployment!  

## Prerequisites

In order to get started, make sure you've installed some prerequisites on your computer:

* [Oracle VirtualBox](https://virtualbox.org) - Downloads page [here](https://www.virtualbox.org/wiki/Downloads)
* [Vagrant](https://vagrantup.com) - Downloads page [here](https://www.vagrantup.com/downloads.html)

## Getting Started

If you're new to Vagrant, perhaps take a run through their [Getting Started](https://www.vagrantup.com/intro/getting-started/index.html) guide.  Once you've got those installed, simply clone this repository and then run `vagrant up`:

```shell
git clone https://github.com/kctechgroup/webdev kctechgroup.webdev
cd kctechgroup.webdev
vagrant up
```

The virtual machine will bring in the template image (it will need to download this only the first time, after that you'll be able to create other Vagrant instances based on that same image with no extra downloads) and then begin to download, install, and configure all of the required dependencies to get you up and running with Hexo and KC Tech Group's website.  

TODO: Show provisioning of Vagrant instance.

## Connecting to your Vagrant environment

TODO: Provide instruction for SSH'ing into the Vagrant environment.

## Sharing your Website Edits in Development

TODO: Provide instruction/links to Vagrant Share functionality on HashiCorp website.

## Setting up GitHub/SSH Credentials

TODO: Provide information on how to configure Git/SSH integration to KC Tech Group GitHub organization.

## Using Hexo

TODO: Hexo quick-start (for KC Tech Group).

### Previewing the Site

TODO: Provide instruction on using Hexo to preview the site.

### Creating a post

TODO: Provide instruction on creating a post.

## Shutting down the environment

TODO: Provide information on shutting down the Vagrant environment.

