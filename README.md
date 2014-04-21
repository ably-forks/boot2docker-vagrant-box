# WiP from dduportal

My goal is to run boot2docker as a dev environment into vagrant with these constraints :
- Vagrant is running on Windows 7/8 x64 with virtualbox provider (no vbox tools, no built-in NFS, how to share contents beetween Win and b2d ? vagrant-winnfsd ?)
- We want to use fig (http://orchardup.github.io/fig/) for dealing with docker
- We can run into a corporate env, with an HTTP proxy

So this fork of mitchellh is going to fully build b2d from the original github, customize our iso and generate a vagrant box.

... WIP ...
- Need to add etc profile to docker dameon in order to auto load proxy if configured
- Moving basebox to docker 0.8.x
- Using a docker polipo image, in order to cache downloaded content accross multi builds
- Integrate fig install (tester manually into b2d, need to inject with mitchellh customization script )
- Test test test !  

# boot2docker Vagrant Box

This repository contains the scripts necessary to create a Vagrant-compatible
[boot2docker](https://github.com/steeve/boot2docker) box. If you work solely
with Docker, this box lets you keep your Vagrant workflow and work in the
most minimal Docker environment possible.

## Usage

The box is available on
[Vagrant Cloud](https://vagrantcloud.com/mitchellh/boot2docker), making
it very easy to use it:

    $ vagrant init mitchellh/boot2docker
    $ vagrant up

If you want the actual box file, you can download it from the
[releases page](https://github.com/mitchellh/boot2docker-vagrant-box/releases).

On OS X, to use the docker client, simply `export DOCKER_HOST=localhost`.
You should then be able to to run `docker version` from the host.

![Vagrant Up Boot2Docker](https://raw.github.com/mitchellh/boot2docker-vagrant-box/master/readme_image.gif)

## Building the Box

If you want to recreate the box, rather than using the binary, then
you can use the scripts and Packer template within this repository to
do so in seconds.

To build the box, first install the following prerequisites:

  * [Packer](http://www.packer.io) (at least version 0.5.1)
  * [VirtualBox](http://www.virtualbox.org) (at least version 4.3) or VMware
  * [Vagrant](http://www.vagrantup.com)

Then follow the steps:

```
$ vagrant up
...
$ vagrant ssh -c 'cd /vagrant && sudo ./build-iso.sh'
...
$ vagrant destroy --force
...
$ packer build template.json
...
```

You can restrict only VirtualBox or VMware by specifying the `-only` flag
to Packer.
