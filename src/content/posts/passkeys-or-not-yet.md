---
title: "Passkeys or Not Yet?"
description: "Finally sitting down and learning about passkeys to determine whether to switch to them"
date: "2025-09-01"
---

When services suggested I set up a passkey, I had been declining, because I didn't know how they worked under the hood. I don't want to add unncessary complexity to authentication when I've already gotten adept at using random password generators, password managers, and MFA.

But since enrolling in the [information security and privacy subject](https://handbook.unimelb.edu.au/2025/subjects/info30006) at university, I've had more exposure to them. A member in my group for an assignment is an extensive passkey user, and a guest lecturer mentioned that passkeys are not only more secure but also easier. So it seems like a good opportunity as ever to finally sit down and determine for myself, whether passkeys are something I want to switch to.

## How passykeys are more secure

A strong and unique password already goes a long way in preventing malicious takeover of accounts. Even if the threat can get past the password, MFA adds a layer of defense. The threat would need to have access to another thing that should only be obtainable by the target. This has been considered a gold standard approach. But of course there is no silver bullet. A password + MFA is still susceptible to phishing attacks. An example is detailed in [Troy Hunt's blog post](https://www.troyhunt.com/passkeys-for-normal-people/), where he showcases how he was compromised, even with MFA. The attackers obtained not only his username and password, but also the TOTP through a fake login website, and used it themselves to login to his account.

Passkeys are resilient to such phishing attacks.

When a user wants to register a new passkey for their account on an online platform, the credential manager (or security key) creates a public/private key pair. The private key is held by the credential manager and the public key is sent to be stored by the online platform. If a user wants to login using the passkey, the online platform sends a cryptographic challenge to the user's device, which is signed with the private key held by the credential manager. The user approves the login with the same method they use to unlock their device. This sounds like it's only as secure as a good password + MFA. But what makes passkeys resilient to phishing is that there is less room for human error. Because the credential manager requires an exact match with the domain that the passkey was registered with [^1].

An additional benefit to this cryptographic signing approach is that there is no shared secret to be stored. Password based authentication requires the platform to store the password hash. There are a lot of areas for error to occur, such as correct implementation of the hashing, appropriate data management, fending off against attacks, etc. But with passkeys only the public key is stored by the platform, and by cryptographic guarantees, it is (at least currently without quantum computers) impractical to derive the private key from just the public key.

But security isn't the only concern when deciding which method to use going forward. Aspects like convenience, ease of backup/recovery must also be considered.

## Backups (that are platform agnostic)

I like independence from platforms and companies. They come and go, and I don't want to rely on something as fragile as them for such a critical function.

My biggest concern with using passkeys was this. I got this impression that passkeys are strung to a single device and couldn't be backed up. But in fact there are [two types of passkeys](https://www.passkeycentral.org/introduction-to-passkeys/passkey-types): Device-bound passkeys and synced passkeys. Device-bound types are the ones that I was thinking of before, like a YubiKey. These are great for when the system is better off and more secure with a guarantee that there is only one device that could be used to sign in. Although that may be good for some use cases where the user and the service maintainers are able to meet in person in case of a lost device, it's not ideal for me. It's too scary carrying around a device that could be used to sign in to anything. Although I'm not the type to lose things, this is so crucial that I don't want to risk it.

But synced passkeys exist, and are able to be used to share passkeys across devices. My initial impression of this before researching wasn't great either, because I had been prompted multiple times on Apple devices to create a passkey and store it in iCloud. While I use Apple devices for now, I don't want my credentials to be stuck in their walled garden.

Thankfully, many credential managers have been implementing storage and syncing of passkeys. While I wouldn't be locked into a specific system OS, passkeys themselves aren't very transportable at the moment, as there isn't an agreed upon standard for storing/transporting them. The FIDO alliance has been working on a [specification](https://fidoalliance.org/fido-alliance-publishes-new-specifications-to-promote-user-choice-and-enhanced-ux-for-passkeys/) though, which is still in [draft stage](https://fidoalliance.org/specifications-credential-exchange-specifications/).

## Conclusion

I'm fairly convinced about what passkeys bring to the table now, and moving forward, will be using it as my preferred method of authentication. There are still some rough edges like no specification to transport passkeys across credential managers, or difference in implementation of passkeys as a method of authentication depending on the online platform. But hopefully, more adoption will lead to a positive feedback loop, of encouraging more users to use passkeys.

I've got my first passkey registered, and it's with GitHub:

![adding-a-passkey-to-github](./assets/adding-a-passkey-to-github.png)

![successful-confirmation-of-adding-a-passkey-on-github](./assets/successful-confirmation-of-adding-a-passkey-on-github.png)

---

## Footnotes

[^1]: <https://www.passkeycentral.org/introduction-to-passkeys/how-passkeys-work>, <https://www.passkeycentral.org/introduction-to-passkeys/passkey-security>
