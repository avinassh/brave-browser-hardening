## Additional about:flags changes by [CHEF-KOCH](https://twitter.com/CKsTechNews) (CKTN) to harden [Brave Browser](https://brave.com/)

![Logo Banner - Credit: ledger.com](https://www.ledger.com/wp-content/uploads/2021/05/cover.png)


## [Project updates](#project-updates)

I'll try to keep this hardening guidance updated as much as I can. The below listed flags configuration/changes and tips are only tested against Windows/Linux & Android, I do not plan to test them against MacOS/iOS!


## [Introduction](#introduction)

*Hardening does not start at choosing the right tools or networks, hardening begins with gathering information to inform yourself and others in order to stay up-to-date so that you can deal with current and upcoming threats. Tools, extensions and Co. are just a workaround until someone build the right system, that starts by voting and supporting the right politicians and organisations.* – Statement CHEF-KOCH, 1997


The main purpose of this guidance is to inform people about possibilities to enhance Brave Browser without depending on other tools or the Brave Team. You also do not need too rely on other quickly outdated guides on the Internet and hopefully even get a learning effect.


In case you have some questions, you can ask them directly on my official [Matrix Server](https://matrix.to/#/#cktn:matrix.org) or use the issue ticket feature to open relevant tickets so that we can address new stuff.

----------------------------------------------------------

## [Table of contents](#table-of-contents)

[[_TOC_]]

----------------------------------------------------------

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
- Google's [Safe Browsing](https://safebrowsing.google.com/) and other security checks and connections are NOT wanted. The OS has its its own protection mechanism (OS security model + hardening).
- [FLoC is disabled](https://brave.com/why-brave-disables-floc/) by default in Brave. Chrome users can use uBlock or change it manually via [flags](https://twitter.com/CKsTechNews/status/1399422582588383242).
- How we [compare the network behavior of popular browsers on first-run](https://brave.com/popular-browsers-first-run/).
- All credential checks are disabled since we do not store passwords in Brave, instead we use KeePass or other password managers of your choice.

----------------------------------------------------------

## [Unresolved issues with the biggest privacy/security impact](#unresolved-issues-with-the-biggest-privacysecurity-impact)

You find an overview of [all opened privacy related and reported issues directly on the issue tracker](https://github.com/brave/brave-browser/labels/privacy%2Ftracking). [x] indicates that mentioned issue was fully resolved, or that this is something that will not be fixed.

- [Working with Flags and background info when they exire](https://chromium.googlesource.com/chromium/src/+/HEAD/docs/flag_expiry.md)
- [List of all Flags](https://source.chromium.org/chromium/chromium/src/+/main:chrome/browser/flag-metadata.json;l=1)
- [List of all Flags that never expire](https://source.chromium.org/chromium/chromium/src/+/main:/chrome/browser/flag-never-expire-list.json)


Please keep in mind that just because there are open issues tickets that this is not necessarily actively abused in the real-world. In lots of cases it is hard to find evidence that theoretically problems are used to directly compromise your security or privacy. Also some of the mentioned issues might be very hard to fix because trying to workaround them can results in unwanted side effects, such as Browser crashes, website breakages etc.


- [ ] Letterboxing ([window size](https://github.com/brave/brave-browser/issues/720))
- [ ] [Crooked Style Sheets Tracking Attacks](https://github.com/brave/brave-browser/issues/818)
- [ ] [Cross-device tracking via ultrasonics](https://github.com/brave/brave-browser/issues/823)
- [ ] [DRAWN APART : A Device Identification Technique based on Remote GPU Fingerprinting](https://orenlab.sise.bgu.ac.il/p/DrawnApart), pretty much every Browser is affected by the new attack.
- [ ] [ETag - Block Tracking via etags and cached scripts](https://github.com/brave/brave-browser/issues/536), possible solution mentioned [here](https://github.com/brave/brave-browser/issues/10719). Test pages can be found [here](http://lucb1e.com/rp/cookielesscookies/) and [here](https://levelup.gitconnected.com/no-cookies-no-problem-using-etags-for-user-tracking-3e745544176b).
- [ ] [Font based fingerprinting](https://github.com/brave/brave-browser/issues/816)
- [ ] [HSTS fingerprinting](https://github.com/brave/brave-browser/issues/5936), see [here](https://webkit.org/blog/8146/protecting-against-hsts-abuse/)
- [ ] [IPTC meta data in images](https://github.com/brave/brave-browser/issues/5238)
- [ ] [Intel iGPU sandboxing in Linux does not exists](https://github.com/brave/brave-browser/issues/19232), fixed with latest [Chromium commit](https://chromium.googlesource.com/chromium/src/+/c45894a002e2d04ccffbd60c568a247fddf60f0e)
- [ ] [Language based fingerprinting](https://github.com/brave/brave-browser/issues/20096)
- [ ] [Resource Timing](https://github.com/brave/brave-browser/issues/5487)
- [ ] [Retrieving your browsing history through a CAPTCHAs](https://varun.ch/history), see [here](https://github.com/w3c/csswg-drafts/issues/3012). On Firefox this can be prevented with toggling `layout.css.visited_links_enabled` while on Chrome you need to manually clear your Browsing history after the session ended. Mozilla has an article regarding such protection mechanism over [here](https://developer.mozilla.org/en-US/docs/Web/CSS/Privacy_and_the_:visited_selector).
- [ ] [TCP Fast Open (TFO)](https://github.com/brave/brave-browser/issues/6800)
- [ ] [TLS session resumption tracking](https://github.com/brave/brave-browser/issues/1852)
- [ ] [There is currently no master password available for saved passwords](https://github.com/brave/brave-browser/issues/13350), which can lead to security and privacy related issues.
- [ ] [Trackability of QUIC connections](https://github.com/brave/brave-browser/issues/3855)
- [ ] [WebGL Extension farbling](https://github.com/brave/brave-browser/issues/15904)
- [ ] [Window dimension based fingerprinting](https://github.com/brave/brave-browser/issues/720)
- [ ] [Zoom Levels tracking](https://github.com/brave/brave-browser/issues/541)
- [ ] [window.Intl.DateTimeFormat() API](https://github.com/brave/brave-browser/issues/8574)
- [ ] getSupportedExtensions in [WebGL](https://github.com/brave/brave-browser/issues/15904)
- [x] Some [AV products using and inspecting your camera and your lockscreen](https://support.kaspersky.com/15408#cameras) - This is a wontfix because this is how AVs and their security features work. You manually need to allow Brave to use the camera permission or block/allow the AV to use/not use it.

----------------------------------------------------------

## [Hardening is not a selling argument](#hardening-is-not-a-selling-argument)

The mass media and some privacy communities wrongfully echo chamber that hardening and applying best practices represent security and privacy, this is an unproven claim. The reason why this is unproven is the fact that the vast majority does not use hardened profiles on a daily bases, there are [cases showing that even hardening setups can be compromised](https://symantec-enterprise-blogs.security.com/blogs/threat-intelligence/daxin-backdoor-espionage), it is a matter of effort. In other words there is no proof that this is enough, what it does is that it potentially reduced the attack surface but this is all. It does not mean you are untouchable or cannot be exploited. Even if you manage to harden everything you still need to take the human factor in consideration, social engineering works really well and can bypass every firewall, every OS or Browser hardening in a matter of time. The Browser acts like a gateway not meant to be a firewall to monitor every data package that goes trough.

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

Brave will not sync those newly set permission defaults. You need to backup your profile manually, this is still the best way to deal with profile corruptions or in case you want to copy your settings to another profile or PC. Permission sync is planned feature.


**Why enforce some settings that depending on your global Shields settings**

We enforce some settings as defaults for various reasons however, some flags and features depending on your global Shield settings for example by default Unlinkable Bouncing is only enable when you set your global Shield setting to aggressive. We override this behavior in case there are some website breakages but and temporarily lowering the shield setting for an specific website without loosing some protection mechanism.

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


### [Additional lists you can enable from the integrated Brave Ad Block page](#additional-lists-you-can-enable-from-the-integrated-brave-ad-block-page)

- `YousList`- To block various cosmetic stuff, aka annoyance in additional to above mentioned annoyances list. If you think this list is not enough use `Dandelion Sprout's Annoying Banners and Overlays List` instead.
- ONE single `language based` list, based for your own country.


Now we can improve specific things alias manually subscribing to addition lists, but which one make the most sense... The answer is easy, we want to get rid of additional extensions and hopefully we can archive it by using an additional list that supports the things we need, anti-coinmining, URL-shortener etc.


### [Optional filter-lists you could add](#optional-filter-lists-you-could-add)

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

## [Do not use portable Browsers](#do-not-use-portable-browsers)

Using portable Browsers has lots of security and privacy implications.

- In most cases the official Browser developer(s) do not provide any officially build, because of that people tend to use unofficial portable Browser repacks. Not often those repacks are done by fans and not experts and can possible contain tracking ads, Trojans, IP-grabbers etc.
- There is no verification, since you use unofficial Browser repacked versions you cannot verify anything yourself. Even if you use some repacks that are open source, you cannot verify something because the installer or the browser itself might be signed with different signatures that does not match the ones from the original manufacturer.
- No support, unofficial repack versions might not be approved nor directly supported from official site. This means they can be outdated after a short while, you already download an outdated version or the integrated update mechanism will fail because the updater depends on a service who check and delivers the actual update. Epic, MS etc Store will also not updating any portable versions.
- Running your Browser and profile on an unprotected drive that everyone can freely access is a privacy and security nightmare. There exist tools to quickly read out your Cookies, [passwords](https://www.nirsoft.net/utils/chromepass.html) and more, usually those tool need admin rights to access protected folders but if the profile folder is unprotected you can even read our or steal the database or the entire profile without admin rights. The internal protection regarding database passwords is weak and easy to crack in seconds, the Browser typically has no master password for the database as well as a Browser startup password check.
- You can workaround some of mentioned problems with a RamDrive or third-party Sandbox but the underlying issue is that it is overall by default easier for an attacker to extract, infect or compromise your Browser profile. Keep in mind that sandboxing trough external third-party apps can also be critical because the sandbox tool can be vulnerable or causes the Browser to crash because the Browser typically updates much more frequently that the sandbox tool needs to address. Another problem is that such workarounds might also require that such software is installed on the host, which needs admin rights. I am not aware of a sandbox solution that protects at low-level without admin rights, because this is what the OS requests to access inner rings.

----------------------------------------------------------

## [How Brave Browser handles Cookies](#how-brave-browser-handles-cookies)

Brave Browser is very well documented. Besides the source code and the wiki entries we have several good articles for beginners on how Brave actually handles the Cookie part.

- [Ephemeral Storage](https://brave.com/privacy-updates/7-ephemeral-storage/) + [Test](https://dev-pages.brave.software/storage/ephemeral-storage.html). This is the quinquevalent to Firefox [Dynamic First-Party Isolation](https://bugzilla.mozilla.org/show_bug.cgi?id=1625228) (dFPI) and [Total Cookie Protection](https://blog.mozilla.org/security/2021/02/23/total-cookie-protection/) mechanism.
- [Insight about how cookies are handled](https://github.com/brave/brave-browser/issues/16310#issuecomment-867269617)

[🔝 Back to top 🔝](#)

----------------------------------------------------------

## [Desktop Flags](#desktop-flags)

The official Brave release schedule can be found over [here](https://github.com/brave/brave-browser/wiki/Brave-Release-Schedule), the [archive is here](https://github.com/brave/brave-browser/wiki/Brave-Release-Schedule-Archive). There is currently no plan to release a Brave Browser version for SmartTV.


### [Desktop Security](#desktop-security)
Flag | Name | Enabled (✔️) / Disabled (❌) or/and Comment
-- | -- | --
[#block-insecure-private-network-requests](chrome://flags/#block-insecure-private-network-requests) | Block insecure private network requests |  ✔️
[#brave-domain-block](chrome://flags/#brave-domain-block) | Enable domain blocking | ✔️
[#brave-ephemeral-storage](chrome://flags/#brave-ephemeral-storage) | Enable Ephemeral Storage | ✔️
[#brave-vpn](chrome://flags/#brave-vpn) | Enable experimental Brave VPN (1.30.27+), the flag got removed but it will return | ✔️
[#disallow-doc-written-script-loads](chrome://flags/#disallow-doc-written-script-loads) | Block scripts loaded via document.write |  ✔️
[#enable-tls13-early-data](chrome://flags/#enable-tls13-early-data) | TLS 1.3 Early Data | ✔️
[#post-quantum-cecpq2](chrome://flags/#post-quantum-cecpq2) | TLS Post-Quantum Confidentiality |  ✔️
[#strict-extension-isolation](chrome://flags/#strict-extension-isolation) | Strict Extension Isolation | ✔️
[#strict-origin-isolation](chrome://flags/#strict-origin-isolation) | Strict-Origin-Isolation | ❌
[#sync-trusted-vault-passphrase-recovery](chrome://flags/#sync-trusted-vault-passphrase-recovery) | Enable sync trusted vault passphrase with improved recovery. | ❌
[#u2f-security-key-api](chrome://flags/#u2f-security-key-api) | Enable the U2F Security Key API | ❌

[🔝 Back to top 🔝](#)


### [Desktop Privacy](#desktop-privacy)
Flag | Name | Enabled (✔️) / Disabled (❌) or/and Comment
-- | -- | --
[#autofill-fill-merchant-promo-code-fields](chrome://flags/#autofill-fill-merchant-promo-code-fields) | Enable Autofill of promo code fields in forms | ❌
[#autofill-parse-merchant-promo-code-fields](chrome://flags/#autofill-parse-merchant-promo-code-fields) | Parse promo code fields in forms | ❌
[#brave-dark-mode-block](chrome://flags/#brave-dark-mode-block) | Enable dark mode blocking fingerprinting protection | ✔️ We enforce it for all Shield modes, otherwise it is only activated in aggressive mode.
[#brave-debounce](chrome://flags/#brave-debounce) | Enable debouncing (94.x+) | ✔️
[#brave-domain-block-1pes](chrome://flags/#brave-domain-block-1pes) | Enable domain blocking using First Party Ephemeral Storage | ✔️
[#brave-extension-network-blocking](chrome://flags/#brave-extension-network-blocking) | Enable extension network blocking | ✔️ (91+)
[#device-posture](chrome://flags/#device-posture) | Device Posture API | ❌
[#enable-accessibility-live-caption](chrome://flags/#enable-accessibility-live-caption) | Live Caption |❌ (90.x+) ⚠️[borked](https://github.com/brave/brave-browser/issues/15640)
[#enable-autofill-credit-card-authentication](chrome://flags/#enable-autofill-credit-card-authentication) | Allow using platform authenticators to retrieve server cards | ❌ (87.x+)
[#enable-fenced-frames](chrome://flags/#enable-fenced-frames) | Enable the <fencedframe> element. | ✔️ with ShadowDOM
[#enable-generic-sensor-extra-classes](chrome://flags/#enable-generic-sensor-extra-classes) | Generic Sensor Extra Classes | ❌
[#enable-payment-request-basic-card](chrome://flags/#enable-payment-request-basic-card) | PaymentRequest API 'basic-card' method | ❌
[#enable-quic](chrome://flags/#enable-quic) | Experimental QUIC protocol | ✔️ Needed for HTTP3/DoQ, now known as [RFC 9000](https://www.fastly.com/blog/quic-is-now-rfc-9000)
[#extensions-menu-access-control](chrome://flags/#extensions-menu-access-control) | Extensions Menu Access Control | ✔️
[#font-access](chrome://flags/#font-access) | Font Access APIs | ❌
[#force-major-version-to-100](chrome://flags/#force-major-version-to-100) | [#force-major-version-to-100](https://blog.chromium.org/2021/10/chrome-96-beta-conditional-focus.html) | ❌
[#ntp-cache-one-google-bar](chrome://flags/#ntp-cache-one-google-bar) | Cache OneGoogleBar | ❌
[#omnibox-dynamic-max-autocomplete](chrome://flags/#omnibox-dynamic-max-autocomplete) | Omnibox Dynamic Max Autocomplete | ❌ (_causes lags if enabled / 5+_)
[#omnibox-pedals-batch2](chrome://flags/#omnibox-pedals-batch2) | Omnibox Pedals batch 2 | ❌
[#omnibox-rich-autocompletion-promisin](chrome://flags/#omnibox-rich-autocompletion-promisin) | Omnibox Rich Autocompletion Promising | ❌
[#partitioned-cookies](chrome://flags/#partitioned-cookies) | Partitioned Cookies | ✔️
[#privacy-review](chrome://flags/#privacy-review) | Privacy Review (93.1.31.39+) | ✔️
[#reduce-user-agent](chrome://flags/#reduce-user-agent) | Reduce User-Agent request header | ✔️
[#system-keyboard-lock](chrome://flags/#system-keyboard-lock) | Experimental system keyboard lock | ❌ (89.x+)
[#webxr-incubations](chrome://flags/#webxr-incubations) | WebXR Incubations | ❌ (92.0+)

[🔝 Back to top 🔝](#)


### [Desktop Performance](#desktop-performance)

Benchmarks against Edge and Firefox are pretty much useless. There are multiple reasons why, please see below:
- Synthetic benchmarks might not reflect real-world performance because a normal website is not a benchmark suite, other factors can here the individual and subjective Browser performance.
- Brave’s blocking and privacy protections require a fixed amount of additional work per page and frame. This means that Brave will do worse in synthetic benchmarks than other browsers (since Brave’s privacy protections won’t be useful in benchmark tests), but will do better on real world sites.
- Firefox and Edge do not have any integrated ad-blocker, they use safe-browsing, which is also included in all Chromium based Browsers and enabled by default.
- Firefox and Edge do not include any crypto wallets.
- [Brave reduces the page load performance cost of its ad-blocker](https://www.ctrl.blog/entry/brave-ab-performance.html).
- [Benchmarks, are often outdated pretty fast](https://old.reddit.com/r/Android/comments/kxg8gh/android_browser_benchmark_tests/). At best this is a snapshot of the current state but every Browser evolves, fixes stuff etc.


Flag | Name | Enabled (✔️) / Disabled (❌) or/and Comment
-- | -- | --
[#brave-adblock-cookie-list-default](chrome://flags/#brave-adblock-cookie-list-default) | Treat 'Easylist-Cookie List' as a default list source | ✔️
[#brave-rewards-verbose-logging](chrome://flags/#brave-rewards-verbose-logging) | Enable Brave Rewards verbose logging | ❌ enabled by default since 1.25.68+
[#enable-parallel-downloading](chrome://flags/#enable-parallel-downloading) | Parallel downloading | ✔️
[#enable-prerender2](chrome://flags/#enable-prerender2) | Prerender2 | ✔️ (90.x+)
[#enable-throttle-display-none-and-visibility-hidden-cross-origin-iframes](chrome://flags/#enable-throttle-display-none-and-visibility-hidden-cross-origin-iframes) | Throttle non-visible cross-origin iframes | ✔️
[#enable-vulkan](chrome://flags/#enable-vulkan) | Use Vulkan as the graphics backend. | ✔️ On Linux either Vulkan or raw draw, if you enable both it will prefer raw draw to avoid compatibility issues.
[#restrict-websockets-pool](chrome://flags/#restrict-websockets-pool) | Restrict WebSockets pool | ✔️ (97.x+)
[#throttle-foreground-timers](chrome://flags/#throttle-foreground-timers) | Throttle Foreground Timers to 30 Hz | ✔️

[🔝 Back to top 🔝](#)


### [Desktop Functionality / Usability](#desktop-functionality--usability)
Flag | Name | Enabled (✔️) / Disabled (❌) or/and Comment
-- | -- | --
[#brave-adblock-cname-uncloaking](chrome://flags/#brave-adblock-cname-uncloaking) | Enable CNAME uncloaking | ✔️ 91.1.27.36 (This will become obsolete and enabled by default once fully stable and merged into shields directly)
[#brave-adblock-redirect-url](chrome://flags/#brave-adblock-redirect-url) | Enable support for $redirect-url filter option for adblock rules | ✔️
[#brave-cosmetic-filtering-sync-load)](chrome://flags/#brave-cosmetic-filtering-sync-load) | Enable sync loading of cosmetic filter rules | ✔️
[#brave-talk](chrome://flags/#brave-talk) | Enable Brave Talk | ✔️
[#chrome-whats-new-ui](chrome://flags/#chrome-whats-new-ui) | Show Chrome What's New page at `chrome://whats-new` (93.x+) | ❌
[#colr-v1-fonts](chrome://flags/#colr-v1-fonts) | COLR v1 Fonts | ✔️
[#enable-force-dark](chrome://flags/#enable-force-dark) | Force Dark Mode for Web Contents | ✔️ `increase text contrast`
[#enable-jxl](chrome://flags/#enable-jxl) | Enable [JXL image format ](https://jpeg.org/jpegxl/) | ✔️ (Chrome 91.1.x+)
[#extension-workflow-justification](chrome://flags/#extension-workflow-justification) | Extension request justification (93.x+) | ✔️
[#force-color-profile](chrome://flags/#force-color-profile) | Force color profile | ✔️[scRBG](https://en.wikipedia.org/wiki/ScRGB) or [HDR](https://en.wikipedia.org/wiki/High_Dynamic_Range_(display_and_formats)#Description) (if your Monitor supports HDR enable the HDR option)
[#forced-colors](chrome://flags/#forced-colors) | Forced Colors | ✔️
[#history-journeys-omnibox-action](chrome://flags/#history-journeys-omnibox-action) | History Journeys Omnibox Action | ✔️ (Chrome 97+)
[#history-journeys](chrome://flags/#history-journeys) | History Journeys | ✔️ (Chrome 98+)
[#media-session-webrtc](chrome://flags/#media-session-webrtc) | Enable WebRTC actions in Media Session (93.x+) | ✔️
[#omnibox-keyword-space-triggering-setting](chrome://flags/#omnibox-keyword-space-triggering-setting) | Omnibox Keyword Space Triggering Setting | ✔️
[#page-info-about-this-site](chrome://flags/#page-info-about-this-site) | About this Site in Page Info | ✔️
[#page-info-history-desktop](chrome://flags/#page-info-history-desktop) | Page info history | ✔️ (Chrome 97+)
[#playback-speed-button](chrome://flags/#playback-speed-button) | Playback Speed Button | ✔️
[#scrollable-tabstrip](chrome://flags/#scrollable-tabstrip) | Tab Scrolling | ✔️ (tabs shrink to a medium width)
[#shared-highlighting-v2](chrome://flags/#shared-highlighting-v2) | Shared Highlighting 2.0 | ✔️ (Chrome 90.x+)
[#sharing-hub-desktop-app-menu](chrome://flags/#sharing-hub-desktop-app-menu) | Desktop Sharing Hub in App Menu | ✔️ (Chrome 91+)
[#sharing-hub-desktop-omnibox](chrome://flags/#sharing-hub-desktop-omnibox) | Desktop Sharing Hub in Omnibox | ✔️ (Chrome 91+)

[🔝 Back to top 🔝](#)


### [Desktop Scrolling](#desktop-scrolling)
Flag | Name | Enabled (✔️) / Disabled (❌) or/and Comment
-- | -- | --
[#percent-based-scrolling](chrome://flags/#percent-based-scrolling) | Percent-based Scrolling | ✔️
[#smooth-scrolling](chrome://flags/#smooth-scrolling) | Smooth Scrolling | ✔️

[🔝 Back to top 🔝](#)


### [Desktop PWA](#desktop-pwa)
Flag | Name | Enabled (✔️) / Disabled (❌) or/and Comment
-- | -- | --
[#enable-desktop-pwas-elided-extensions-menu](chrome://flags/#enable-desktop-pwas-elided-extensions-menu) | Desktop PWAs elided extensions menu | ✔️
[#enable-desktop-pwas-launch-handler](chrome://flags/#enable-desktop-pwas-launch-handler) | Desktop PWA launch handler | ✔️
[#enable-desktop-pwas-notification-icon-and-title](chrome://flags/#enable-desktop-pwas-notification-icon-and-title) | Desktop PWAs improvements in notification icon and title | ✔️
[#enable-desktop-pwas-prefix-app-name-in-window-title](chrome://flags/#enable-desktop-pwas-prefix-app-name-in-window-title) | Desktop PWAs prefix window title with app name. | ✔️
[#enable-desktop-pwas-remove-status-bar](chrome://flags/#impulse-scroll-animations) | Desktop PWAs remove status bar | ✔️
[#enable-desktop-pwas-sub-apps](chrome://flags/#enable-desktop-pwas-sub-apps) | Desktop PWA Sub Apps | ✔️
[#enable-desktop-pwas-tab-strip-settings](chrome://flags/#enable-desktop-pwas-tab-strip-settings) | Desktop PWA tab strips settings | ✔️
[#enable-desktop-pwas-web-bundles](chrome://flags/#enable-desktop-pwas-web-bundles) | Desktop PWAs Web Bundles | ✔️
[#enable-desktop-pwas-window-controls-overlay](chrome://flags/#enable-desktop-pwas-window-controls-overlay) | Desktop PWA Window Controls Overlay | ✔️
[#pwa-update-dialog-for-name-and-icon](chrome://flags/#pwa-update-dialog-for-name-and-icon) | Enable PWA install update dialog for name/icon changes | ✔️

[🔝 Back to top 🔝](#)


### [Desktop Brave Reader Mode / Speedreader](#desktop-brave-reader-mode--speedreader)
Flag | Name | Enabled (✔️) / Disabled (❌) or/and Comment
-- | -- | --
[#enable-reader-mode](chrome://flags/#enable-reader-mode) | Enable Reader Mode | ✔️ Enabled available in settings (_we enforce it_, optional)

[🔝 Back to top 🔝](#)

--------------------

## [Android (mobile) Flags](#android-mobile-flags)

### [Mobile Security](#mobile-security)
Flag | Name | Enabled (✔️) / Disabled (❌) or/and Comment
-- | -- | --
[#block-insecure-private-network-requests](chrome://flags/#block-insecure-private-network-requestst) | Block insecure private network requests. | ✔️
[#brave-ephemeral-storage](chrome://flags/#brave-ephemeral-storage) | Enable Ephemeral Storage | ✔️
[#brave-vpn](chrome://flags/#brave-vpn) | Enable experimental Brave VPN (1.30.27+), the flag got removed but it will return | ✔️
[#disallow-doc-written-script-loads](chrome://flags/#disallow-doc-written-script-loads) | Block scripts loaded via document.write |  ✔️
[#enable-site-isolation-for-password-sites](chrome://flags/#enable-site-isolation-for-password-sites) | Enable site Isolation for Password Sites | ✔️
[#enable-site-per-process](chrome://flags/#enable-site-per-process) | [Part of Site isolation](https://www.chromium.org/Home/chromium-security/site-isolation/) | ✔️
[#post-quantum-cecpq2](chrome://flags/#post-quantum-cecpq2) | TLS Post-Quantum Confidentiality | ✔️
[#strict-origin-isolation](chrome://flags/#strict-origin-isolation) | Strict-Origin-Isolation | ❌
[#sync-trusted-vault-passphrase-recovery](chrome://flags/#sync-trusted-vault-passphrase-recovery) | Enable sync trusted vault passphrase with improved recovery | ❌

[🔝 Back to top 🔝](#)


### [Mobile Privacy](#mobile-privacy)
Flag | Name | Enabled (✔️) / Disabled (❌) or/and Comment
-- | -- | --
[#autofill-fill-merchant-promo-code-fields](chrome://flags/#autofill-fill-merchant-promo-code-fields) | Enable Autofill of promo code fields in forms | ❌
[#autofill-parse-merchant-promo-code-fields](chrome://flags/#autofill-parse-merchant-promo-code-fields) | Parse promo code fields in forms | ❌
[#brave-dark-mode-block](chrome://flags/#brave-dark-mode-block) | Enable dark mode blocking fingerprinting protection | ✔️ We enforce it for all Shield modes, otherwise it is only activated in aggressive mode.
[#brave-debounce](chrome://flags/#brave-debounce) | Enable debouncing (94.x+) | ✔️
[#brave-domain-block-1pes](chrome://flags/#brave-domain-block-1pes) | Enable domain blocking using First Party Ephemeral Storage | ✔️
[#continuous-search](chrome://flags/#continuous-search) | Continues Search | ❌
[#device-posture](chrome://flags/#device-posture) | Device Posture API | ❌
[#enable-autofill-credit-card-authentication](chrome://flags/#enable-autofill-credit-card-authentication) | Allow using platform authenticators to retrieve server cards | ❌ (87.x+)
[#enable-commerce-price-tracking](chrome://flags/#enable-commerce-price-tracking) | Price Tracking | ❌ Connections to Google and partners + market influence and manipulation. It is better and more privacy-friendly to trust independent retailers and engine-crawlers such as Geizhals, Mindfactory etc.
[#enable-fenced-frames](chrome://flags/#enable-fenced-frames) | Enable the <fencedframe> element. | ✔️ with ShadowDOM, on older Android versions prior 9 set this to Enabled otherwise you might get Browser crashes.
[#enable-generic-sensor-extra-classes](chrome://flags/#enable-generic-sensor-extra-classes) | Generic Sensor Extra Classes | ❌
[#enable-quic](chrome://flags/#enable-quic) | Enable QUIC Protocol | ✔️ (Brave filters controversial APIs)
[#enable-payment-request-basic-card](chrome://flags/#enable-payment-request-basic-card) | PaymentRequest API 'basic-card' method | ❌
[#force-major-version-to-100](chrome://flags/#force-major-version-to-100) | [#force-major-version-to-100](https://blog.chromium.org/2021/10/chrome-96-beta-conditional-focus.html) | ❌
[#font-access](chrome://flags/#font-access) | Font Access APIs | ❌
[#google-mobile-services-passwords](chrome://flags/#google-mobile-services-passwords) | Google Mobile Services for Passwords | ❌
[#incognito-screenshot](chrome://flags/#incognito-screenshot) | Allow Incognito Screenshots | ❌
[#large-favicon-from-google](chrome://flags/#large-favicon-from-google) | Large favicons from Google | ❌
[#omnibox-assistant-voice-search](chrome://flags/#omnibox-assistant-voice-search) | Omnibox Voice Search Assistant | ❌
[#partitioned-cookies](chrome://flags/#partitioned-cookies) | Partitioned Cookies | ✔️
[#reduce-user-agent](chrome://flags/#reduce-user-agent) | Reduce User-Agent request header | ✔️
[#related-searches-in-bar](chrome://flags/#related-searches-in-bar) | Enables showing Related Searches in the peeking bar. | ❌ disabled to avoid search engine ping backs
[#wallet-service-use-sandbox](chrome://flags/#wallet-service-use-sandbox) | Wallet Services uses Google's Sandbox | ❌Connects to some Google Endpoints.
[#webxr-incubations](chrome://flags/#webxr-incubations) | WebXR Incubations | ❌ (92.0+)

[🔝 Back to top 🔝](#)


### [Mobile PWA](mobile-pwa)
Flag | Name | Enabled (✔️) / Disabled (❌) or/and Comment
-- | -- | --
[#messages-for-android-pwa-install](chrome://flags/#messages-for-android-pwa-install) | PWA Installation Messages UI | ✔️
[#pwa-update-dialog-for-name-and-icon](chrome://flags/#pwa-update-dialog-for-name-and-icon) | Enable PWA install update dialog for name/icon changes | ✔️

[🔝 Back to top 🔝](#)


### [Mobile Performance](#mobile-performance)
Flag | Name | Enabled (✔️) / Disabled (❌) or/and Comment
-- | -- | --
[#back-forward-cache](chrome://flags/#back-forward-cache) | Back and forward Cache | ✔️
[#brave-adblock-cookie-list-default](chrome://flags/#brave-adblock-cookie-list-default) | Treat 'Easylist-Cookie List' as a default list source | ✔️
[#canvas-oop-rasterization](chrome://flags/#canvas-oop-rasterization) | Out-of-process 2D canvas rasterization. | ✔️ enable it on Android 10+
[#chrome-share-long-screenshot](chrome://flags/#chrome-share-long-screenshot) | N/A | ❌
[#contextual-search-debug](chrome://flags/#contextual-search-debug) | Contextual Search Debug | ❌
[#contextual-search-longpress-resolve](chrome://flags/#contextual-search-longpress-resolve) | N/A | ❌
[#contextual-search-translation](chrome://flags/#contextual-search-translation) | N/A | ❌
[#enable-drdc](chrome://flags/#enable-drdc) | Enables Display Compositor to use a new gpu thread. | ✔️ enable it on Android 10+
[#enable-gpu-rasterization](chrome://flags/#enable-gpu-rasterization) | GPU rasterization | ✔️ enable it on Android 10+
[#enable-instant-start](chrome://flags/#enable-instant-start) | Instant start | ✔️
[#enable-parallel-downloading](chrome://flags/#enable-parallel-downloading) | Parallel downloading | ✔️
[#enable-prerender2](chrome://flags/#enable-prerender2) | Prerender2 | ✔️ (90.x+)
[#enable-throttle-display-none-and-visibility-hidden-cross-origin-iframes](chrome://flags/#enable-throttle-display-none-and-visibility-hidden-cross-origin-iframes) | Throttle non-visible cross-origin iframes | ✔️
[#restrict-websockets-pool](chrome://flags/#restrict-websockets-pool) | Restrict WebSockets pool | ✔️ (97.x+)
[#smooth-scrolling](chrome://flags/#smooth-scrolling) | Smooth Scrolling | ✔️
[#throttle-foreground-timers](chrome://flags/#throttle-foreground-timers) | Throttle Foreground Timers to 30 Hz | ✔️

[🔝 Back to top 🔝](#)


### [Mobile Functionality / Usability](#mobile-functionality--usability)
Flag | Name | Enabled (✔️) / Disabled (❌) or/and Comment
-- | -- | --
[#android-picture-in-picture-api](chrome://flags/#android-picture-in-picture-api) | Picture in Picture Web API for Android | ✔️
[#brave-adblock-cname-uncloaking](chrome://flags/#brave-adblock-cname-uncloaking) | Enable CNAME uncloaking | ✔️ 91.1.27.36 (This will become obsolete and enabled by default once fully stable and merged into shields directly)
[#brave-adblock-redirect-url](chrome://flags/#brave-adblock-redirect-url) | Enable support for $redirect-url filter option for adblock rules | ✔️
[#brave-cosmetic-filtering-sync-load)](chrome://flags/#brave-cosmetic-filtering-sync-load) | Enable sync loading of cosmetic filter rules | ✔️
[#context-menu-google-lens-chip](chrome://flags/#context-menu-google-lens-chip) | Google Lens powered image search for surfaced as a chip below the context menu. | ❌
[#context-menu-search-with-google-lens](chrome://flags/#context-menu-search-with-google-lens) | Google Lens powered image search in the context menu. | ❌
[#context-menu-shop-with-google-lens](chrome://flags/#context-menu-shop-with-google-lens) | Google Lens powered image search for shoppable images in the context menu. | ❌
[#context-menu-translate-with-google-lens](chrome://flags/#context-menu-translate-with-google-lens) | Google Lens powered image search for translatable images surfaced as a chip under the context menu. | ❌
[#continuous-search](chrome://flags/#continuous-search) | Continuous Search | ✔️
[#darken-websites-checkbox-in-themes-setting](chrome://flags/#darken-websites-checkbox-in-themes-setting) | Darken Websites checkbox in Theme settings | ✔️
[#enable-force-dark](chrome://flags/#enable-force-dark) | Force Dark Mode for Web Contents | ✔️ `increase text contrast`
[#enable-jxl](chrome://flags/#enable-jxl) | Enable [JXL image format ](https://jpeg.org/jpegxl/) | ✔️ (Chrome 91.1.x+)
[#enable-quick-action-search-widget-android](chrome://flags/#enable-quick-action-search-widget-android) | [Quick Search Widget](https://www.androidpolice.com/2021/06/29/chrome-for-android-is-rediscovering-widgets-now-that-apple-made-them-hot-again/) | ✔️
[#google-lens-sdk-intent](chrome://flags/#google-lens-sdk-intent) | Enable the use of the Lens SDK when starting intent into Lens. | ❌
[#media-session-webrtc](chrome://flags/#media-session-webrtc) | Enable WebRTC actions in Media Session (93.x+) | ✔️
[#messages-for-android-ads-blocked](chrome://flags/#messages-for-android-ads-blocked) | Ads Blocked Messages UI | ✔️
[#messages-for-android-permission-update](chrome://flags/#messages-for-android-permission-update) | Permission Update Messages UI | ✔️
[#messages-for-android-reader-mode](chrome://flags/#messages-for-android-reader-mode) | Reader Mode Messages UI | ✔️
[#page-info-about-this-site](chrome://flags/#page-info-about-this-site) | About this Site in Page Info | ✔️
[#photo-picker-video-support](chrome://flags/#photo-picker-video-support) | Photo Picker Video Support | ✔️ (with animated thumbnails)
[#playback-speed-button](chrome://flags/#playback-speed-button) | Playback Speed Button | ✔️
[#shared-highlighting-v2](chrome://flags/#shared-highlighting-v2) | Shared Highlighting 2.0 | ✔️ (Chrome 90.x+)
[#shopping-list](chrome://flags/#shopping-list) | Shopping List | ❌ can create problems with Sync and working with Bookmarks is a PITA in Chrome in general, hopefully Brave gets a Widget for this one day.
[#voice-button-in-top-toolbar](chrome://flags/#voice-button-in-top-toolbar) | Voice Button in Top Toolbar | ❌ The reason why Voice function will never work is that Google prevents using alternative services, so we disable it.

[🔝 Back to top 🔝](#)


### [Brave only specific flags (not needed to be enforced)](#brave-only-specific-flags-not-needed-to-be-enforced)
Flag | Name | Comment
-- | -- | --
[#brave-adblock-cosmetic-filtering](chrome://flags/#brave-adblock-cosmetic-filtering) | Enable cosmetic filtering | Enabled by default even if it only shows "default"
[#brave-adblock-csp-rules](chrome://flags/#brave-adblock-csp-rules) | Enable support for CSP rules | Not need to be enforced (since 1.25.68+)
[#brave-ads-allowed-to-fallback-to-custom-push-notification-ads](chrome://flags/#brave-ads-allowed-to-fallback-to-custom-push-notification-ads) | Allow Brave Ads to fallback from native to custom push notifications | This is OS specific and in the future will be obsolete since Brave will detect the OS and then automatically fallback to the legacy system.
[#brave-decentralized-dns](chrome://flags/#brave-decentralized-dns) | Enable Decentralized DNS | ✔️ This is now a settings point under Browser Settings since v95+ which you can easily switch.
[#brave-news](chrome://flags/#brave-news) | Enable Brave News | Your own decision to enable it or not, it is a global switch.
[#enable-lens-region-search](chrome://flags/#enable-lens-region-search) | Search your screen with Google Lens (93.1.31.39+), since 1.36.112 it is disabled by default. | ❌
[#enable-webrtc-hide-local-ips-with-mdns](chrome://flags/#enable-webrtc-hide-local-ips-with-mdns) | This is not Brave only specific but there are two ways how Brave handles it, [via Shields or Setting](https://avoidthehack.com/webrtc-leaks-how-to-fix) | Do not enforce it via flag

[🔝 Back to top 🔝](#)


## [Default Fonts](#default-fonts)

By default Brave Browser uses `Poppins` and `Muli` for the content you see around the web, those mentioned fonts are not the default fonts to render the actual content. 

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


## [Reference for the Brave vs. Browser X discussion](#reference-for-the-brave-vs-browser-x-discussion)
- [Browser Startup Comparison (netmeister.org)](https://www.netmeister.org/blog/browser-startup.html) and [Braves own inspection (brave.com)](https://brave.com/popular-browsers-first-run/)
- [Browser privacy analyzed (tcd.ie) [pdf]](https://www.scss.tcd.ie/Doug.Leith/pubs/browser_privacy.pdf)
- [Firefox and Chromium (madaidans-insecurities.github.io)](https://madaidans-insecurities.github.io/firefox-chromium.html)
- [Goggles: Democracy dies in darkness, and so does the Web (brave.com) [pdf]](https://brave.com/wp-content/uploads/2021/03/goggles.pdf)
- [How to find the most secure browsers (onlinesecurityworld.com)](https://onlinesecurityworld.com/how-to-find-the-most-secure-browsers/)
- [Mozilla's position on specific web standards (mozilla.github.io)](https://mozilla.github.io/standards-positions/)
- [The Security Architecture of the Chromium Browser (seclab.stanford.edu)](https://seclab.stanford.edu/websec/chromium/chromium-security-architecture.pdf)
- [Update on Brave’s Ongoing Direct Mail Marketing Campaign (reddit.com)](https://old.reddit.com/r/brave_browser/comments/t4gzuw/update_on_braves_ongoing_direct_mail_marketing/)

[🔝 Back to top 🔝](#)
