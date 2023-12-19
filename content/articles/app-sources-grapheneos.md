+++
draft = false
title = 'A Summary of App Repositories for GrapheneOS'

# SEO ~150 chars max
description = 'A comparison of different sources to retrieve apps from for GrapheneOS.'
# SEO keywords
keywords = ['GrapheneOS', 'Aurora Store', 'F-Droid', 'Accrescent', 'Obtainium']

date = 2023-09-17T18:13:10+02:00
+++

**tl;dr:**

For GrapheneOS users, the best practice is to use the Apps app and Accrescent, supplemented by the Google Play Store if Google Play Services are in use. In the absence of these options, Obtainium is a viable alternative. Stay cautious and informed about the sources of your app downloads.

---

Users often seek guidance on secure app procurement. This write-up tries to answer the question where to obtain apps in a short and precise way.

Remember, no app repository can guarantee against backdoors introduced by the developers themselves. Thus, choose your apps wisely.

## Do not…

Do not download APKs from unofficial sources.  This includes every site of the first trillion pages you see on your preffered search engine when you enter "clash of clans apk".  This includes apkpure, Uptodown, APKMirror and other known direct download websites.

Do not install APKs someone sent you via WhatsApp.  Or email.  Or Signal.


## APK von GitHub Releases

* GitHub releases are not all the same.  Ultimately, GitHub releases are just git tags and nothing stops a developer (and or malicious actors) from injecting manipulated APKs. 
* Uniform and simpler infrastructure for the developer and user in comparison to websites.
* Signatures can be verified but UI doesn't tell at all if signing key has changed.
    * Means, similar process to GPG via website
* CI/CD possible to build APKs using GitHub Pipeline.


## Recommended Sources for App Downloads

1. GrapheneOS's Apps App

* Comes pre-installed with GrapheneOS.
* Only features pre-installed apps for GrapheneOS.

2. [Accrescent](https://accrescent.app/)

> The app source with 12 apps.

* Focuses on privacy and security with a modern code base.
* Removes apps not meeting the target SDK, thus modern standards.
* More vigilant about developer signature changes compared to F-Droid.
* Employs ed25519 whole-file signing for repository metadata.

3. Sandboxed Google Play Store

I'm *not* talking about MicroG which is not recommended to use at all.

* Offers both developer and Google app signing.
* Enforces strict minimum SDK requirements.
* More details on target API level: Google Play API level requirements.
* https://nitter.net/GrapheneOS/status/1497272529223917575
* Strict minimum SDK (same Accrescent uses) - but do not remove apps that don't match target API level. Read here: [Target API level requirements for Google Play apps](https://support.google.com/googleplay/android-developer/answer/11926878)

4. Obtainium

* Direct download from repositories like GitHub, GitLab, and Codeberg and a few websites (e.g. MullvadVPN, Signal).
* UI and codebase are modern, written in Dart.
* Note: Some functionality is in development, and GitHub releases are not inherently secure for APK downloads.

5. APKs from GitHub Releases

* Provides a uniform infrastructure for developers and users.
* Allows signature verification, but the UI does not alert users to signature changes.

6. F-Droid and Its Derivatives

* Addresses some security concerns but leaves *a lot* to be desired…
* Recommended reading: [F-Droid Security Issues](https://privsec.dev/posts/android/f-droid-security-issues)
* [2023-09-03 F-Droid: Reproducible builds, signing keys, and binary repos](https://f-droid.org/en/2023/09/03/reproducible-builds-signing-keys-and-binary-repos.html)
* [2022-02-25 GrapheneOS: On Google Play Store and F-Droid](https://nitter.net/GrapheneOS/status/1497273173364166662)

7. Aurora Store

* Not secure or trustworthy.

Reasons, why you might want to use Aurora Store in the past:

* One would like to use "anonymously" one's apps such as WhatsApp and Netflix from the Google Play Store without logging in with a Google account.
* One does not want to or cannot use a Google Play Store.
* Security issue: The Google Play Store has special rights on one's own device and is not subject to the same App Sandbox as other apps are.

8. APKs from Official Websites

* Not recommended due to the lack of signature verification.
* Not user-friendly or secure.
* Might lack auto-updates.
* Android isn't Windows. Don't do it.