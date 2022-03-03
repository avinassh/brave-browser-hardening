## Additional about:flags changes by [CHEF-KOCH](https://twitter.com/CKsTechNews) (CKTN) to harden [Brave Browser](https://brave.com/)

![Logo Banner - Credit: ledger.com](https://www.ledger.com/wp-content/uploads/2021/05/cover.png)

## [Project updates](#project-updates)

I'll try to keep this hardening guidance updated as much as I can. The below listed flags configuration/changes and tips are only tested against Windows/Linux & Android, I do not plan to test them against MacOS/iOS!

## [Introduction](#introduction)

*Hardening does not start at choosing the right tools or networks, hardening begins with gathering information to informing yourself, and others in order to stay up-to-date so that you can deal with current and upcomign threats. Tools, extensions and co. are just a workaround until someone build the right system, which starts by voting and supporting the right organisations.* – Statement CHEF-KOCH, 1997


The main purpose of this guidance is to inform people about possibilities to enhance Brave Browser without depending on other tools or the Brave Team or to rely on usually quickly outdated guides on the Internet.


In case you have some questions, you can ask them directly on my official [Matrix Server](https://matrix.to/#/#cktn:matrix.org).


[[_TOC_]]


## [Important notice: READ this before you start changing some random Browser flags!](#important-notice-read-this-before-you-start-changing-some-random-browser-flags)

Just because there are some flag who _promise_ X does not necessarily mean you should enable/change them, there are possible drawbacks!

- Browser flags are in general [beta](https://chromium.googlesource.com/chromium/src/+/HEAD/docs/flag_expiry.md) and can decrease performance/privacy or even corrupt your entire browser profile, however all mentioned flags here are carefully tested and reviewed before they are mentioned.
- In case you report some bugs in the official [Brave Browser GitHub repository](https://github.com/brave/brave-browser/issues) make sure that you use a fresh Browser profile, not any "optimized" one.
- Some flags (changes) depends on server-side related configuration and platform updates, which means that especially some security based flags only fully work when the server/domain actually supports them.
- Some flags are OS and platform specific, on older Android or Linux, Windows Builds or Versions they are probably listed under *Unavailable*, in this case you can, of course not use that flag on your platform.
- ~~[QUIC is disabled](https://arxiv.org/abs/2101.11871) due to [privacy](https://github.com/brave/brave-browser/issues/3855) and [fingerprinting concerns](https://eprint.iacr.org/2015/582.pdf)~~ - This concern is fixed with Brave 91.1.27.8 (nightly) and got original proposal got approved as [RFC 9000](https://www.fastly.com/blog/quic-is-now-rfc-9000).
- Use [KeePass](https://keepass.info/) (or a [fork](https://www.keepassdx.com/)) instead of the [internal password manager](https://www.tomsguide.com/news/dont-let-web-browsers-save-passwords). I personally prefer [not to work with Browser based password manager/integration](https://www.nirsoft.net/utils/chromepass.html). For more information, read [here](https://security.stackexchange.com/questions/170481/how-secure-is-chrome-storing-a-password).
- Voice (Android) search input is disabled due to multiple [privacy concerns](https://www.makeuseof.com/tag/stop-google-android-listening/).
- Browser based PDF is not changed because I prefer [Sumatra PDF](https://www.sumatrapdfreader.org/free-pdf-reader.html) (_aka offline reading_) due to multiple [privacy/malware concerns](https://arxiv.org/abs/2103.02707).
- Omnibox functionality is limited due to multiple [privacy concerns](https://www.cnet.com/news/eff-were-concerned-about-googles-omnibox/). See [here](http://blogoscoped.com/archive/2008-09-04-n10.html) for more info.
- Implications with [BrowserAudit.com](https://browseraudit.com/).
- Google's [Safe Browsing](https://safebrowsing.google.com/) and other security checks and connections are NOT wanted. The OS has its its own protection mechanism (OS security model + hardening).
- [FLoC is disabled](https://brave.com/why-brave-disables-floc/) by default in Brave. Chrome users can use uBlock or change it manually via [flags](https://twitter.com/CKsTechNews/status/1399422582588383242).
- How we [compare the network behavior of popular browsers on first-run](https://brave.com/popular-browsers-first-run/).
- All credential checks are disabled since we do not store passwords in Brave, instead we use KeePass or other password managers of your choice.

----------------------------------------------------------

## [Unresolved Issues with the biggest privacy/security impact](#unresolved-issues-with-the-biggest-privacysecurity-impact)

You find an overview of [all opened privacy related and reported issues directly on the issue tracker](https://github.com/brave/brave-browser/labels/privacy%2Ftracking). [x] indicates that mentioned issue was fully resolved.

- [Working with Flags and background info when they exire](https://chromium.googlesource.com/chromium/src/+/HEAD/docs/flag_expiry.md)
- [List of all Flags](https://source.chromium.org/chromium/chromium/src/+/main:chrome/browser/flag-metadata.json;l=1)
- [List of all Flags that never expire](https://source.chromium.org/chromium/chromium/src/+/main:/chrome/browser/flag-never-expire-list.json)


Please keep in mind that just because there are open issues tickets that this is not necessarily actively abused in the real-world. In lots of cases it is hard to find evidence that theoretically problems are used to directly compromise your security or privacy. Also some of the mentioned issues might be very hard to fix because trying to workaround them can results in unwanted side effects, such as Browser crashes, website breakages etc.


- [ ] Letterboxing ([window size](https://github.com/brave/brave-browser/issues/720))
- [ ] [Crooked Style Sheets Tracking Attacks](https://github.com/brave/brave-browser/issues/818)
- [ ] [Cross-device tracking via ultrasonics](https://github.com/brave/brave-browser/issues/823)
- [ ] [ETag - Block Tracking via etags and cached scripts](https://github.com/brave/brave-browser/issues/536), possible solution mentioned [here](https://github.com/brave/brave-browser/issues/10719). Test pages can be found [here](http://lucb1e.com/rp/cookielesscookies/) and [here](https://levelup.gitconnected.com/no-cookies-no-problem-using-etags-for-user-tracking-3e745544176b).
- [ ] [HSTS fingerprinting](https://github.com/brave/brave-browser/issues/5936), see [here](https://webkit.org/blog/8146/protecting-against-hsts-abuse/)
- [ ] [IPTC meta data in images](https://github.com/brave/brave-browser/issues/5238)
- [ ] [Resource Timing](https://github.com/brave/brave-browser/issues/5487)
- [ ] [TCP Fast Open (TFO)](https://github.com/brave/brave-browser/issues/6800)
- [ ] [TLS session resumption tracking](https://github.com/brave/brave-browser/issues/1852)
- [ ] [Trackability of QUIC connections](https://github.com/brave/brave-browser/issues/3855)
- [ ] [Tracking via Progressive Web Application Manifests](https://github.com/brave/brave-browser/issues/4237)
- [ ] [Zoom Levels tracking](https://github.com/brave/brave-browser/issues/541)
- [ ] [window.Intl.DateTimeFormat() API](https://github.com/brave/brave-browser/issues/8574)
- [ ] getSupportedExtensions in [WebGL](https://github.com/brave/brave-browser/issues/15904)
- [ ] [Intel iGPU sandboxing in Linux does not exists](https://github.com/brave/brave-browser/issues/19232), fixed with latest [Chromium commit](https://chromium.googlesource.com/chromium/src/+/c45894a002e2d04ccffbd60c568a247fddf60f0e)
- [ ] [DRAWN APART : A Device Identification Technique based on Remote GPU Fingerprinting](https://orenlab.sise.bgu.ac.il/p/DrawnApart), pretty much every Browser is affected by the new attack.
- [ ] [There is currently no master password available for saved passwords](https://github.com/brave/brave-browser/issues/13350), which can lead to security and privacy related issues.
- [x] Some [AV products using and inspecting your camera and your lockscreen](https://support.kaspersky.com/15408#cameras) - This is a wontfix because this is how AVs and their security features work. You manually need to allow Brave to use the camera permission or block/allow the AV to use/not it.


----------------------------------------------------------

## [Hardening is not a selling argument](#hardening-is-not-a-selling-argument)

The mass media and some privacy communities wrongfully echo chamber that hardening and applying best practices represent security and privacy, this is an unproven claim. The reason why this is unproven is the fact that the vast majority does not use hardened profiles on a daily bases. In other words there is no proof that this is enough, what it does is that it potentially reduced the attack surface but this is all. It does not mean you are untouchable or cannot be exploited. Even if you manage to harden everything you still need to take the human factor in consideration, social engineering works really well and can bypass every firewall, every OS or Browser hardening in a matter of time. The Browser acts like a gateway not meant to be a firewall to monitor every data package that goes trough.

I am entirely against selling privacy and security as product and the project goal here is not to fool people that hardening is something that is either one or zero. The factors for privacy and security are not products you install or scripts or tools you use. It is a relationship between developer and the community to deal with existent as well as new threats. Giving up control by depending on another unknown third-party who promises you xyz is not what I like to represent here because the overall goal is that mentioned issues getting shown to warn users that there are potential risks involved that you can address on a theoretical level, this means it should be shown in order to fix such problems, not to make profit out of it.

Claiming hardening makes you more secure because 0,1% of all users doing or using it is working with statistics. Statistics that are often flawed because depending on the data, point of view and experience, those can variate a lot. Assuming everything one day gets fixed, hackers still trying to bypass everything, break it or invent new techniques. This is a cat and mouse game without a winner because the web evolves as well as the Browser itself and hardening will always be a part of adapting those changes by workaround potential issues.

I am not a fan of mass advertising that hardening or to apply best practices is enough, what makes more sense is to make people aware of problems, provide some workarounds until it is fixed and then test it to verify if it is actually working as intended or not because even workarounds and fixes can cause additional problems or even new holes.

----------------------------------------------------------

## [Energy consumption is not a big priority](#energy-consumption-is-not-a-big-priority)

As much as I would love putting this point into a bigger consideration I need to clearly say that I cannot do much tests regarding energy consumption in general. Especially not with individual flags and then even do independent tests across multiple OS and Browser builds. This would require me to work and research on this subject in full-time.

There are lots of variables which can and will influence the energy aspect and this is a huge topic which I am not willingly to do on my own.

The only big focus regarding the overall energy consumption is when a flag dramatically decreases battery life or put extra pressure on the CPU and/or GPU that is directly debuggable trough internal tools.

----------------------------------------------------------


## [Enforced settings as new defaults](#enforced-settings-as-new-defaults)

We change mentioned default settings to [improve the default behavior in order to reduce possible risks](https://80daystartup.com/day-34/insecure-defaults-considered-harmful/). You can manually unlock stuff you need, which seems more work but it is worth it + you only have to do this once per domain. This basically acts like a firewall for specific things, which is then disabled by default and you need to manually unlock first (see last screenshot to understand what I mean).

![Shield Defaults](https://i.ibb.co/jD07Df0/Shield-defaults.png)

![Shield Defaults](https://i.ibb.co/vsQwMDt/4.png)

![Shield Defaults](https://i.ibb.co/Nsws654/Shields-Default.png)

![Permission Defaults](https://i.ibb.co/hMBJgpr/Permissions.png)

![Shield Defaults](https://i.ibb.co/sqPgLFj/More-control.png)


On mobile we can theoretically do the same but there are some downsides, as you can see on the last screenshot, if your screen resolution is below x or you are on a smartphone with limited screen size you cannot see all options, which makes it impossible for you to change or reveal some settings or information. Brave as well as Chrome is aware that this modal dialogue is currently not optimal. That said, I - for now - only suggest doing this on Desktop and on Mobile only enforce the stronger Shield defaults only see first (screenshot).

Brave will not sync those newly set permission defaults. Backup your profile manually, this is still the best way to deal with profile corruptions or in case you want to copy your settings to another profile or PC.

----------------------------------------------------------

## [Using JS-Restrictor with Brave](#using-js-restrictor-with-brave)

JavaScript Restrictor or [JShelter](https://polcak.github.io/jsrestrictor/) extension is normally not needed with Brave Browser, however you can  use it to fine control some specific settings if you want to. Changing those options can make you more unique and is the reason why this is not suggested unless you know exactly what you are dealing with.


JShelter uses, depending on your chosen profile, [twice as much CPU power](https://github.com/polcak/jsrestrictor/issues/151) than uBlock Origin or other solutions which you can check with the integrated Task Manager and internal debugging tools. This is the main reason why I not suggest using it on a daily basis. It is better to wait until Brave addresses all above listed privacy risks.


![Import the configuration file.](https://i.ibb.co/fDMMySB/JSRC.png)

Importing the configuration file is quickly done. Just import the configuration and click override. After that relead the website and check the configuration to ensure that settings are fully working. I includes some example pages for reference.

----------------------------------------------------------

## [Utilizing Brave Ad Block, the right-way](#utilizing-brave-ad-block-the-right-way)

The overall amount of trackers are limited. This means that the majority of websites uses Google - among some other - tracking systems. Most [popular and even unpopular websites trusting the big tracking players](https://arxiv.org/pdf/1810.09160.pdf), which means it makes no sense to load filter-lists with 2 trillion entries when 80 Percent of the world uses the same tracking system. You can skip this section if you already block ads via DNS blocker system-wide in your network with AdGuard Home or Pi-Hole and continue with the manual filter-lists we could use sub-section.


Finding some lists is pretty easy, you can manually search them or use some [aggregators who list filter-lists](https://filterlists.com/).


By default those [filters are already used and enabled by default](https://github.com/brave/adblock-resources/blob/master/filter_lists/default.json).
- Block Origin Filters
- Brave Android-Specific Rules
- Brave Social
- Brave Social Unbreak
- Brave Specific
- Brave Unbreak
- EasyList
- EasyPrivacy
- Peter Lowe's Ad and tracking server list
- SugarCoat Rules 
- URLhaus Malicious URL Blocklist
- uBlock Origin 2020 Filters
- uBlock Origin 2021 Filters
- uBlock Origin filters - Badware risks
- uBlock Origin filters - Unbreak
- uBlock Origin filters – Privacy
- uBlock Origin filters – Resource abuse


General rules
- By default without selecting, enabling or subscribing to third-party lists, Brave already blocks some stuff, if you are comfy enough with this, you can stop reading this section.
- Less is more, everything counts because everything that needs to be loaded ends-up in your RAM or causes the CPU to consume more CPU cycles which can end-up eating more energy and more battery. Good quality filter lists shouldn't have a perceptible effect on browsing performance. The first worry with too many filter lists is undue website breakage.
- Just because X filter-list has more entries does not mean it is more efficient.
- Only use lists which are regularity updated and well maintained.

The following steps are on Desktop and Mobile platforms the same, so I do not explicitly mention them.


Go to `brave://adblock/`, just type it in the URL bar and it will display the ad-block interface with some options. By default nothing is selected and you have to choose which filters you want to enable or even manually add. Custom filters are being updated every 7 days, which might change in the future. Syncing filter-lists and your custom rules are possible - the flag is `#brave-cosmetic-filtering-sync-load`, it will get removed in the future and directly integrated and enabled by default once it is reliable enough.


#### Additional lists you can enable from the integrated Brave Ad Block page

- `CJX's Annoyance List` alternative `Fanboy Annoyances List`
- `YousList`- To block various cosmetic stuff, aka annoyance in additional to above mentioned annoyances list. If you think this list is not enough use `Dandelion Sprout's Annoying Banners and Overlays List` instead.
- ONE single `language based` list, based for your own country.


Now we can improve specific things alias manually subscribing to addition lists, but which one make the most sense... The answer is easy, we want to get rid of additional extensions and hopefully we can archive it by using an additional list that supports the things we need, anti-coinmining, URL-shortener etc.

#### Optional filter-lists we could add

Additional filter-lists can be useful, for example to [get rid of ClearURLs extension](https://raw.githubusercontent.com/DandelionSprout/adfilt/master/ClearURLs%20for%20uBo/clear_urls_uboified.txt), or in case if we already block DNS based ads on our entire network, in this case we might wanna use something directly which only blocks cosmetic stuff. It should be noted that uBlock as well as Brave Ad Block solutions only removing the untouched query parameter given by the original URL, this means they cannot rewrite parts or the original path of clicked URL.

- AdGuard DNS filter - `https://filters.adtidy.org/windows/filters/15.txt`
- Actually Legitimate URL Shortener Tool - `https://raw.githubusercontent.com/DandelionSprout/adfilt/master/LegitimateURLShortener.txt`
- First-party trackers host list - `https://hostfiles.frogeye.fr/firstparty-only-trackers-hosts.txt` - You do not need it if you use DNS based network blocking.
- EU_US+most_used_ad_and_tracking_networks - `https://raw.githubusercontent.com/Kees1958/W3C_annual_most_used_survey_blocklist/master/EU_US%2Bmost_used_ad_and_tracking_networks`
- `Social Media Filters`, this is totally up to you.
- You `do not need any anti-coinminers`, it is normally covered by your language based list which you choose. Adding another one makes no sense because by default we block or optional restrict JavaScript anyway via extension.
- Block outside intruders breaking into LAN - `https://github.com/gwarser/filter-lists/blob/master/lan-block.txt` The list will become irrelevant at some point because Brave will at some point block all LAN requests by default starting with Chromium v101+. JS-Restrictor can do exactly the same, benefit in using the JS-Restrictor extension solution is that it is enabled by default and you can create with only two clicks exceptions for a domain.


This is all, you do not need 10+ lists. Well-maintained lists are much more worth than huge lists that die within the first 6-12 months.

----------------------------------------------------------

## [Why fingerprinting matters less than you think](#why-fingerprinting-matters-less-than-you-think)

Fingerprinting per-see is not an intrinsically problem, which means it only becomes a problem when it makes it possible to render you traceable, particularly across sessions. The main point is to become less traceable - or traceable only with adjustable levels of difficulty - whatever your "fingerpritability" could be.

And there are 2 ways to try to reach this goal
- The static way
- The dynamic way

In the static (or often called low entropy) way, the user or you can try to display the same fingerprint than many others people. In that sense, being seen as unique is bad. The best way to achieve this "low entropy" goal is to use the Tor Browser on the Tor network. No Brave hardening, no Firefox Browser hardening with thousands of configuration changes, simply and pure Tor Browser because it provides much more than configuration changes and the best way is that each and every user uses the exact same fingerprint.

In the dynamic (or high [entropy](https://en.wikipedia.org/wiki/Entropy)) way, you try to becomes "someone else" for each browser sessions, eg for each browsing session, you (ideally) try to change all your browser's displayed characteristics. In this case, being seen as unique is not a problem. At the contrary, it's something desirable: That a test site achieves to correlate you cross session, and so, achieves to see you as not unique, simply means that your attempts to becomes "someone else" for each session miserably failed and that you are traceable cross session (at least by this precise test site, and by any other site using the same tracking techniques). This way is the path that eg Brave developers are trying to take, this is also what you do if you harden other Browsers like Firefox, Edge etc.

In the real-world we have limited amount of possibilities to fingerprint users, this means most stuff heavily relies on JavaScript, CSS and so on. Developing counter-measures for this is possible, but since we enforce by default to disable JavaScript which already lower attacks by around 98%, the rest are some small tricks that abuses some weaknesses that are fixable more or less easily. There might be considerable small stuff which cannot be fixed but that never leads to leaks that can identify you, your browsing habits or connect other dots.

The most important stuff is listed above and is on the to-do regarding fingerprinting. None of the open issues are enough to truly expose you even if someone gets all of the remaining entropy that is currently not covered by Braves Shield. Most people just use the [fingerprinting argument to bypass restrictions](https://github.com/niespodd/browser-fingerprinting).

----------------------------------------------------------

## [Unofficial Brave Browser Build on F-Droid](#unofficial-brave-browser-build-on-f-droid)

Brave Browser is not yet listed in any official F-Droid repository or has its own because there are some leftovers in the repository as well as some other thing that need to be addressed by the Brave Team first. Another main argument is that the app uses Google Push.

![Alefvanoon's Repository QR-Code](https://repo.alefvanoon.xyz/img/qr.png)

However, there is an unofficial Repository - [Alefvanoon's Repository](https://repo.alefvanoon.xyz/fdroid/repo/?fingerprint=04DF198F553069C7BE60F057AE12000E99F7700DA895CC1CE2EB11DC871581F1) - which delivers Brave Browser with 2 Anti-Features, you can add the repository via QR-Code in F-Droid, Aurora Droid or enable the repository in the Droidify app.


Please keep in mind that [using F-Droid has its own downsides](https://wonderfall.dev/fdroid-issues/).


----------------------------------------------------------

## [Do not use portable Browsers](#do-not-use-portable-browsers)

Using portable Browsers has lots of security and privacy implications.

- In most cases the official Browser developer does not provide any officially build, because of that people tend to use unofficial portable Browser repacks. Not often those repacks are done by fans and not experts and can possible contain tracking ads, Trojans, IP-grabbers etc.
- There is no verification, since you use unofficial Browser repacked versions you cannot verify anything yourself. Even if you use some repacks that are open source, you cannot verify something because the installer or the browser itself might be signed with different signatures that does not match the ones from the original manufacturer.
- No support, unofficial repack versions might not be approved nor directly supported from official site. This means they can be outdated after a short while, you already download an outdated version or the integrated update mechanism will fail because the updater depends on a service who check and delivers the actual update. Epic, MS etc Store will also not updating any portable versions.
- Running your Browser and profile on an unprotected drive that everyone can freely access is a privacy and security nightmare. There exist tools to quickly read out your Cookies, [passwords](https://www.nirsoft.net/utils/chromepass.html) and more, usually those tool need admin rights to access protected folders but if the profile folder is unprotected you can even read our or steal the database or the entire profile without admin rights. The internal protection regarding database passwords is weak and easy to crack in seconds, the Browser typically has no master password for the database as well as a Browser startup password check.
- You can workaround some of mentioned problems with a RamDrive or third-party Sandbox but the underlying issue is that it is overall by default easier for an attacker to extract, infect or compromise your Browser profile. Keep in mind that sandboxing trough external third-party apps can also be critical because the sandbox tool can be vulnerable or causes the Browser to crash because the Browser typically updates much more frequently that the sandbox tool needs to address. Another problem is that such workarounds might also require that such software is installed on the host, which needs admin rights. I am not aware of a sandbox solution that protects at low-level without admin rights, because this is what the OS requests to access inner rings.

----------------------------------------------------------

## [How does Brave Browser handle Cookies](#how-does-brave-browser-handle-cookies)

Brave Browser is very well documented. Besides the source code and the wiki entries we have several good articles for beginners on how Brave actually handles the Cookie part.

- [Ephemeral Storage](https://brave.com/privacy-updates/7-ephemeral-storage/) + [Test](https://dev-pages.brave.software/storage/ephemeral-storage.html). This is the quinquevalent to Firefox [Dynamic First-Party Isolation](https://bugzilla.mozilla.org/show_bug.cgi?id=1625228) (dFPI) and [Total Cookie Protection](https://blog.mozilla.org/security/2021/02/23/total-cookie-protection/) mechanism.
- [Insight about how cookies are handled](https://github.com/brave/brave-browser/issues/16310#issuecomment-867269617)


----------------------------------------------------------


## [Desktop Flags](#Desktop-Flags)

The official Brave release schedule can be found over [here](https://github.com/brave/brave-browser/wiki/Brave-Release-Schedule), the [archive is here](https://github.com/brave/brave-browser/wiki/Brave-Release-Schedule-Archive). There is currently no plan to release a Brave Browser version for SmartTV.


### [Desktop Security](#desktop-security)
Flag | Name | Enabled (✔️) / Disabled (❌) or/and comment
-- | -- | --
[#u2f-security-key-api](chrome://flags/#u2f-security-key-api) | Enable the U2F Security Key API | ❌
[#enable-tls13-early-data](chrome://flags/#enable-tls13-early-data) | TLS 1.3 Early Data | ✔️
[#sync-trusted-vault-passphrase-recovery](chrome://flags/#sync-trusted-vault-passphrase-recovery) | Enable sync trusted vault passphrase with improved recovery. | ❌
[#brave-ephemeral-storage](chrome://flags/#brave-ephemeral-storage) | Enable Ephemeral Storage | ✔️
[#brave-vpn](chrome://flags/#brave-vpn) | Enable experimental Brave VPN (1.30.27+), the flag got removed but it will return | ✔️
[#strict-extension-isolation](chrome://flags/#strict-extension-isolation) | Strict Extension Isolation | ✔️
[#block-insecure-private-network-requests](chrome://flags/#block-insecure-private-network-requests) | Block insecure private network requests |  ✔️
[#strict-origin-isolation](chrome://flags/#strict-origin-isolation) | Strict-Origin-Isolation | ❌
[#disallow-doc-written-script-loads](chrome://flags/#disallow-doc-written-script-loads) | Block scripts loaded via document.write |  ✔️
[#post-quantum-cecpq2](chrome://flags/#post-quantum-cecpq2) | TLS Post-Quantum Confidentiality |  ✔️
[#brave-domain-block](chrome://flags/#brave-domain-block) | Enable domain blocking | ✔️

[🔝 Back to top 🔝](#)


### [Desktop Privacy](#desktop-privacy)
Flag | Name | Enabled (✔️) / Disabled (❌) or/and comment
-- | -- | --
[#extensions-menu-access-control](chrome://flags/#extensions-menu-access-control) | Extensions Menu Access Control | ✔️
[#force-major-version-to-100](chrome://flags/#force-major-version-to-100) | [#force-major-version-to-100](https://blog.chromium.org/2021/10/chrome-96-beta-conditional-focus.html) | ❌
[#enable-fenced-frames](chrome://flags/#enable-fenced-frames) | Enable the <fencedframe> element. | ✔️ with ShadowDOM
[#reduce-user-agent](chrome://flags/#reduce-user-agent) | Reduce User-Agent request header | ✔️
[#brave-debounce](chrome://flags/#brave-debounce) | Enable debouncing (94.x+) | ✔️
[#privacy-review](chrome://flags/#privacy-review) | Privacy Review (93.1.31.39+) | ✔️
[#enable-lens-region-search](chrome://flags/#enable-lens-region-search) | Search your screen with Google Lens (93.1.31.39+) | ❌
[#webxr-incubations](chrome://flags/#webxr-incubations) | WebXR Incubations | ❌ (92.0+)
[#enable-quic](chrome://flags/#enable-quic) | Experimental QUIC protocol | ✔️ Needed for HTTP3/DoQ, now known as [RFC 9000](https://www.fastly.com/blog/quic-is-now-rfc-9000)
[#omnibox-pedals-batch2](chrome://flags/#omnibox-pedals-batch2) | Omnibox Pedals batch 2 | ❌
[#omnibox-rich-autocompletion-promisin](chrome://flags/#omnibox-rich-autocompletion-promisin) | Omnibox Rich Autocompletion Promising | ❌
[#omnibox-dynamic-max-autocomplete](chrome://flags/#omnibox-dynamic-max-autocomplete) | Omnibox Dynamic Max Autocomplete | ❌ (_causes lags if enabled / 5+_)
[#brave-extension-network-blocking](chrome://flags/#brave-extension-network-blocking) | Enable extension network blocking | ✔️ (91+)
[#enable-accessibility-live-caption](chrome://flags/#enable-accessibility-live-caption) | Live Caption |❌ (90.x+) ⚠️[borked](https://github.com/brave/brave-browser/issues/15640)
[#system-keyboard-lock](chrome://flags/#system-keyboard-lock) | Experimental system keyboard lock | ❌ (89.x+)
[#enable-autofill-credit-card-authentication](chrome://flags/#enable-autofill-credit-card-authentication) | Allow using platform authenticators to retrieve server cards | ❌ (87.x+)

[🔝 Back to top 🔝](#)


### [Desktop Performance](#desktop-performance)

Benchmarks against Edge and Firefox are useless. There are multiple reasons why, see below:
- Synthetic benchmarks might not reflect real-world performance because a normal website is not a benchmark suite, other factors can here the individual and subjective Browser performance.
- Brave’s blocking and privacy protections require a fixed amount of additional work per page and frame. This means that Brave will do worse in synthetic benchmarks than other browsers (since Brave’s privacy protections won’t be useful in benchmark tests), but will do better on real world sites.
- Firefox and Edge do not have any integrated ad-blocker, they use safe-browsing, which is also included in all Chromium based Browsers and enabled by default.
- Firefox and Edge do not include any crypto wallets.
- [Brave reduces the page load performance cost of its ad-blocker](https://www.ctrl.blog/entry/brave-ab-performance.html).
- [Benchmarks, are often outdated pretty fast](https://old.reddit.com/r/Android/comments/kxg8gh/android_browser_benchmark_tests/). At best this is a snapshot of the current state but every Browser evolves, fixes stuff etc.


Flag | Name | Enabled (✔️) / Disabled (❌) or/and comment
-- | -- | --
[#brave-adblock-cookie-list-default](chrome://flags/#brave-adblock-cookie-list-default) | Treat 'Easylist-Cookie List' as a default list source | ✔️
[#enable-parallel-downloading](chrome://flags/#enable-parallel-downloading) | Parallel downloading | ✔️
[#enable-prerender2](chrome://flags/#enable-prerender2) | Prerender2 | ✔️ (90.x+)
[#brave-rewards-verbose-logging](chrome://flags/#brave-rewards-verbose-logging) | Enable Brave Rewards verbose logging | ❌ enabled by default since 1.25.68+

[🔝 Back to top 🔝](#)


### [Desktop Functionality / Usability](#desktop-functionality--usability)
Flag | Name | Enabled (✔️) / Disabled (❌) or/and comment
-- | -- | --
[#brave-cosmetic-filtering-sync-load)](chrome://flags/#brave-cosmetic-filtering-sync-load) | Enable sync loading of cosmetic filter rules | ✔️
[#media-session-webrtc](chrome://flags/#media-session-webrtc) | Enable WebRTC actions in Media Session (93.x+) | ✔️
[#extension-workflow-justification](chrome://flags/#extension-workflow-justification) | Extension request justification (93.x+) | ✔️
[#omnibox-keyword-space-triggering-setting](chrome://flags/#omnibox-keyword-space-triggering-setting) | Omnibox Keyword Space Triggering Setting | ✔️
[#playback-speed-button](chrome://flags/#playback-speed-button) | Playback Speed Button | ✔️
[#chrome-whats-new-ui](chrome://flags/#chrome-whats-new-ui) | Show Chrome What's New page at `chrome://whats-new` (93.x+) | ❌
[#scrollable-tabstrip](chrome://flags/#scrollable-tabstrip) | Tab Scrolling | ✔️ (tabs shrink to a medium width)
[#brave-talk](chrome://flags/#brave-talk) | Enable Brave Talk | ✔️
[#colr-v1-fonts](chrome://flags/#colr-v1-fonts) | COLR v1 Fonts | ✔️
[#enable-force-dark](chrome://flags/#enable-force-dark) | Force Dark Mode for Web Contents | ✔️ `increase text contrast`
[#force-color-profile](chrome://flags/#force-color-profile) | Force color profile | ✔️[scRBG](https://en.wikipedia.org/wiki/ScRGB) or [HDR](https://en.wikipedia.org/wiki/High_Dynamic_Range_(display_and_formats)#Description) (if your Monitor supports HDR enable the HDR option)
[#forced-colors](chrome://flags/#forced-colors) | Forced Colors | ✔️
[#enable-jxl](chrome://flags/#enable-jxl) | Enable [JXL image format ](https://jpeg.org/jpegxl/) | ✔️ (Chrome 91.1.x+)
[#shared-highlighting-v2](chrome://flags/#shared-highlighting-v2) | Shared Highlighting 2.0 | ✔️ (Chrome 90.x+)
[#sharing-hub-desktop-app-menu](chrome://flags/#sharing-hub-desktop-app-menu) | Desktop Sharing Hub in App Menu | ✔️ (Chrome 91+)
[#sharing-hub-desktop-omnibox](chrome://flags/#sharing-hub-desktop-omnibox) | Desktop Sharing Hub in Omnibox | ✔️ (Chrome 91+)
[#brave-adblock-cname-uncloaking](chrome://flags/#brave-adblock-cname-uncloaking) | Enable CNAME uncloaking | ✔️ 91.1.27.36 (This will become obsolete and enabled by default once fully stable and merged into shields directly)

[🔝 Back to top 🔝](#)


### [Desktop Scrolling](#desktop-scrolling)
Flag | Name | Enabled (✔️) / Disabled (❌) or/and comment
-- | -- | --
[#smooth-scrolling](chrome://flags/#smooth-scrolling) | Smooth Scrolling | ✔️
[#percent-based-scrolling](chrome://flags/#percent-based-scrolling) | Percent-based Scrolling | ✔️

[🔝 Back to top 🔝](#)


### [Desktop PWA](#desktop-pwa)
Flag | Name | Enabled (✔️) / Disabled (❌) or/and comment
-- | -- | --
[#enable-desktop-pwas-prefix-app-name-in-window-title](chrome://flags/#enable-desktop-pwas-prefix-app-name-in-window-title) | Desktop PWAs prefix window title with app name. | ✔️
[#enable-desktop-pwas-remove-status-bar](chrome://flags/#impulse-scroll-animations) | Desktop PWAs remove status bar | ✔️
[#enable-desktop-pwas-elided-extensions-menu](chrome://flags/#enable-desktop-pwas-elided-extensions-menu) | Desktop PWAs elided extensions menu | ✔️
[#enable-desktop-pwas-notification-icon-and-title](chrome://flags/#enable-desktop-pwas-notification-icon-and-title) | Desktop PWAs improvements in notification icon and title | ✔️
[#enable-desktop-pwas-tab-strip-settings](chrome://flags/#enable-desktop-pwas-tab-strip-settings) | Desktop PWA tab strips settings | ✔️
[#enable-desktop-pwas-launch-handler](chrome://flags/#enable-desktop-pwas-launch-handler) | Desktop PWA launch handler | ✔️
[#enable-desktop-pwas-sub-apps](chrome://flags/#enable-desktop-pwas-sub-apps) | Desktop PWA Sub Apps | ✔️
[#enable-desktop-pwas-window-controls-overlay](chrome://flags/#enable-desktop-pwas-window-controls-overlay) | Desktop PWA Window Controls Overlay | ✔️
[#enable-desktop-pwas-web-bundles](chrome://flags/#enable-desktop-pwas-web-bundles) | Desktop PWAs Web Bundles | ✔️
[#pwa-update-dialog-for-name-and-icon](chrome://flags/#pwa-update-dialog-for-name-and-icon) | Enable PWA install update dialog for name/icon changes | ✔️

[🔝 Back to top 🔝](#)


### [Desktop Brave Reader Mode / Speedreader](#desktop-brave-reader-mode--speedreader)
Flag | Name | Enabled (✔️) / Disabled (❌) or/and comment
-- | -- | --
[#enable-reader-mode](chrome://flags/#enable-reader-mode) | Enable Reader Mode |✔️(_we enforce it_, optional)

[🔝 Back to top 🔝](#)

--------------------

## [Android (mobile) Flags](#android-mobile-flags)

### [Mobile Security](#mobile-security)
Flag | Name | Enabled (✔️) / Disabled (❌) or/and comment
-- | -- | --
[#sync-trusted-vault-passphrase-recovery](chrome://flags/#sync-trusted-vault-passphrase-recovery) | Enable sync trusted vault passphrase with improved recovery | ❌
[#brave-ephemeral-storage](chrome://flags/#brave-ephemeral-storage) | Enable Ephemeral Storage | ✔️
[#brave-vpn](chrome://flags/#brave-vpn) | Enable experimental Brave VPN (1.30.27+), the flag got removed but it will return | ✔️
[#block-insecure-private-network-requestst](chrome://flags/#block-insecure-private-network-requestst) | N/A | ✔️
[#enable-site-isolation-for-password-sites](chrome://flags/#enable-site-isolation-for-password-sites) | N/A | ✔️
[enable-site-per-process](chrome://flags/#enable-site-per-process) | N/A | ✔️
[#post-quantum-cecpq2](chrome://flags/#post-quantum-cecpq2) | N/A | ✔️
[#strict-origin-isolation](chrome://flags/#strict-origin-isolation) | N/A | ❌
[#disallow-doc-written-script-loads](chrome://flags/#disallow-doc-written-script-loads) | Block scripts loaded via document.write |  ✔️

[🔝 Back to top 🔝](#)


### [Mobile Privacy](#mobile-privacy)
Flag | Name | Enabled (✔️) / Disabled (❌) or/and comment
-- | -- | --
[#force-major-version-to-100](chrome://flags/#force-major-version-to-100) | [#force-major-version-to-100](https://blog.chromium.org/2021/10/chrome-96-beta-conditional-focus.html) | ❌
[#enable-fenced-frames](chrome://flags/#enable-fenced-frames) | Enable the <fencedframe> element. | ✔️ with ShadowDOM, on older Android versions prior 9 set this to Enabled otherwise you get Browser crashes.
[#reduce-user-agent](chrome://flags/#reduce-user-agent) | Reduce User-Agent request header | ✔️
[#brave-debounce](chrome://flags/#brave-debounce) | Enable debouncing (94.x+) | ✔️
[#webxr-incubations](chrome://flags/#webxr-incubations) | WebXR Incubations | ❌ (92.0+)
[#continuous-search](chrome://flags/#continuous-search) | Continues Search | ❌
[#enable-quic](chrome://flags/#enable-quic) | Enable QUIC Protocol | ✔️(Brave filters controversial APIs)
[#incognito-screenshot](chrome://flags/#incognito-screenshot) | Allow Incognito Screenshots | ❌
[#omnibox-assistant-voice-search](chrome://flags/#omnibox-assistant-voice-search) | Omnibox Voice Search Assistant | ❌
[#wallet-service-use-sandbox](chrome://flags/#wallet-service-use-sandbox) | Wallet Services uses Google's Sandbox | ❌Connects to some Google Endpoints.
[#enable-autofill-credit-card-authentication](chrome://flags/#enable-autofill-credit-card-authentication) | Allow using platform authenticators to retrieve server cards | ❌ (87.x+)

[🔝 Back to top 🔝](#)


### [Mobile PWA](mobile-pwa)
Flag | Name | Enabled (✔️) / Disabled (❌) or/and comment
-- | -- | --
[#pwa-update-dialog-for-name-and-icon](chrome://flags/#pwa-update-dialog-for-name-and-icon) | Enable PWA install update dialog for name/icon changes | ✔️

[🔝 Back to top 🔝](#)


### [Mobile Performance](#mobile-performance)
Flag | Name | Enabled (✔️) / Disabled (❌) or/and comment
-- | -- | --
[#brave-adblock-cookie-list-default](chrome://flags/#brave-adblock-cookie-list-default) | Treat 'Easylist-Cookie List' as a default list source | ✔️
[#enable-instant-start](chrome://flags/#enable-instant-start) | Instant start | ✔️
[#back-forward-cache](chrome://flags/#back-forward-cache) | Back and forward Cache | ✔️
[#contextual-search-debug](chrome://flags/#contextual-search-debug) | Contextual Search Debug | ❌
[#chrome-share-long-screenshot](chrome://flags/#chrome-share-long-screenshot) | N/A | ❌
[#contextual-search-longpress-resolve](chrome://flags/#contextual-search-longpress-resolve) | N/A | ❌
[#contextual-search-translation](chrome://flags/#contextual-search-translation) | N/A | ❌
[#enable-parallel-downloading](chrome://flags/#enable-parallel-downloading) | Parallel downloading | ✔️
[#smooth-scrolling](chrome://flags/#smooth-scrolling) | Smooth Scrolling | ✔️
[#video-tutorials](chrome://flags/#video-tutorials) | N/A | ❌
[#enable-prerender2](chrome://flags/#enable-prerender2) | Prerender2 | ✔️ (90.x+)

[🔝 Back to top 🔝](#)


### [Mobile Functionality / Usability](#mobile-functionality--usability)
Flag | Name | Enabled (✔️) / Disabled (❌) or/and comment
-- | -- | --
[#brave-cosmetic-filtering-sync-load)](chrome://flags/#brave-cosmetic-filtering-sync-load) | Enable sync loading of cosmetic filter rules | ✔️
[#media-session-webrtc](chrome://flags/#media-session-webrtc) | Enable WebRTC actions in Media Session (93.x+) | ✔️
[#playback-speed-button](chrome://flags/#playback-speed-button) | Playback Speed Button | ✔️
[#enable-quick-action-search-widget-android](chrome://flags/#enable-quick-action-search-widget-android) | [Quick Search Widget](https://www.androidpolice.com/2021/06/29/chrome-for-android-is-rediscovering-widgets-now-that-apple-made-them-hot-again/) | ✔️
[#continuous-search](chrome://flags/#continuous-search) | Continuous Search | ✔️
[#enable-force-dark](chrome://flags/#enable-force-dark) | Force Dark Mode for Web Contents | ✔️ `increase text contrast`
[#darken-websites-checkbox-in-themes-setting](chrome://flags/#darken-websites-checkbox-in-themes-setting) | Darken Websites checkbox in Theme settings | ✔️
[#voice.button-in-top-toolbar](chrome://flags/#voice.button-in-top-toolbar) | Voice Button in Top Toolbar | ❌
[#enable-jxl](chrome://flags/#enable-jxl) | Enable [JXL image format ](https://jpeg.org/jpegxl/) | ✔️ (Chrome 91.1.x+)
[#shared-highlighting-v2](chrome://flags/#shared-highlighting-v2) | Shared Highlighting 2.0 | ✔️ (Chrome 90.x+)
[#brave-adblock-cname-uncloaking](chrome://flags/#brave-adblock-cname-uncloaking) | Enable CNAME uncloaking | ✔️ 91.1.27.36 (This will become obsolete and enabled by default once fully stable and merged into shields directly)

[🔝 Back to top 🔝](#)


### [Brave only specific flags (not needed to be enforced)](#brave-only-specific-flags-not-needed-to-be-enforced)
Flag | Name | Info comment
-- | -- | --
[#brave-news](chrome://flags/#brave-news) | Enable Brave News | Your own decision to enable it or not, it is a global switch.
[#brave-ads-allowed-to-fallback-to-custom-push-notification-ads](chrome://flags/#brave-ads-allowed-to-fallback-to-custom-push-notification-ads) | Allow Brave Ads to fallback from native to custom push notifications | This is OS specific and in the future will be obsolete since Brave will detect the OS and then automatically fallback to the legacy system.
[#brave-adblock-cosmetic-filtering](chrome://flags/#brave-adblock-cosmetic-filtering) | Enable cosmetic filtering | Enabled by default even if it only shows "default"
[#brave-adblock-cosmetic-filtering-native](chrome://flags/#brave-adblock-cosmetic-filtering-native) | Use native implementation for cosmetic filtering | Enabled by default even if it only shows "default"
[#brave-adblock-csp-rules](chrome://flags/#brave-adblock-csp-rules) | Enable support for CSP rules | Not need to be enforced (since 1.25.68+)
[#enable-webrtc-hide-local-ips-with-mdns](chrome://flags/#enable-webrtc-hide-local-ips-with-mdns) | This is not Brave only specific but there are two ways how Brave handles it, [via Shields or Setting](https://avoidthehack.com/webrtc-leaks-how-to-fix) | Do not enforce it via flag
[#brave-decentralized-dns](chrome://flags/#brave-decentralized-dns) | Enable Decentralized DNS | ✔️ This is now a settings point under Browser Settings since v95+ which you can easily switch.
[#brave-speedreader](chrome://flags/#brave-speedreader) | Enable SpeedReader | ✔️ This is now a settings point under Browser Settings since v95+ which you can easily switch.

[🔝 Back to top 🔝](#)


### [Other Useful Brave Browser Tips](#other-useful-brave-browser-tips)
- [Add shortcuts to instantly use a website's search bar directly from Brave's search bar, e.g. youtube, amazon, etc.](https://old.reddit.com/r/brave_browser/comments/r7pnlk/psa_you_can_add_shortcuts_to_instantly_use_a/)
- **DO NOT** use nightly builds. The logic to use nightly builds to get "things first" is flawed. Often you run into MORE fingerprinting due to bugs and not reviewed stuff than using stable builds. Critical vulnerabilities getting fixed immediately in stable builds anyway.
- Brave is well [documented](https://support.brave.com/hc/en-us) and their [Wiki](https://github.com/brave/brave-browser/wiki) helps a lot.
- ~~Export / import Chrome flags (mobile/desktop) via script, see [here](https://gist.github.com/kkeybbs/d817fad016b401485ab8c4c8fcffe568).~~
- Go to `brave://adblock` (URI also works in Mobile!) and enable following Filters only to maintain the best filtering performance: `CJX's Annoyance List`, `Easylist-Cookie List - Filter Obtrusive Cookie Notices`, `Fanboy Annoyances List`, `Fanboy Social List` (_optional_), `uBlock Annoyances List (used with Fanboy Annoyances List)` + **one OPTIONAL** language based Easylist (depends on your Region). __DO NOT__ enable more filters, more is not (always) better.
- Starting with Chrome 90/91+ [Sandboxie Technologies](https://github.com/sandboxie-plus/Sandboxie) (SBIE Open source) has some issues with Chrome/Chromium/Brave, I do not suggest using it. If you want another isolation layer use a [RAM Disk](https://www.raymond.cc/blog/12-ram-disk-software-benchmarked-for-fastest-read-and-write-speed/) and outsource entirely all temp data into that drive. It has a much better performance than Sandboxie.
- You still can [change the User-Agent on mobile with root](https://newbedev.com/how-to-make-google-chrome-definitely-remain-as-the-desktop-version), it is not advised to change the UA because [Brave addressed all UA based concerns](https://github.com/brave/brave-browser/issues/9190).
- [How-To start Brave in Incognito Mode](https://github.com/brave/brave-browser/issues/2105), see also here for a [more in-depth guidance](https://techpp.com/2020/02/07/always-launch-google-chrome-incognito-mode/).
- You can start Brave directly in _Tor Mode_ via `onion` e.g. `"C:\Program Files\BraveSoftware\Brave-Browser\Application\brave.exe" onion`, further modes and implementation is been discussed over [here](https://github.com/brave/brave-browser/issues/2105).
- If Brave Browser blocks your download turn off "Safe Browsing" in the settings. There is also a secret cheat code built into these warnings like "This is not a safe connection" etc. if you type in using your keyboard `thisisunsafe` in all lower case, you can [bypass any security warningst](https://cybercafe.dev/thisisunsafe-bypassing-chrome-security-warnings/).
- "Zero-copy rasterizer" and "Disable site isolation" shall be never touched, they causing crashes.
- Some useful start parameters are `--silent-launch`, `--tor` and `--incognito`, those [cmdline params](https://kapeli.com/cheat_sheets/Chromium_Command_Line_Switches.docset/Contents/Resources/Documents/index) work since 1.29.48 (or higher).

[🔝 Back to top 🔝](#)


### [Linux specific Tips](#linux-specific-tips)

You can create a file called `chrome-flags.conf` and put it into `$HOME/.config/chrome-flags.conf`, this makes it easier to work with flags without opening the Browser.

Example `chrome-flags.conf` below:

```sh
-use-vulkan
--disable-features=UseChromeOSDirectVideoDecoder
--disable-gpu-driver-bug-workarounds
--enable-accelerated-2d-canvas
--enable-accelerated-video-decode 
--enable-features=VaapiVideoDecoder
--enable-gpu-rasterization
--enable-oop-rasterization
--enable-zero-copy
--ignore-gpu-blocklist
# Borked until Chrome 96
#  https://chromiumdash.appspot.com/commit/a4de986102a45e29c3ef596f22704bdca244c26c
# ... and Chrome 98 
# https://bugs.chromium.org/p/chromium/issues/detail?id=1236697
#
# Up to you and your preference and device.
# --gpu-testing-vendor-id=0x8086 
# --gpu-testing-device-id=0x5917
# --force-device-scale-factor=1.00
# --enable-features=WebUIDarkMode
# --force-dark-mode
```

- You can enforce the usage of [vaapi](https://github.com/brave/brave-browser/issues/1024) by default via `brave --enable-oop-rasterization --enable-accelerated-video-decode`.
- To enforce [Wayland](https://github.com/brave/brave-browser/issues/6212) support (Chromium 87+) you can use `brave --enable-features=UseOzonePlatform --ozone-platform=wayland`.
- [SIGSEGV & SIGTRAP error codes in Brave](https://bbs.archlinux.org/viewtopic.php?pid=1950852#p1950852)
- No video hardware acceleration available on some pages: Some videos on e.g. YouTube are encoded using AV1 and Brave will use dav1d software decoder for that. But for ones encoded differently, Brave will indeed uses GPU for it if you enabled `--enable-features=VaapiVideoDecoder on`.
- `Override software rendering list` flag can be used to enforce that your GPU will be used (which might be blacklisted otherwise).
- `Enable Mojo Shared Memory Channel` flag can be used to share messages from GPU buffer, which might increase performance a bit.
- On Ubuntu based Distros I personally use the following combination for passthrough  `--ignore-gpu-blocklist`, `--enable-gpu-rasterization`, `--enable-zero-copy`, `--disable-gpu-driver-bug-workarounds` and `--use-gl=desktop`. Keep in mind that rasterization and zero-copy are highly unstable (depends on the OS/distro).
- [Font rendering can be a PITA](https://lonesysadmin.net/2011/09/12/how-to-fix-google-chrome-font-rendering-issues/), Settings --> Advanced --> System --> Hardware Acceleration is your first starter here.
- `#enable-gpu-rasterization` + `#enable-zero-copy` + `#canvas-oop-rasterization` combined can boost the performance on Linux by solid 10 percent, do not enable those flags on other platforms.


[🔝 Back to top 🔝](#)


### [Default Fonts](#default-fonts)
By default Brave Browser uses Poppins and Muli for the content you see around the web, those mentioned fonts are not the default fonts to render the actual content.

The [actual fonts](https://brave.com/brave-branding-assets/) are
- Standard font: Liberation Serif / Times New Roman 16
- Serif font: Liberation Serif / Times New Roman 16
- Liberation Serif Sans-serif font: Liberation / Arial 16
- Sans Fixed-width font: Monospace / Consolas 13

Keep in mind that the list can be different because some Distros do not include mentioned fonts by default. In this case other fonts are the default ones. Font rendering and issues are actually a [thing](https://github.com/brave/brave-browser/issues/5032).

My own suggestion is
- Poppin 16
- Poppin 16
- Open Sans 16
- Muli 12
- Set the minimum font size to 6 and not 0 which is a borked default.

There is currently no way to disable font anti-aliasing/font smoothing.

[🔝 Back to top 🔝](#)


### [Browser Extensions](#browser-extensions)
In general less is more, which means less memory + attack surface & in terms of fingerprinting.

Extension | comment
-- | --
[Behave!](https://github.com/mindedsecurity/behave) | Monitors and warns if a web page performs DNS Rebinding attacks to Private IPs, accesses Private IPs and allows Port Scans (among other features).
[Bypass Paywalls](https://github.com/iamadamdev/bypass-paywalls-chrome) alternative [Bypass Paywalls for Chrome Clean](https://gitlab.com/magnolia1234/bypass-paywalls-chrome-clean) | Bypass annoying article [PayWalls](https://en.wikipedia.org/wiki/Paywall).
[CSS Exfil Protection](https://github.com/mlgualtieri/CSS-Exfil-Protection) | Guard your browser against CSS Exfil attacks (_will be obsolete with Chrome 98+!_).
[Demodal](https://github.com/AliasIO/demodal) | A browser extension that blocks modals and overlays. It can be used in additional to uBlock or Braves Ad-Block to bypass eg. Paywalls and other modals which are hard to block via uBO or heavily rely on static filterlists.
[Extension source viewer](https://chrome.google.com/webstore/detail/chrome-extension-source-v/jifpbeccnghkjeaalbbjmodiffmgedin) | View source code of Chrome extensions, Firefox addons or Opera extensions (crx/nex/xpi) from the Chrome web store and elsewhere.
[JShelter alias JS-Restrictor](https://polcak.github.io/jsrestrictor/) | Extension for increasing security and privacy level of the user.
[Keyboard Privacy](https://chrome.google.com/webstore/detail/keyboard-privacy/aoeboeflhhnobfjkafamelopfeojdohk?hl=en&ucbcb=1) | Prevents behavioral profiling by randomizing the rate at which characters reach the DOM (_will be obsolete with Chrome 92+!_).
[Old Reddit Redirect](https://chrome.google.com/webstore/detail/old-reddit-redirect/dneaehbmnbhcippjikoajpoabadpodje) | Alternative via [script](https://greasyfork.org/en/scripts/377047-old-reddit-redirect/code), I prefer the script! Or you use Redirector 👇.
[Redirector](https://einaregilsson.com/redirector/) | The add-on lets you create redirects for specific webpages, e.g. always redirect http://bing.com to http://startpage.com
[Session Buddy](https://chrome.google.com/webstore/detail/session-buddy/edacconmaakjimmfgnblocblbcdcpbko) | Manage Browser Tabs and Bookmarks easily.
[Tabs Session Manager](https://github.com/sienori/Tab-Session-Manager) | WebExtensions for restoring and saving window / tab states.
[Terms of Service; Didn’t Read](https://tosdr.org/) | Ranks website terms & privacy policies from very good Class A to very bad Class E.
[uBlacklist](https://github.com/iorate/uBlacklist) | Blocks specific sites from appearing in Google search results.
[zwBlocker](https://github.com/aido179/zwBlocker) | [An extension that helps spot zero-width characters.](https://medium.com/@aidobreen/hidden-text-fingerprints-and-how-to-avoid-them-d0103edd2ce4)

[🔝 Back to top 🔝](#)


### [Optional Browser Extensions (some suggestions for specific needs)](#optional-browser-extensions-some-suggestions-for-specific-needs)
Extension | comment
-- | --
[Acid Tabs](https://chrome.google.com/webstore/detail/acid-tabs/hgceopemmcmigbmhphbcgkeffommpjfc) | Auto-Grouping your Tabs easily.
[CheaperThan. Amazon](https://chrome.google.com/webstore/detail/cheaperthan-amazon/dgoicbnaoajknfnkijgjdelfdihpicie) | Snipe Amazon deals.
[ClearURLs](https://chrome.google.com/webstore/detail/clearurls/lckanjgmijmafbedllaakclkaicjfmnk) | [Until](https://github.com/brave/brave-browser/issues/11250) [merged](https://github.com/brave/adblock-rust/issues/166) with [Brave adblock](https://github.com/brave/brave-browser/issues/16118) (needs [syntax changes](https://github.com/brave/adblock-rust/issues/166) in Braves AdBlock). Merged in [1.30.84](https://github.com/brave/brave-browser/releases/tag/v1.30.84).
[Copy Guard](https://github.com/roedesh/copyguard) | A browser extension to prevent copy hijacking. It can be useful if you want a feedback.
[Enhancer for YouTube](https://chrome.google.com/webstore/detail/enhancer-for-youtube/ponfpcnoihfmfllpaingbgckeeldkhle) | Improve some YouTube features.
[Export links of all extensions](https://chrome.google.com/webstore/detail/export-links-of-all-exten/cmeckkgeamghjhkepejgjockldoblhcb) | Export your list of extensions.
[External Application Button](https://chrome.google.com/webstore/detail/external-application-butt/bifmfjgpgndemajpeeoiopbeilbaifdo) | Useful if you want to add [youtube-dl](https://github.com/ytdl-org/youtube-dl) to right-click!
[FastForward](https://github.com/FastForwardTeam/FastForward) | Don't waste your time with compliance. FastForward automatically skips annoying link shorteners.
[Fake news debunker by InVID & WeVerify](https://chrome.google.com/webstore/detail/fake-news-debunker-by-inv/mhccpoafgdgbhnjfhkcmgknndkeenfhe) | AI to detect fake news.
[Grammar and Spell Checker — LanguageTool](https://chrome.google.com/webstore/detail/grammar-and-spell-checker/oldceeleldhonbafppcapldpdifcinji) | Spellchecking is integrated into the Brave Browser (might not work on all websites.
[Header Editor](https://github.com/FirefoxBar/HeaderEditor) | An extension which can modify the request, include request headers, response headers, redirect requests, and cancel requests.
[JShelter](https://jshelter.org/) | Browser extension to mitigate potential threats from JavaScript.
[Kee - Password Manager](https://chrome.google.com/webstore/detail/kee-password-manager/mmhlniccooihdimnnjhamobppdhaolme) | Helper extension for KeePass.
[MyJDownloader Browser Extension](https://chrome.google.com/webstore/detail/myjdownloader-browser-ext/fbcohnmimjicjdomonkcbcpbpnhggkip) | Only relevant if you use/work with [JDownloader2](https://jdownloader.org/jdownloader2).
[papers-with-video](https://chrome.google.com/webstore/detail/papers-with-video/aflnhgmklenfljibnfellgkmdpmmoekf) | Add a video icon to the paper title on arxiv.org if a conference video exists for the paper.
[Reddit Enhancement Suite](https://chrome.google.com/webstore/detail/reddit-enhancement-suite/kbmfpngjjgdllneeigpgjifpgocmfgmb) | Some Reddit tweaks.
[Search by Image](https://chrome.google.com/webstore/detail/search-by-image/cnojnbdhbhnkbcieeekonklommdnndci) | reverse Image Search utility.
[Shodan](https://chrome.google.com/webstore/detail/shodan/jjalcfnidlmpjhdfepjhjbhnhkbgleap) alternative [(Open Source) Country Flag & Website Info](https://chrome.google.com/webstore/detail/open-source-country-flag/peofjmjcfkokkfmffphnhcmnkakdlghm) | IP info, Whois and more for visited domain (website).
[SponsorBlock for YouTube](https://chrome.google.com/webstore/detail/sponsorblock-for-youtube/mnjggcdmjocbbbhaepdhchncahnbgone) | Skip sponsor ads on YouTube.
[Tampermonkey](https://chrome.google.com/webstore/detail/tampermonkey/dhdgffkkebhmkfjojejmpbldmpobfkfo) | Make sure to opt-out of telemetry! There are [alternatives](https://chrome.google.com/webstore/detail/violentmonkey/jinjaccalgkegednnccohejagnlnfdag) but they do not work as well as TM. TM needs `enable-javascript-harmony` & `enable-experimental-web-platform-features` for some features (default disabled in Brave), only activate it if absolutely necessary.
[The Commenter](https://chrome.google.com/webstore/detail/the-commenter/glhpoenomnnhjddjloedbjoeeianflod) | Check for comments on the web.
[Tomato Clock](https://chrome.google.com/webstore/detail/tomato-clock/enemipdanmallpjakiehedcgjmibjihj) | Egg timer for your Browser.
[VectorDraw - Paint on Tab](https://chrome.google.com/webstore/detail/vectordraw-paint-on-tab/ncffpnjojecpmbbejgficgcphjijfigc) | Pain on tabs, useful if you do some videos and want to show something.
[vidIQ Vision for YouTube](https://chrome.google.com/webstore/detail/vidiq-vision-for-youtube/pachckjkecffpdphbpmfolblodfkgbhl) | YouTube statistics (needs login for advance functions!)
[Web Scrobbler](https://chrome.google.com/webstore/detail/web-scrobbler/hhinaapppaileiechjoiifaancjggfjm) | Web Scrobbler helps online music listeners to scrobble their playback history.
[WebWormhole](https://chrome.google.com/webstore/detail/webwormhole/jhombkhjanncdalcbcahinpjoacaiidn) | WebWormhole lets you send files from one place to another.
[YouTube Dislike Count which doesn't need external API call](https://textbin.net/8iyxfntpaa) | Userscript solution which works without any external API, an extension but with external calls is available [here](https://chrome.google.com/webstore/detail/youtube-dislike-button-co/mjnhacklcfliofhdgnkemmkioinkhcnk?ucbcb=1).


[🔝 Back to top 🔝](#)


### [Browser Extensions you DO NOT need](#browser-extensions-you-do-not-need)
Extension | comment
-- | --
[Barrier](https://chrome.google.com/webstore/detail/barrier/glaclfmcjdiljbojakihhobalpnihndd) | Already integrated into Brave Shields.
[Canvas Blocker](https://chrome.google.com/webstore/detail/canvas-blocker-fingerprin/nomnklagbgmgghhjidfhnoelnjfndfpd) | Brave [randomize the fingerprint, depending on your Shield settings](https://brave.com/privacy-updates-3/).
[Canvas Fingerprint Defender](https://chrome.google.com/webstore/detail/canvas-fingerprint-defend/lanfdkkpgfjfdikkncbnojekcppdebfp) | ↑
[CanvasFingerprintBlock](https://chrome.google.com/webstore/detail/canvasfingerprintblock/ipmjngkmngdcdpmgmiebdmfbkcecdndc) | ↑
[ChromeGalvanizer](https://github.com/mandatoryprogrammer/ChromeGalvanizer) | Harden your browser against extension backdoors and exploits. Brave includes hardening already by default.
[Cookie-AutoDelete](https://github.com/Cookie-AutoDelete/Cookie-AutoDelete) | Set shield defaults to never allow Cookies and only unlock Cookies when needed, ensure "clear browser data on exit" and cookies are enabled in Brave's settings.
[Decentraleyes](https://chrome.google.com/webstore/detail/decentraleyes/ldpochfccmkkmhdbclfhpagapcfdljkj) | Decentraleyes is practically abandonware with little to no impact and outdated resources. The benefit cannot be proven in the real-world because CDNs update very often, due to security fixes, performance etc. using hardcoded and old libraries can make you more vulnerable.
[Disconnect](https://disconnect.me/disconnect) | Useless, integrated into Braves filter-lists.
[Ghostery](https://www.ghostery.com/) | Brave Adblock does the same. ↑
[HTTPS Everywhere](https://github.com/EFForg/https-everywhere) | Integrated into [Brave Shields](https://support.brave.com/hc/en-us/articles/360022973471-What-is-Shields).
[LAN-port-scan forbidder](https://github.com/garywill/LAN-port-scan-forbidder) | Browser extension to protect private network. You can archive same with a Lan blocking filterlist + Browser restricts specific ports already by default.
[LocalCDN](https://chrome.google.com/webstore/detail/localcdn/njdfdhgcmkocbgbhcioffdbicglldapd) | Integrated into Brave Shields, lots of [CDNs and Endpoints getting tunneled](https://github.com/brave/brave-browser/wiki/Deviations-from-Chromium-(features-we-disable-or-remove)#services-we-proxy-through-brave-servers).
[NoScript](https://chrome.google.com/webstore/detail/noscript/doojmbjmlfjjnbmnoijecmcbfeoakpjm) | Not needed, you archive same with Brave shield or uBlock (if you know how to work with custom filters).
[Privacy Badger](https://privacybadger.org/) | Privacy Badger does same as uBO/Brave Adblock, the ["AI" based function (learning) got disabled by default](https://www.eff.org/privacybadger/faq#How-does-Privacy-Badger-work) due to metadata (privacy) concerns. It can also easily be [detected](https://adtechmadness.wordpress.com/2020/03/27/detecting-privacy-badgers-canvas-fp-detection/).
[Privacy Possum](https://github.com/cowlicks/privacypossum) | Integrated into Brave Shields.
[Trace](https://chrome.google.com/webstore/detail/trace-online-tracking-pro/njkmjblmcfiobddjgebnoeldkjcplfjb) | Partially integrated into Shields, not all features.
[uBlock Origin](https://github.com/gorhill/uBlock) | Only needed if you are an advance user because Brave Adblock constantly evolves together with uBlock and new features getting adopted and integrated.


[🔝 Back to top 🔝](#)


### [Parcourstest](#parcourstest)

Here are the tests the Browser (Desktop/Mobile) needs to pass. This needs to be done so that we know the flag/changes we done do not influence (negatively) the Browser in a way we do not want. [Privacytests.org](https://privacytests.org/) provides a solid but not perfect overview of what is currently covered with the DEFAULT Brave Browser settings and shield settings. Test results variate a lot with changed shield settings as well as changed flags and settings.


This is my own Test Setup.


- All: `brave://interstitials/` must pass (contains all sub-resources to test security, privacy etc.), there ae bunch of others like e.g. `chrome://floc-internals/` but they are not relevant since the source for this got removed.
- Security: [BrowserAudit](https://browseraudit.com/), needs minimum a score of 95% (some tests never pass on Chrome, this is okay and expected). You need to disable the shield and allow cookies to test it. Keep in mind that the test is not 100 percent reliable and is only an overall test to quickly reveal majaro issues and nothing more.
- Performance: [Input lag test](basro.github.io/input-lag-measuring-tool), needs to pass 90+ Hz check (your monitor/device needs to support it) on some Android ROMs you need to enforce the [refresh rate manually](https://www.androidcentral.com/how-change-your-phones-resolution-and-refresh-rate) (or use an [app](https://forum.xda-developers.com/t/app-galaxy-max-hz-refresh-rate-control-quick-resolution-switcher-screen-off-mods-adaptive-mod-keep-high-adaptive-on-power-saving-mode-and-more.4181447/) and unlock [fps](https://forum.xda-developers.com/t/mod-increase-frames-per-second-5-14-15.3108786/))
- Privacy: [Browser IP leak](https://browserleaks.com/ip), needs to pass in Tor + Incognito mode
- Privacy: Cloaked CNAMEs _check_ against a real world website e.g. https://publicwww.com/websites/EA_data/ Brave shields must block `https://seomon.com/piwik/matomo.js`.
- Browser platform test: [Web Platform Tests](https://web-platform-tests.org/), needs to pass
- Privacy: [FLoC](https://github.com/brave/brave-browser/issues/14942), needs to pass (check against a website which supports it e.g. https://web.archive.org/)
- Security: [Schemeflood](https://schemeflood.com/), needs to pass
- Privacy: [Font Fingerprinting test](https://amiunique.org/fp), see [here](https://github.com/brave/brave-browser/issues/816)
- Privacy: [window.Intl.DateTimeFormat() API](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Intl/DateTimeFormat/DateTimeFormat#Parameters), see [here](https://github.com/brave/brave-browser/issues/8574)
- Privacy: [Dark Mode detection](https://github.com/brave/brave-browser/issues/15265), needs to pass
- Privacy: `Clear Data on Exit` must be enabled and enforced by default
- Privacy: [HSTS fingerprinting](https://github.com/pastly/satis-hsts-tracking), needs to pass, [read how it works](https://www.usenix.org/system/files/conference/foci18/foci18-paper-syverson.pdf) and [how to protect yourself](https://webkit.org/blog/8146/protecting-against-hsts-abuse/) - Shields set to "aggressive" & cookies blocked (by default must be enabled)
- Privacy: Do Not Track must be disabled (default), its [useless](https://boingboing.net/2018/10/17/no-call-list.html) and enabling it [results in more fingerprinting](https://www.w3.org/2011/track-privacy/papers/Soghoian.pdf)
- Privacy: [Cover your Tracks](https://coveryourtracks.eff.org/about), needs to pass (fonts and GL / canvas fingerprints randomized) - The site is misleading, because it can only detect a unique fingerprint within your session. You can test this if you try running the test and making note of the actual fingerprint ID, after that, restart your browser and run the test again. Compare the two fingerprint IDs. If they're the same, your fingerprint is persisting across sessions, which is problematic. The website doesn't show you your actual fingerprint ID, so you have to go to [browserleaks.com/canvas](https://browserleaks.com/canvas) and scroll down to the "Your Fingerprint" section, and you'll see your fingerprint ID (signature).
- Privacy: [3rd party cookie bypass](https://xsid-demo.glitch.me/5wmt9tz.html), needs to pass ("Block third-party cookies" must be enabled [default]).
- Privacy: [Does your browser have TablesNG?](https://tablesng.com/), do not need to pass because the fingerprint vector for this is none existing. But it indicates if your flag with TablesNG worked or not (only interesting for nightly users).
- Privacy: [SameSite 🍪 sandbox](https://samesite-sandbox.glitch.me/), needs to pass
- Privacy: [is-chrome-100-yet.glitch.me](https://is-chrome-100-yet.glitch.me/) must return: NO which is always the case because we never use not enforce `#force-major-version-to-100`.
- Functionality: [webcamtests](https://webcamtests.com/), Webcam Test Web Utility must show a picture in case you use and plugged in your webcam. Since we blocked the webcam permission by default, you need to unlock that permission first for the website. Do not add an general exclusion to the permission page. This then also tests if it really blocks the cam permission or not each time we revisit the page.
- Security: [XSinator – XS-Leak Browser Test Suite](https://xsinator.com/), needs to pass, this will not happen this year but this is a long-time goal.

----------------------------------------------------------

The official [Brave QA Test Pages are here](https://dev-pages.brave.software/index.html).


[🔝 Back to top 🔝](#)


### [Brave Browser FAQ](#brave-browser-faq)
- [Brave has its own alternative to Firefox's Total Cookie Protection with Ephemeral Site Storage](https://brave.com/privacy-updates/7-ephemeral-storage/)
- [Brave: Opt-In Data Collection](https://support.brave.com/hc/en-us/articles/4409406835469)
- [Brave Telemetry Explained](https://brave.com/popular-browsers-first-run/)
- [Uphold Privacy Policy (used by Brave Rewards)](https://uphold.com/en/legal/privacy-policy)
- [Brave forces rival browser 'Braver' to change its name](https://decrypt.co/35146/brave-forces-rival-browser-braver-change-name), the Browser was always behind Chromium (un-googled, Brave,... and is now "dead")
- `I can't claim my BAT!?` Try disabling any VPN/Proxy or SOCKS. In case you're on Android you need SafetyNet to pass, you can try to [bypass it via Magisk](https://android.gadgethacks.com/how-to/magisk-101-fix-safetynet-cts-profile-mismatch-errors-0178047/).
- [Brave Team answered to wrong accusations](https://np.reddit.com/r/brave_browser/comments/nw7et2/i_just_read_a_post_on_rprivacytoolsio_and_wtf/h18fxec/?context=3), see [here](https://old.reddit.com/r/CryptoCurrency/comments/nxce6t/brave_browser_scam_a_fake_privacy_browser_sharing/h1ely5i/) for more details. Especially [Firefox fanboys cannot accept the competition](http://ebin.city/~werwolf/posts/brave-is-shit/) even after they got [proven wrong](https://news.ycombinator.com/item?id=27552530) they do not even edit their article.
- [IPFS Support in Brave](https://brave.com/ipfs-support/)
- Brave News for Android - To enable it go to `brave://flags` and enable the `Brave News` toggle. It will hit the release version of Android on Jan 4, 2022. At the time of posting it, it is only available trough nightly.

[🔝 Back to top 🔝](#)


### [Brave VPN FAQ](#brave-vpn-faq)

![Brave VPN](https://i.ibb.co/QMtrfSN/2021-11-12-00-52.png)

- [Brave VPN](https://guardianapp.com/company/partners/brave/) is based on The Guardian VPN - 9,99 per month.
- Brave wants 4,99 Dollars per month but with less servers you can choose from compared to what Guardian offers and only limited up to 100Mbps.

[🔝 Back to top 🔝](#)


### [Brave Talk FAQ](#brave-talk-faq)
- [Differences between Jitsi and Brave Talk](https://old.reddit.com/r/BATProject/comments/q77o9g/brave_talk_vs_jisti/).
- You can access [Brave Talk](https://brave.com/brave-talk-launch/) via sidebar (needs to be enabled) or via official URL directly: [talk.brave.com](https://talk.brave.com/).
- Why do I need to enable Rewards to use Brave Talk? For the no-cost option, enabling Brave Rewards helps Brave to cover the costs of video infrastructure. There is an alternative option available, you can subscribe to Brave Premium for a cost ($7 USD/month).

[🔝 Back to top 🔝](#)


### [Brave Rewards FAQ](#brave-rewards-faq)
- Brave Rewards, depending on your country count as income, which means it is [NOT tax free](https://koinly.io/blog/crypto-airdrop-tax/).
- [The browser Brave pays its 42 million users 70% of the revenue it generates from ads they see. Brave compensates them in its own “Basic Attention Tokens,” which they can redeem for currency or use to tip their favorite sites. Users report earning $5 to $10 monthly, according to a Brave spokeswoman.](https://www.wsj.com/articles/personal-data-is-worth-billions-these-startups-want-you-to-get-a-cut-11638633640?mod=hp_featst_pos3)
- In case you see no Ads at all while you actually enabled it, make sure you check this [article](https://community.brave.com/t/if-you-not-receive-ads-on-windows-or-ubuntu/162298) first.
- [BAT is a cryptocurrency you get from Brave Rewards](https://basicattentiontoken.org/)
- [At the End of Every Month Your Bat Rewards Stats Reset](https://github.com/brave/brave-browser/issues/15005)
- Verifying your (Uphold/Gemini) Wallet requires minimum 15 BAT (_reduced from previously 25_).
- Claiming Rewards on Mobile [requires SafetyNet to pass](https://ruqqus.com/+BraveBrowser/post/bk8n/android-if-your-phone-fails-safetynet) and depends on Google Play Services. If you never pass SN you will not be able to claim your BAT.
- [How can I add my other Crypto Wallets to Brave?](https://support.brave.com/hc/en-us/articles/360034535452)
- If you cannot claim your reward disable your VPN/Proxy and restart (relaunch) your Browser.
- If you see 0.00 BAT (while you actually have some BATs) wait, the sync might be confused, no need to panic! Waiting or restarting your Browser can help in this case.
- If you format your PC/Smartphone you loose your BAT because they are temporarily stored on local machine until sync grabs it.
- [Custom tipping amount](https://old.reddit.com/r/BATProject/comments/nn73yz/custom_tipping_amounts_feature_is_now_live_on/) can freely adjusted (_for now_) on Desktop only.
- [No more 5 BAT payout minimum for Creators](https://ruqqus.com/+BraveBrowser/post/c5wk/no-more-5-bat-payout-minimum).
- I got some BAT and cannot verify my wallet (country not supported etc.). Create a publisher's account and connect your YouTube, Reddit or a website. Then tip yourself. You'll lose 10% of your BAT in the process, but it's better than losing everything.
- [Gemini Now Provides an Integrated Crypto Experience for Brave Users](https://www.gemini.com/blog/gemini-now-provides-an-integrated-crypto-experience-for-brave-users)
- [The new Gemini User Wallet in Brave Rewards lets users seamlessly redeem and move their BAT. (video)](https://vimeo.com/595169365), for text only announce, [check this out](https://brave.com/gemini-user-wallet/).
- Rewards are borked on Arch Linux based Distros, which seems to be a [Wayland problem](https://github.com/brave/brave-browser/issues/13352).
- You can change the ads window position, just click and hold on the window while it appears and then you can drag it to another position.
- The lack of Brave Rewards on iOS is thanks to Apple's App Store rules, see [here](https://brave.com/rewards-ios/) why.
- You can obtain growth statistics for BAT [here](https://basicattentiontoken.org/growth), monthly [growth statistics are disclosed here](https://bravebat.info/).


[🔝 Back to top 🔝](#)


### [Brave Wallet FAQ](#brave-wallet-faq)

You can see the Wallet implementation progress [here](https://github.com/brave/brave-browser/projects/24).

- Brave [Wallet’s source code](https://github.com/brave/brave-core/blob/master/LICENSE) is available under an Open Source license, unlike other popular web 3.0 extensions.
- If you install MetaMask, then the default wallet will actively change to MetaMask. If you’re a user of the old Crypto Wallets extension in Brave (a fork of MetaMask), then the first thing to know is that you can switch back to the old wallet in brave://settings/wallet by changing your default wallet back to Crypto Wallets.
- Mobile wallet support (_planned_)
- Full native NFT support, including owned NFT discovery, an NFT catalog, and the addition of NFT asset values in your portfolio. (_planned_)
- Support for more blockchains (_planned_)
- Brave Swap Rewards (_planned_)
- Brave Rewards integrated into the wallet UI (_planned_)
- Live Market data for most asset (including non EVM based assets) (_planned_)
- Default currency and crypto conversion display settings. (_planned_)

[🔝 Back to top 🔝](#)


### [Brave Search FAQ](#brave-search-faq)

Brave needs to fix mentioned points otherwise I cannot suggest using it as private alternative. Until then you could use Qwant, Presearch or other [listed alternatives](https://chef-koch.bearblog.dev/privacy-tools-list-by-chef-koch/#metasearch-engines).


![Brave Premium Search](https://i.ibb.co/Lvt1tJ6/j0ail2sokac81.png)


- [Brave Search Premium is 3$ a month](https://account.brave.com/?intent=checkout&product=search), Brave intends to implement Brave Rewards into Brave Search sometime in mid 2022. If you pay premium you "Get a cleaner view on all results pages", which means those that don't won't get cleaner page results.
- [Brave Search censorship](https://web.archive.org/web/20211202152804/https://imgur.com/a/lkPTFC1) - [original source](https://imgur.com/a/lkPTFC1) - is even worse than [Google Search censorship](https://en.wikipedia.org/wiki/Censorship_by_Google).
- [Brave Search requires you to solve a Captcha behind a VPN or Tor](https://imgur.com/8RUS3Vu)
- Amazon is used as their CA.
- Brave access your IP address upon your visit to determine your location and better serve you ads. While they claim to not store IP addresses, unlike DDG and Startpage, they do read your full IP address which is not private.
- Brave uses Amazon Cloudfront as their CDN, meaning all traffic passes through Amazon servers. CDNs itself are more than controversial. CDN usage violating GDPR according to Munich State Court, but this does not that mean [CDNs in general are not illegal](https://news.ycombinator.com/item?id=30135264).
- Brave Search is currently not displaying any ads in their Beta period, but the free version of Brave Search will soon be ad-supported. Brave Search will also offer an ad-free premium version in the near future, it is unclear if you can, similar like with Talk, use your Rewards to unlock the premium version or not.
- [Brave Search Uses Click Data in Search Ranking Algorithm](https://www.seroundtable.com/brave-search-uses-click-data-ranking-algorithm-32319.html)
- [Brave Removes Google as its Default Search Engine](https://brave.com/search-and-web-discovery/). Braves own search engine region selection [depends on your location](https://github.com/brave/brave-browser/issues/18331).
- **FAKE** URL: `h̷t̷t̷p̷s̷:̷/̷/̷b̷r̷a̷v̷e̷s̷e̷a̷r̷c̷h̷.̷c̷o̷m̷/̷` and the **real URL** is: `https://search.brave.com`.
- [Brave Search](https://brave.com/brave-search-beta/) is still beta, which means that since October 2021, Brave Search was declared the default search engine for the Brave browser users in the US, Canada, UK (replacing Google Search), France (replacing Qwant) and Germany (replacing DuckDuckGo and Ecosia).
- Starting with Brave Browser v1.26.67+ you can set the search engine to Brave Search.
- What are "[bangs](https://duckduckgo.com/bang)"? Bangs are shortcuts that quickly take you to search results on other sites. For example, when you know you want to search on another site like Wikipedia or Amazon, our bangs get you there fastest. A search for !w filter bubble will take you directly to Wikipedia.
- You get locally based search results if you change the location settings on search.brave.com and save cookies under `brave://settings/cookies`, you must check that "Sites that can always use cookies" is selected for the website. This is a web limitation and not Braves fault, without cookies no new content can be indexed to show the actual results.

[🔝 Back to top 🔝](#)


### [Brave - Ask me anything (AMA) (sorted from newest to oldest)](#brave---ask-me-anything-ama-sorted-from-newest-to-oldest)
- [Upcoming Brave Wallet AMA with Brian Bondy (CTO & Co-founder), Douglas Daniel (Front-End Engineer), James Mudgett (Sr. Director, Wallet), & Luke Mulks (VP, BizDev) from Brave - November 18, 2021 (reddit.com)](https://old.reddit.com/r/BATProject/comments/qwa4dc/upcoming_brave_wallet_ama_with_brian_bondy_cto/)
- [I'm Peter Snyder, Senior Privacy Researcher and Director of Privacy at Brave. (reddit.com)](https://old.reddit.com/r/BATProject/comments/p6u6o9/im_peter_snyder_senior_privacy_researcher_and/)
- [Brave CTO, and IPFS Lead: AMA about IPFS in Brave and the Decentralized Web (reddit.com)](https://old.reddit.com/r/IAmA/comments/l2tvx1/we_are_brian_bondy_cofounder_and_cto_of_the_brave/)
- [Reddit AMA with Brendan Eich on Brave Browser (reddit.com)](https://old.reddit.com/r/IAmA/comments/dwfbmf/im_brendan_eich_inventor_of_javascript_and/)
- [Transcript of AMA with Brendan Eich, CEO of Brave, BAT, Creator of JavaScript (reddit.com)](https://old.reddit.com/r/BATProject/comments/7l4033/transcript_of_ama_with_brendan_eich_ceo_of_brave/)

[🔝 Back to top 🔝](#)


### [Brave Referral Story](#brave-referral-story)

- [Brave browser CEO apologizes for automatically adding affiliate links to cryptocurrency URLs](https://www.theverge.com/2020/6/8/21283769/brave-browser-affiliate-links-crypto-privacy-ceo-apology).

The whole story got a lot of attention, however it always was misleading and spread to gain clicks. The matter was resolved after 7-8 hours and pushed within 12 hours as commit. The actual update got released within 24 hours. Some users had to wait 48 hours because this is how the distribution system handles and delivers updates to avoid huge pressure on the server or hit GitHub limitations.

> “That being said, I think there was a lot of misunderstanding of the situation. There was no privacy harm to users, and what was being done is similar to how most, if not all, browsers interact with search engines, to receive referral cash. Using DDG in Firefox, to give one example, tells DDG the query came from Firefox the "FFAB", or, guessing, "Firefox Address Bar"…”


> “…The user was never able to be tracked, the site wasn't able to learn anything additional about you, etc.”

[Source](https://reddit.com/r/BATProject/comments/p6u6o9/_/h9fwa42/?context=1)

Later in 2020 the [referral program was shut down](https://brave.com/referral-program-update/).


### [Reference for the Brave vs. Browser X discussion](#reference-for-the-brave-vs-browser-x-discussion)
- [Browser Startup Comparison (netmeister.org)](https://www.netmeister.org/blog/browser-startup.html) and [Braves own inspection (brave.com)](https://brave.com/popular-browsers-first-run/)
- [Browser privacy analyzed (tcd.ie) [pdf]](https://www.scss.tcd.ie/Doug.Leith/pubs/browser_privacy.pdf)
- [Firefox and Chromium (madaidans-insecurities.github.io)](https://madaidans-insecurities.github.io/firefox-chromium.html)
- [Goggles: Democracy dies in darkness, and so does the Web (brave.com) [pdf]](https://brave.com/wp-content/uploads/2021/03/goggles.pdf)
- [How to find the most secure browsers (onlinesecurityworld.com)](https://onlinesecurityworld.com/how-to-find-the-most-secure-browsers/)
- [Mozilla's position on specific web standards (mozilla.github.io)](https://mozilla.github.io/standards-positions/)
- [The Security Architecture of the Chromium Browser (seclab.stanford.edu)](https://seclab.stanford.edu/websec/chromium/chromium-security-architecture.pdf)
- [Update on Brave’s Ongoing Direct Mail Marketing Campaign](https://old.reddit.com/r/brave_browser/comments/t4gzuw/update_on_braves_ongoing_direct_mail_marketing/)

[🔝 Back to top 🔝](#)


## [Why does Brave consume more RAM than Chrome](#why-does-brave-consume-more-ram-than-chrome)
- Brave currently contains over 250k code changes compared to Chrome, which adds a lot of more features such as ad-blocking, Rewards, Wallet integration and more. Brave is not only yet another Chromium fork and adds a lot of unique features.
- You can reduce the overall memory footprint by disabling hardware acceleration and disable to let run Brave in the background. Both options are enabled by default. You find the options under `brave://settings/system`. Disabling Brave News also reduces the memory usage.
- The Brave Team as well as the Chrome team constantly working on lowering the overall memory footprint, however while adding more and more features and dependencies this is a challenging task.
- On some systems Brave comes preinstalled with an extension called Plasma Integration, it is enabled by default. If you do not use the GTK+ theme + search for e.g. Kwin or KRunner you can disable or uninstall it.

[🔝 Back to top 🔝](#)


## [Aggressive trolling because Brave uses the word ”Privacy”](#aggressive-trolling-because-brave-uses-the-word-privacy)

Especially some Firefox people or shall I say loyal fans [trolling](https://en.wikipedia.org/wiki/Internet_troll) Brave Browser and their Developer Team since practically day one because of the marketing slogan - ”privacy browser”. This is harsh as well as based because no Browser ever will be perfect in this regard. Privacy is not an on or off switch and needs continuously inspection, maintenance and changes to adopt new problems. Those smear campaigns come often from uneducated people that are not even developers themselves, these people tend to cherry pick some leaks or open issue tickets and claim the Browser is not as private as advertised to make the Browser look worse than others. This is a pointless effort because you find on every single Browser some open issue tickets, Tor Browser, Firefox, all of them have always some open issue tickets regarding privacy. This is not how FOSS works and this is no measurement instrument as "privacy index". The Brave Team puts a lot of time and research into privacy related problems, same like Firefox and the Tor Browser Project.

Another strategy is to [spread fake forks to smear Brave](https://aur.archlinux.org/packages/unbrave-git), even after I reported it to Brave and the Arch Team via Tweet, such disrespectful forks continue to stay online. Not only is this deformation it also exposes how based people are against any competition.

Brave Browser is de facto privacy respecting and does by default more than any other Browser on the market, this is done by including a lot of ideas and privacy respecting changes directly into the Brave Browser. In every other Browser you need to work with extensions or configuration changes to come even remotely close to Brave Browser. I do not see how the troll argumentation holds that Brave fails regarding privacy, it is offering a solid ground with the arguably best default out-of-the-box configuration.

If you goal is to become nearly anonymous then use Tor Browser, the Brave Team clearly communicated this since day one on their website.

[🔝 Back to top 🔝](#)


## [Story about Dissenter](#story-about-dissenter)

Fake with false background information.
- [Brave legally threatens Brave fork trying to remove adds.](https://bitgrum.com/2020/09/11/brave-browser-fork-changes-name-after-legal-threats/)

> [In April 2019, Dissenter was removed from the Firefox Add-ons website and the Chrome Web Store for violation of their policies that causes the creation of the Dissenter web browser.

[Source](https://discourse.mozilla.org/t/the-removal-of-the-dissenter-extention/38140/70)


Actual facts:
- [Alt-Right ‘parasites’ fork Brave Browser, replace BAT with BTC](https://micky.com.au/gab-parasites-fork-brave-browser-replace-bat-with-btc/)
- [Dissenter (web browser)](https://everipedia.org/wiki/lang_en/dissenter-web-browser)
- [Gab Network and Dissenter](https://en.wikipedia.org/wiki/Gab_(social_network)#Dissenter)
- [No one disputes the fact that Gab’s founder has the right to fork Brave. We just don’t think nazis add value to anything, including code bases](https://www.customerservant.com/no-one-disputes-the-fact-that-gabs-founder-has-the-right-to-fork-brave-we-just-dont-think-nazis-add-value-to-anything-including-code-bases/)
- [What happened to Dissenter](https://old.reddit.com/r/browsers/comments/ptaau2/what_happened_to_dissenter/)

[🔝 Back to top 🔝](#)


## [Story about Braver Fork](#story-about-braver-fork)

The story was mainly about [Trademark](https://trademarks.justia.com/869/51/brave-86951863.html) violation and not about replacing ads, the Team never asked or contacted Brave to ask for permission to begin with. Also you need to do some legal proceeding because GitHub does not take content offline without any court order or trademark confirmation.

- [Brave forces rival browser 'Braver' to change its name](https://decrypt.co/35146/brave-forces-rival-browser-braver-change-name)

[🔝 Back to top 🔝](#)


## [Contradiction regarding Privacy Communities](#contradiction-regarding-privacy-communities)

Brave contradicts themselves with weird statements regarding supporting privacy related communities or not. This is not positive nor negative, just weird.

["Brave doesn't want to be associated with privacy focused groups"](https://web.archive.org/web/20210914083347/https://privacyguides.org/browsers/) while [Peter Snyder](https://brave.com/ama-with-peter-snyder/) is backing [GPC](https://brave.com/web-standards-at-brave/4-global-privacy-control/) along with [DuckDuckGo](https://spreadprivacy.com/global-privacy-control-enabled-by-default/), [Mozilla](https://blog.mozilla.org/netpolicy/2021/10/28/implementing-global-privacy-control/), [Disconnect](https://blog.disconnect.me/introducing-global-privacy-control/), [Abine](https://www.abine.com/blog/2020/online-privacy-leaders-launch-gpc-global-privacy-control-standard/) and the [EFF](https://www.eff.org/gpc-privacy-badger).


## [Personal Note](#personal-note)

I do not work for Brave nor do I get paid for writing any of this. The intention/motivation behind this guide is to harden Brave Browser for maximum performance, security, privacy and make it even more awesome than it already is.


[🔝 Back to top 🔝](#)
