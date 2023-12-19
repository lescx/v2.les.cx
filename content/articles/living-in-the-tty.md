+++
draft = false

title = 'Living in the TTY'
subtitle = '> Do you expect to run the X Window System? no'
summary = 'Hier stehe eine sehr tolle Zusammenfassung.'

date = 2023-10-08T10:32:00+02:00
+++

*Oct 2023: This article is in WIP since 2022. Once I successfully finished my project, this disclaimer will disappear. Also, then the article will be written in English. Return later.*

Seit 2021 denke ich viel darüber nach, mein digitales Leben vollständig in ein "OG Terminal" zu verschieben. Viel Charme hatte ich insbesondere dem Gedanke abgewonnen, meine Arbeiten an einem alten Macintosh mit OpenBSD zu erledigen. Alter Monitor, alte Tastatur, hohe Stromkosten.

![Insert image of "OG Terminal"]()

Das heißt keine grafische Oberfläche. Kein Browser. Das Ganze ist aus einem Verdruss entstanden, dass alle bekannten Betriebsysteme ziemlich mies sind. Und Xorg. [Hier bisschen ausführlicher] Plan9 hätte ein gutes Betriebsystem werden können mit grafischer Oberfläche by design, aber Plan9, sein nicht-Erfolg und mehr, ist ein eine ganze Artikelserie für sich.

Im Grunde genommen wollte ich unnötiges herumsurfe im Internet minimieren, mich tiefer mit OpenBSD auseinandersetzen und C und Rust lernen. Ich höre schon die Stimmen, die sagen *aber ist das nicht total unnötig und macht das Dein Leben nicht viel schwerer als es sein müsste?* Ja.

Ich möchte wissen, ob es möglich ist, in ~~2022~~ 2023 zurück in das digitale Mittelalter zurückzufallen - auch, wenn ich mich täglich frage, wie weit wir wirklich fortgeschritten sind seit dem Ende des virtuellen Terminals als Benutzeroberfläche.

## Was mache ich an meinem Rechner?

Bevor ich mich halb-über-Kopf in das Projekt stürze, sollte ich mir hier, mehr denn je, über die Konsequenzen Gedanken machen. Ich muss mir klar machen, dass ich dennoch einen weiteren Rechner brauche für Studium und Arbeit. Nicht zuletzt möchte ich auch hin und wieder mal einen Film anschauen.

### ist mir wichtig/ist notwendig

* VPNs
* RSS: [sfeed](https://codemadness.org/sfeed-simple-feed-parser.html)
* Emails: `neomutt`? `meli`? `himalaya`?
	* Personal Accounts via IMAP/SMTP with PGP
	* University Emails via Microsoft Exchange
* Encrypt messages with PGP/age
* IRC (TLS only) [catgirl](https://git.causal.agency/catgirl/about/)
* Calendar + Reminder
* Markdown + LaTeX Notes
	* ASCII Art Mathmatical Expressions
* Music [amused](https://projects.omarpolo.com/amused.html)
* Password Manager
* SSH
* Torrents? For what?
* Yubikeys
* Programming
	* Helix Editor
	* Hugo for website
	* C, Shell, Lisp (Scheme), Python, Rust, HTML+CSS development environment
* Read books
* PDFs?
* Gopher/Gemini browser
* HTTPS Web browser

## Installation

Beginn:

* Installation ohne Spiele, Xorg-basierten Pakete,… --> Achtung! Bei Upgrade ist Mehrarbeit angesagt!
* Kein Xorg (Xenocara) darf installiert werden
* Nur ein TTY mit tmux ist erlaubt

> Do you expect to run the X Window System? [yes]
>no