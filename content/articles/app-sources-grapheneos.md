+++
draft = false

title = 'A Summary of App Repositories for GrapheneOS'
subtitle = "Don't bully the app store with only 12 apps… :("
tldr = 'Ideally, only use GrapheneOSs *Apps* app and [Accrescent](https://accrescent.app).  If you use the sandboxed Google Play Services then make use of the Google Play Store!  Download [Obtainium](https://github.com/ImranR98/Obtainium) from GitHub for APKs not found on Accrescent or in the Google Play Store.'

# SEO ~150 chars max
description = 'A comparison of different sources to retrieve apps from for GrapheneOS.'
# SEO keywords
keywords = ['GrapheneOS', 'Aurora Store', 'F-Droid', 'Accrescent', 'Obtainium']

date = 2023-09-17T18:13:10+02:00
+++

Since in the GrapheneOS Matrix rooms the question arises almost daily about the best way to obtain Apps, this is a short "how to" and "why to" for GrapheneOS users.  The goal is to obtain Apps from a source that is trustworthy and secure without being altered on the way to the device.

Important: I think it's clear that no app store in the world protects against an app having backdoors built in by its own developers. Therefore, you should think about *which* apps you want to have installed on your device beforehand.

I'm writing a short "what you should definitely not do" here.  I assume this as a consensus.

## Do not…

Do not download APKs from unofficial sources.  This includes every site of the first trillion pages you see on your preffered search engine when you enter "clash of clans apk".  This includes apkpure, Uptodown, APKMirror and other known direct download websites.

Do not install APKs someone sent you via WhatsApp.  Or Telegram.  Or email.  Or Signal.

Below are the sources from which you should obtain your apps in descending order, starting with the GrapheneOS Apps app and Accrescent.

## GrapheneOS's *Apps* App

-- To-Do --


## Accrescent

And here we are… The app source with 12 apps. [Accrescent](https://accrescent.app/).

Accrescent's focus is to have a modern code base with a focus on privacy and security.

> Accrescent will *remove* apps when they don't meet the target SDK

[Target SDK](https://support.google.com/googleplay/android-developer/answer/11926878)

For a full list of features, please take a look at the [FAQ](https://accrescent.app/faq), [features](https://accrescent.app/features) and also the [App requirements](https://accrescent.app/docs/guide/publish/requirements.html) section on which apps are allowed to be hosted on Accrescent.

Also…:

* Unlike F-Droid, they actually care if the signature changes!
* Accrescent uses a strong signing method for its repository metadata than F-Droid (Ed25519 whole-file signing vs Jar signing)


## Sandboxed Google Play Store

I want to point out again that this guide is *not* looking for the most private way to obtain its apps, but the most secure, as defined above.

* https://nitter.net/GrapheneOS/status/1497272529223917575
* Developer and Google sign the app.
* Strict minimum SDK (same Accrescent uses) - but do not remove apps that don't match target API level. Read here: [Target API level requirements for Google Play apps](https://support.google.com/googleplay/android-developer/answer/11926878)


## Obtainium

Most repository hosting provider (GitHub, GitLab, Codeberg,…) allow subscribing to a project via RSS feeds. Many even support multiple RSS feeds on a per commit or per release basis.

[Obtainium](https://github.com/ImranR98/Obtainium) builds on top of this concept and allows a direct download of apps straight from the source.
Obtainium also scrapes from some website app sources like MullvadVPN, Signal. See their documentation for a long list of supported sources.

The UI and codebase are modern, with the code written in Dart. Updates can be rolled out fast by design.

*Caveat:* The project is pretty new so not everything works perfectly (e.g. GitLab requires an API key to download apps) - but it works as a daily driver! Also, the core problem remains: (GitHub) releases aren't a trustworthy solution for APK installation.


## APK von GitHub Releases

* GitHub releases are not all the same. Ultimately, GitHub releases are just git tags and nothing stops a developer (and or malicious actors) from injecting manipulated APKs. 
* Uniform and simpler infrastructure for the developer and user in comparison to websites.
* Signatures can be verified but UI doesn't tell at all if signing key has changed.
    * Means, similar process to GPG via website
* CI/CD possible to build APKs using GitHub Pipeline.


## Aurora Store

Reasons, why you might want to use Aurora Store in the past:

* One would like to use "anonymously" one's apps such as WhatsApp and Netflix from the Google Play Store without logging in with a Google account.
* One does not want to or cannot use a Google Play Store.
* Security issue: The Google Play Store has special rights on one's own device and is not subject to the same App Sandbox as other apps are.


## F-Droid (and derivates)

I recommend this article on [F-Droid Security Issues](https://privsec.dev/posts/android/f-droid-security-issues) which goes into great detail. ([Wayback Machine](http://web.archive.org/web/20230000000000*/https://privsec.dev/posts/android/f-droid-security-issues))

See also…

* [2023-09-03 F-Droid: Reproducible builds, signing keys, and binary repos](https://f-droid.org/en/2023/09/03/reproducible-builds-signing-keys-and-binary-repos.html)
* [2022-02-25 GrapheneOS: On Google Play Store and F-Droid](https://nitter.net/GrapheneOS/status/1497273173364166662)


## APKs from Official Websites

I guess Windows users in particular like to do this because for a long time it was a matter of course on the platform to go to the official website (or not) of a specific program and download the .exe or .msi file. For the most part, you shouldn't do that on Windows, nor on other platforms.

There is no signature check happening if the APK is *actually* coming from the developer(s).
Also: Do you check the APK hash and PGP signature on android? Probably not.

Not a particularly confidence-inspiring way to obtain an app.
And not a user-friendly one. How often have you checked the PGP signature on your phone for a programme?


## Conclusion

Currently it isn't possible to just use Apps and Accrescent. If you do not want to use Google Play Services, then use Obtainium. Otherwise also use the Google Play Store where you can.