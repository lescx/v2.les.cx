+++
draft = false
title = 'The future of LXD does not look good on ChromeOS'
date = 2024-01-02T21:31:00+02:00
+++

What you should take from this article if you don't want to read everything?

Starting in mid-April, it will not be possible for ChromeOS LXD users to get new LXD images for distributions other than the `ubuntu:` and `ubuntu-daily:` remotes from Canonical and the Debian "penguin" image from Googles CDN. The image server at https://images.linuxcontainers.org is getting phased out.

---

[1] https://discuss.linuxcontainers.org/t/important-notice-for-lxd-users-image-server/18479
[2] https://discuss.linuxcontainers.org/t/the-future-of-lxc-incus-images-on-chromeos/18590
[3] https://stgraber.org/2023/12/12/lxd-now-re-licensed-and-under-a-cla/

ChromeOS Nutzer, die schonmal ein Terminal geöffnet haben, haben, ob bewusst oder nicht, schon einmal [LXD](https://wiki.archlinux.org/title/LXD) verwendet. Kurzgesagt wird LXD verwendet, um Linux in einer isolierten Umgebung nutzen zu können. Klingt ein wenig nach Docker, ist aber cooler! :-) 

Und auch ähnlich zu Docker, wo man images von [Docker Hub](https://hub.docker.com) herunterlädt, lädt man die images bei LXD häufig von [images.linuxcontainers.org](https://images.linuxcontainers.org) herunter. Der Unterschied zu Docker Hub ist, dass die LXD images von nur zwei maintainern gebaut und bereit gestellt wurden, mit Unterstützung von [Canonical](https://canonical.com/). Und das fällt LXD Nutzern, und insbesondere ChromeOS Nutzern, bald auf die Füße. Aber von vorn…

## What happended?

[Thomas Hipp](https://github.com/monstermunchkin), einer der Hauptentwickler für LXD, hat im November 2023 Canonical verlassen. Canonical hat daraufhin sämtliche Finanzierungen an dem image server images.linuxcontainers.org eingestellt. Die Kosten können aktuell nicht nachhaltig bezahlt werden. Der Zugang zu images.linuxcontainers.org wird nach und nach eingestellt mit Übergangsfristen. Bekannt gegeben wurde das [in dem blog post](https://discuss.linuxcontainers.org/t/important-notice-for-lxd-users-image-server/18479) von Stéphane Graber, einem der Haupt-maintainer von LXD, Mitte Dezember 2023 inklusive konkreter Fristen.

Ganz neu ist außerdem, dass Canonical sich dazu entschieden hat, mit nur einem commit die LXD Lizenz von Apache2 auf AGPLv3 zu ändern. Außerdem zwingen sie alle contributions to sign the Canonical CLA.

The Canonical image mirror sites ([UK](https://uk.lxd.images.canonical.com/), [US](https://us.lxd.images.canonical.com/)) were last updated in August 2023 und bieten nur noch `ubuntu:` und `ubuntu-daily:` images an.

## The ChromeOS issue

Pffifige Füchse fragen sich vielleicht, was mit dem Debian image ist, welches in ChromeOS `penguin` genannt wird. Dieses image wird nicht von dem öffentlichen image server bezogen, sondern von einem privaten Google CDN gebaut und publiziert. Diese images sind von dem Abschalten des image servers nicht betroffen. Einen Einstieg in die Unterschiede zwischen "Vanilla Debian" und dem ChromeOS image wurde in dem blog post [A closer look at Chrome OS using LXD to run Linux GUI apps](https://blog.simos.info/a-closer-look-at-chrome-os-using-lxd-to-run-linux-gui-apps-project-crostini/) von Simos Xenitellis gegeben.

Das Problem wird konkret, wenn man ein image verwenden möchte, welches nicht das bereitgestellt Debian oder Canonical's Ubuntu ist. Beispielsweise wenn man ein Paket für andere Linux-Distros testen möchte, einen Alpine Linux container braucht, einen Kali Container aufmacht oder mit Busybox spielen möchte.

ChromeOS hat tatsächlich den images.linuxcontainers.org image server in seiner remote list, überprüfbar via `crosh`:

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

[Bis Mitte-April](https://discuss.linuxcontainers.org/t/the-future-of-lxc-incus-images-on-chromeos/18590) wird man weiterhin seine images herunterladen können. Was danach geschieht, ist im Moment noch unklar.

Google ist dafür bekannt, keine AGPL licensed software in ihren Produkten zu verwenden. Die Gründe weichen vom Thema dieses Artikels ab, aber eine ähnliche Situation kennt man beispielsweise von Apple mit ihrer steinalt-`bash` Version. Im Moment sieht es so aus, als ob ChromeOS bis LXD Version 5.20 upgraden kann und dann wir Nutzer ein Problem haben, welches im Moment noch keine absehbare Lösung bereithält. 

## The Incus hard fork

In Folge der plötzlichen Lizenzänderung von Canonical und der damit verbundenen CLA, musste LXD leider unter Zwang einem hard fork unterzogen werden.

> Incus is a fork of LXD, which is a daemon that is primarily used to manage containers. It tends to be favored by those who wish to treat containers as if they were full system images.
> 
> Canonical, relatively recently, (LXD/LXC/Libvirt/etc have been around for a long time) added support for managing virtual machines to LXD for some reason with their 4.0 LTS release. So in a way it is a competitor with Libvirt.^2
>
> [2] https://www.reddit.com/r/linux/comments/15ldqng/comment/jvch136

## Workarounds for the future

LXD erlaubt nested container (insert). Das heißt, es ist möglich, Incus oder Docker bereits heute in ChromeOS ohne Probleme zu verwenden. Das fühlt sich natürlich "hacky" an, wenn man erst ein Debian image aus LXD heraus öffnet, um bspw. Docker zu starten, in dem dann ein Alpine Linux läuft.

## The ideal solution

Incus, a fork of LXD, is one possible alternative to LXD on ChromeOS. Sadly, it's not possible to replace LXD with Incus on ChromeOS.
Ideally, Google provides more images besides the debian, if not via a public image server, than maybe natively from ChromeOS with their CDN.