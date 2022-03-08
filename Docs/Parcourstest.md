## [Parcourstest](#parcourstest)

Here are the tests the Browser (Desktop/Mobile) needs to pass. This needs to be done so that we know the flag/changes we done do not influence (negatively) the Browser in a way we do not want. [Privacytests.org](https://privacytests.org/) provides a solid but not perfect overview of what is currently covered with the DEFAULT Brave Browser settings and shield settings. Test results variate a lot with changed shield settings as well as changed flags and settings.


This is my own test setup.


- All: `brave://interstitials/` must pass (contains all sub-resources to test security, privacy etc.), there ae bunch of others like e.g. `chrome://floc-internals/` but they are not relevant since the source for this got removed.
- Performance: [Input lag test (basro.github.io)](https://basro.github.io/input-lag-measuring-tool), needs to pass 90+ Hz check (your monitor/device needs to support it) on some Android ROMs you need to enforce the [refresh rate manually (androidcentral.com)](https://www.androidcentral.com/how-change-your-phones-resolution-and-refresh-rate) (or use an [app (forum.xda-developers.com)](https://forum.xda-developers.com/t/app-galaxy-max-hz-refresh-rate-control-quick-resolution-switcher-screen-off-mods-adaptive-mod-keep-high-adaptive-on-power-saving-mode-and-more.4181447/) and unlock [fps (forum.xda-developers.com)](https://forum.xda-developers.com/t/mod-increase-frames-per-second-5-14-15.3108786/))
- Privacy: [Browser IP leak (browserleaks.com)](https://browserleaks.com/ip), needs to pass in Tor + Incognito mode
- Privacy: Cloaked CNAMEs _check_ against a real world website e.g. [https://publicwww.com/websites/EA_data/](https://publicwww.com/websites/EA_data/) Brave shields must block `https://seomon.com/piwik/matomo.js`.
- Browser platform test: [Web Platform Tests (web-platform-tests.org)](https://web-platform-tests.org/), needs to pass
- Privacy: [FLoC (github.com)](https://github.com/brave/brave-browser/issues/14942), needs to pass (check against a website which supports it e.g. https://web.archive.org/)
- Security: [Schemeflood (schemeflood.com)](https://schemeflood.com/), needs to fully pass.
- Privacy: [Font Fingerprinting test (amiunique.org)](https://amiunique.org/fp), see [here (github.com)](https://github.com/brave/brave-browser/issues/816)
- Privacy: [window.Intl.DateTimeFormat() API (developer.mozilla.org)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Intl/DateTimeFormat/DateTimeFormat#Parameters), see [here (github.com)](https://github.com/brave/brave-browser/issues/8574)
- Privacy: [Dark Mode detection (github.com)](https://github.com/brave/brave-browser/issues/15265), needs to pass
- Privacy: `Clear Data on Exit` must be enabled and enforced by default
- Privacy: [HSTS fingerprinting (github.com)](https://github.com/pastly/satis-hsts-tracking), needs to pass, [read how it works (usenix.org)](https://www.usenix.org/system/files/conference/foci18/foci18-paper-syverson.pdf) and [how to protect yourself (webkit.org)](https://webkit.org/blog/8146/protecting-against-hsts-abuse/) - Shields set to "aggressive" & cookies blocked (by default must be enabled)
- Privacy: Do Not Track must be disabled (default), its [useless (boingboing.net)](https://boingboing.net/2018/10/17/no-call-list.html) and enabling it [results in more fingerprinting (w3.org)](https://www.w3.org/2011/track-privacy/papers/Soghoian.pdf)
- Privacy: [Cover your Tracks (coveryourtracks.eff.org)](https://coveryourtracks.eff.org/about), needs to pass (fonts and GL / canvas fingerprints randomized) - The site is misleading, because it can only detect a unique fingerprint within your session. You can test this if you try running the test and making note of the actual fingerprint ID, after that, restart your browser and run the test again. Compare the two fingerprint IDs. If they're the same, your fingerprint is persisting across sessions, which is problematic. The website doesn't show you your actual fingerprint ID, so you have to go to [browserleaks.com/canvas (browserleaks.com)](https://browserleaks.com/canvas) and scroll down to the "Your Fingerprint" section, and you'll see your fingerprint ID (signature).
- Privacy: [3rd party cookie bypass (xsid-demo.glitch.me)](https://xsid-demo.glitch.me/5wmt9tz.html), needs to pass ("Block third-party cookies" must be enabled [default]).
- Privacy: [Does your browser have TablesNG? (tablesng.com)](https://tablesng.com/), do not need to pass because the fingerprint vector for this is none existing. But it indicates if your flag with TablesNG worked or not (only interesting for nightly users).
- Privacy: [SameSite 🍪 sandbox (samesite-sandbox.glitch.me)](https://samesite-sandbox.glitch.me/), needs to pass
- Privacy: [is-chrome-100-yet.glitch.me (is-chrome-100-yet.glitch.me)](https://is-chrome-100-yet.glitch.me/) must return: NO which is always the case because we never use not enforce `#force-major-version-to-100`.
- Functionality: [webcamtests (webcamtests.com)](https://webcamtests.com/), Webcam Test Web Utility must show a picture in case you use and plugged in your webcam. Since we blocked the webcam permission by default, you need to unlock that permission first for the website. Do not add an general exclusion to the permission page. This then also tests if it really blocks the cam permission or not each time we revisit the page.
- Security: [XSinator – XS-Leak Browser Test Suite (xsinator.com)](https://xsinator.com/), needs to pass, this will not happen this year but this is a long-time goal.


Official Test:

The official [Brave QA Test Pages are here (dev-pages.brave.software)](https://dev-pages.brave.software/index.html).

[🔝 Back to top 🔝](#)
