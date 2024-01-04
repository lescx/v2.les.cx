+++
draft = false
title = 'The future of LXD does not look good on ChromeOS'
date = 2024-01-02T21:31:00+02:00
+++

Starting in mid-April 2024, it will not be possible for ChromeOS LXD users to get new LXD images for distributions other than the `ubuntu:` and `ubuntu-daily:` remotes from Canonical and the Debian "penguin" image from Googles CDN. The image server at https://images.linuxcontainers.org is getting phased out.

---

## Introduction

ChromeOS users who have ever opened a terminal have, whether consciously or not, used [LXD](https://wiki.archlinux.org/title/LXD). In short, LXD is used to run Linux in an isolated environment. Sounds a bit like Docker, but it's cooler! :-) 

And also similar to Docker, where you download images from [Docker Hub](https://hub.docker.com), with LXD you often download the images from [images.linuxcontainers.org](https://images.linuxcontainers.org). The difference to Docker Hub is that the LXD images were built and provided by only two maintainers, with support from [Canonical](https://canonical.com/). And this soon falls on the feet of LXD users, and ChromeOS users in particular. But from the beginning…

## What happended?

[Thomas Hipp](https://github.com/monstermunchkin), one of the main developers for LXD, left Canonical in November 2023. Canonical has subsequently cancelled all funding for the image server images.linuxcontainers.org. The costs cannot currently be paid sustainably. Access to images.linuxcontainers.org will be gradually discontinued with transition periods. This was announced [in the blog post](https://discuss.linuxcontainers.org/t/important-notice-for-lxd-users-image-server/18479) by Stéphane Graber, one of the main maintainers of LXD, in mid-December 2023, including specific deadlines.

What is also brand new is that Canonical has decided to change the LXD licence from Apache2 to AGPLv3 with just one commit. They are also forcing all contributions to sign the Canonical CLA. [This is a bad idea.](https://stgraber.org/2023/12/12/lxd-now-re-licensed-and-under-a-cla)

The Canonical image mirror sites ([UK](https://uk.lxd.images.canonical.com/), [US](https://us.lxd.images.canonical.com/)) were last updated in August 2023 und bieten nur noch `ubuntu:` und `ubuntu-daily:` images an.

## The ChromeOS issue

Pffiffy foxes may wonder what about the Debian image, which is called `penguin` in ChromeOS. This image is not obtained from the public image server, but is built and published by a private Google CDN. These images are not affected by the shutdown of the image server. An introduction to the differences between "Vanilla Debian" and the ChromeOS image was given in the blog post [A closer look at Chrome OS using LXD to run Linux GUI apps](https://blog.simos.info/a-closer-look-at-chrome-os-using-lxd-to-run-linux-gui-apps-project-crostini/) by Simos Xenitellis.

The problem becomes concrete if you want to use an image that is not the provided Debian or Canonical's Ubuntu. For example, if you want to test a package for other Linux distros, need an Alpine Linux container, open a Kali container or want to play with Busybox.

ChromeOS actually has the images.linuxcontainers.org image server in its remote list, checkable via `crosh`:

```shell
(termina) chronos@localhost ~ $ lxc remote list   
+-----------------+------------------------------------------+---------------+-------------+--------+--------+--------+
|      NAME       |                   URL                    |   PROTOCOL    |  AUTH TYPE  | PUBLIC | STATIC | GLOBAL |
+-----------------+------------------------------------------+---------------+-------------+--------+--------+--------+
| images          | https://images.linuxcontainers.org       | simplestreams | none        | YES    | NO     | NO     |
+-----------------+------------------------------------------+---------------+-------------+--------+--------+--------+
| local (current) | unix://                                  | lxd           | file access | NO     | YES    | NO     |
+-----------------+------------------------------------------+---------------+-------------+--------+--------+--------+
| ubuntu          | https://cloud-images.ubuntu.com/releases | simplestreams | none        | YES    | YES    | NO     |
+-----------------+------------------------------------------+---------------+-------------+--------+--------+--------+
| ubuntu-daily    | https://cloud-images.ubuntu.com/daily    | simplestreams | none        | YES    | YES    | NO     |
+-----------------+------------------------------------------+---------------+-------------+--------+--------+--------+
```

[Until mid-April](https://discuss.linuxcontainers.org/t/the-future-of-lxc-incus-images-on-chromeos/18590) you will still be able to download your images. What happens after that is still unclear at the moment.

Google is known for not using AGPL licensed software in its products. The reasons differ from the topic of this article, but a similar situation is known for example from Apple with their steinalt-`bash` version. At the moment it looks as if ChromeOS will be able to upgrade to LXD version 5.20 and then we users will have a problem that has no foreseeable solution at the moment. 

## The Incus hard fork

As a result of Canonical's sudden licence change and the associated CLA, LXD unfortunately had to undergo a hard fork under duress.

> Incus is a fork of LXD, a daemon mainly used to manage containers. It is favoured by those who want to treat containers like complete system images.
> 
> Canonical has only recently (LXD/LXC/Libvirt/etc have been around for a long time) added virtual machine management support to LXD with version 4.0 LTS, for some reason. So in a way it is a competitor to Libvirt.^2
>
> [2] https://www.reddit.com/r/linux/comments/15ldqng/comment/jvch136

## Workarounds for the future

LXD allows nested containers (insert). This means that it is already possible to use Incus or Docker in ChromeOS today without any problems. Of course, this feels "hacky" if you first open a Debian image from LXD to start Docker, for example, in which an Alpine Linux is then running.

## The ideal solution

Incus, a fork of LXD, is a possible alternative to LXD under ChromeOS. Unfortunately, it is not possible to replace LXD under ChromeOS with Incus.
Ideally, Google provides other images besides the Debian image, if not via a public image server, then perhaps natively from ChromeOS with their CDN.