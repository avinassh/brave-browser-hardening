[[_TOC_]]


### [Desktop outdated, removed or integrated/replaced](#desktop-outdated-removed-or-integratedreplaced)
Flag | Name | Disabled since or comment
-- | -- | --
[#brave-speedreader](chrome://flags/#brave-speedreader) | Enable SpeedReader | ✔️ This is now a settings point under Browser Settings since v95+ which you can easily switch.
`N/A` | Enable Tab Search (the little arrow down icon to search trough tabs) | Chrome 90, to disable it you can use `-disable-features=TabSearch`, an option to disable it is [planned](https://github.com/brave/brave-browser/issues/16007).
`#enable-experimental-fling-animation` | Enable experimental fling animation (enabled) | Chrome 91+
`#vertical-tabs` | Vertical tabs (enabled) | Implemented in Brave 91+ - Menu allows multiple states, hide on click, on/off etc.
`#pdf-viewer-update` | PDF Viewer Update (enabled) | Chrome 91+
`N/A` | Cookies without SameSite must be secure (enabled) | Chrome 91+
`N/A` | SameSite by default cookies (enabled) | Chrome 91+
`N/A` | Anonymize local IPs exposed by WebRTC (enabled) | Chrome 91+
`N/A` | Show enhanced protection message in security interstitials (enabled) | Chrome 90+
`#storage-access-api` | Storage Access API | Chrome 90+
`N/A` | Treat risky downloads over insecure connections as active mixed content (enabled) | Chrome 90+, default in 91+ (no visible option)
`Multiple flags` | Every `image lazy loading` flag | Enabled, but caused too much problems
`N/A` | Load media router component (disabled) | Chrome 89+
`N/A` | Force empty CORB and CORS allowlist (enabled) | Chrome 89+
`N/A` | Load media router component (disabled) | By default removed by Brave (Chrome 89+)
`N/A` | Background Push Notifications (disabled) | Push replaced/tunneled(Chrome 89+)
`N/A` | Enable On-Demand Media Router Extension (disabled) | Chrome 89+
`N/A` | Toast Notification Background Task Event Handlers (disabled) | Chrome 89+
`N/A` | Enable Share Targets (disabled) | Chrome 89+
`#use-sync-sandbox ` | Use Chrome Sync Sandbox (disabled) | Brave enforces disabled as default state (metadata).
`#global-media-controls-for-chromeos` | Global Media Controls for ChromeOS | ChromeOS 90 (default)
`N/A` | screen-capture (disabled) | Default with Chrome 89+
`#scanning-ui` | Scanning UI | Enabled by default in Chrome 90+
`#app-service-adaptive-icons` | Adaptive Icons | Replaced in Chrome 90+
`#enable-holding-space` | Holding Space API | Replaced with Chrome 90+
`#holding-space-previews` | Space Previews | Disabled by default in Chrome 90+
`#enhanced_clipboard` | Enhanced Clipboard | Removed with Chrome 89+
`#ash-limit-alt-tab-to-active-desk` | Activate Tab limit | Removed with Chrome 88+
`#ash-limit-shelf-items-to-active-desk` | N/A | Default in Chrome 90+ (removed, no visible option)
`#enable-auto-select` | Enable Auto Select | Default integrated since Chrome 89+
`#force-preferred-interval-for-video` | Force preferred Internal Video | Default in Chrome 89+ (removed, no visible option)
`#files-filters-in-recents` |  Filter files in Recents | Obsolete with Chrome 89+
`#copy-link-to-text` | Copy link to Text | [Disabled with Brave 1.31.87](https://github.com/brave/brave-browser/issues/17994)
`#enable-accessibility-live-caption` | Enable Accessibility Live Caption (disabled) | Broken in Chrome 89, pulls data from Google
`N/A` | Allow all sites to initiate mirroring (disabled) | Removed with Chrome 88+
`N/A` | Enable Share Targets (disabled) | Disabled in Chrome 89+
[#turn-off-streaming-media-caching-always](chrome://flags/#turn-off-streaming-media-caching-always) |  Turn off caching of streaming media to disk (Chrome 92+) | ✔️
[#turn-off-streaming-media-caching-on-battery](chrome://flags/#turn-off-streaming-media-caching-on-battery) | Turn off caching of streaming media to disk while on battery power. (Chrome 91+) | ✔️
[#enable-new-contacts-picker](chrome://flags/#enable-new-contacts-picker) | Enables the new contacts picker | ✔️
[#enable-new-photo-picker](chrome://flags/#enable-new-photo-picker) | Enables the new photo picker | ✔️
[#enable-ftp](chrome://flags/#enable-ftp) | Enable FTP | FTP support was removed in Chrome 95+.
[#sync-compromised-credentials](chrome://flags/#sync-compromised-credentials) | Syncing of Security Issues | ❌
[#brave-adblock-default-1p-blocking](chrome://flags/#brave-adblock-default-1p-blocking) | Shields first-party network blocking (1.30.27+) | ✔️
[#brave-dark-mode-block](chrome://flags/#brave-dark-mode-block) | Enable dark mode blocking fingerprinting protection (1.30.27+), the settings depends now on Shield settings | ✔️
[#omnibox-short-bookmark-suggestions](chrome://flags/#omnibox-short-bookmark-suggestions) | Omnibox short bookmark suggestions | ❌
[#omnibox-tab-switch-suggestions](chrome://flags/#omnibox-tab-switch-suggestions) | Omnibox switch to tab suggestions | ❌ (_Omnibox calls to Google Backend for Beacon, Statistics etc._)
[#omnibox-pedal-suggestions](chrome://flags/#omnibox-pedal-suggestions) | Omnibox Pedal suggestions | ❌
[#schemeful-same-site](chrome://flags/#schemeful-same-site) | Schemeful Same-Site | ✔️
[#brave-permission-lifetime](chrome://flags/#brave-permission-lifetime) | Permission Lifetime | ✔️ (91+)
[#safe-browsing-real-time-url-lookup-enterprise-ga-endpoint](chrome://flags/#safe-browsing-real-time-url-lookup-enterprise-ga-endpoint) | Use the new GA endpoint to perform enterprise real time URL check. | ❌
[#clear-cross-browsing-context-group-main-frame-name](chrome://flags/#clear-cross-browsing-context-group-main-frame-name) | [Clear window name in top-level cross-browsing-context-group navigation](https://github.com/whatwg/html/issues/4198) | ✔️ (91.1+) ⚠️ needs further investigation, since the [impact](https://github.com/whatwg/html/issues/5350) is unclear.
[#passwords-account-storage](chrome://flags/#passwords-account-storage) | Enable the account data storage for passwords | ❌ (88.x+)
[#brave-ads-custom-notifications](chrome://flags/#brave-ads-custom-notifications) | Enable Brave Ads custom notifications | ✔️
[#window-naming](chrome://flags/#window-naming) | Window Naming | ✔️ Setting under `More tools - Name Window`
[#brave-adblock-cname-uncloaking](chrome://flags/#brave-adblock-cname-uncloaking) | Enable CNAME uncloaking | ✔️ 91.1.27.36 (This will become obsolete and enabled by default once fully stable and merged into shields directly)
[#dns-httpssvc](chrome://flags/#dns-httpssvc) | Support for HTTPSSVC records in DNS | ✔️ (_needs further investigation_)
[#omnibox-default-typed-navigations-to-https](chrome://flags/#omnibox-default-typed-navigations-to-https) | Omnibox - Use HTTPS as the default protocol for navigations | ✔️
[#brave-first-party-ephemeral-storage](chrome://flags/#brave-first-party-ephemeral-storage) | First Party Ephemeral Storage (95.0.4638.40+) | ✔️
[#enable-unsafe-webgpu-service](chrome://flags/#enable-unsafe-webgpu-service) | Unsafe WebGPU Service | ❌
[#quiet-notification-prompts](chrome://flags/#quiet-notification-prompts) | Quieter notification permission prompts | ✔️
[#privacy-sandbox-settings](chrome://flags/#privacy-sandbox-settings) | Privacy Sandbox Settings | ✔️ (90.1+)
[#safety-check-chrome-cleaner-child](chrome://flags/#safety-check-chrome-cleaner-child) | Enables the Chrome Cleanup Tool child in safety check. | ❌ (91.x+)

[🔝 Back to top 🔝](#)

-------------------------

### [Mobile outdated, removed or integrated/replaced](#mobile-outdated-removed-or-integratedreplaced)
Flag | Name | Disabled since or comment
-- | -- | --
`#brave-sync-v2` | Enable Brave Sync v2 | Depends on user choice (opt-in) you manually can set under `Settings`.
`#global-media-controls-for-chromeos` | Global Media Controls for ChromeOS | Depends on your Platform, only avbl. in ChromeOS
`#Enable-sharing-page-via-qr-code` | Enable sharing page via QR Code | Merged into the Browser (stable).
[#enable-tls13-early-data](chrome://flags/#enable-tls13-early-data) | TLS 1.3 Early Data | ✔️
[#enable-ftp](chrome://flags/#enable-ftp) | Enable FTP | Removed from the source code
[#brave-adblock-default-1p-blocking](chrome://flags/#brave-adblock-default-1p-blocking) | Shields first-party network blocking (1.30.27+) | ✔️
[#brave-dark-mode-block](chrome://flags/#brave-dark-mode-block) | Enable dark mode blocking fingerprinting protection (1.30.27+), the settings depends now on Shield settings | ✔️
[#clear-cross-browsing-context-group-main-frame-name](chrome://flags/#clear-cross-browsing-context-group-main-frame-name) | [Clear window name in top-level cross-browsing-context-group navigation](https://github.com/whatwg/html/issues/4198) | ✔️ (91.1+) ⚠️ needs further investigation, since the [impact](https://github.com/whatwg/html/issues/5350) is unclear.
[#passwords-account-storage](chrome://flags/#passwords-account-storage) | Enable the account data storage for passwords | ❌ (88.x+)
[#brave-rewards-bitflyer](chrome://flags/#brave-rewards-bitflyer) | Enable bitFlyer for Brave Rewards (default) | Will be detected by keyboard/OS language
[#u2f-security-key-api](chrome://flags/#u2f-security-key-api) | Enable the U2F Security Key API | ❌
[#cookies-without-same-site-must-be-secure](chrome://flags/#cookies-without-same-site-must-be-secure) | N/A | ✔️
[#legacy-tls-enforced](chrome://flags/#legacy-tls-enforced) | N/A | ❌ (_might break some pages who use "outdated TLS configurations"_)
[#omnibox-default-typed-navigations-to-https](chrome://flags/#omnibox-default-typed-navigations-to-https) | N/A | ✔️
[#treat-unsafe-downloads-as-active-content](chrome://flags/#treat-unsafe-downloads-as-active-content) | N/A | ✔️
[#brave-first-party-ephemeral-storage](chrome://flags/#brave-first-party-ephemeral-storage) | First Party Ephemeral Storage (95.0.4638.40+) | ✔️
[#safe-browsing-client-side-detection-android](chrome://flags/#safe-browsing-client-side-detection-android) | Safe Browsing Client Side Detection on Android | ❌
[#omnibox-local-zero-suggest-frcency-ranking](chrome://flags/#omnibox-local-zero-suggest-frcency-ranking) | Omnibox Local Zero Suggest Frequency Ranking | ❌
[#share-by-default-in-cct](chrome://flags/#share-by-default-in-cct) | Share by Default | ❌
[#enable-accessibility-live-caption](chrome://flags/#enable-accessibility-live-caption) | Live Caption |❌ (90.x+) ⚠️[borked](https://github.com/brave/brave-browser/issues/15640)
[#system-keyboard-lock](chrome://flags/#system-keyboard-lock) | Experimental system keyboard lock | ❌ (89.x+)
[#privacy-sandbox-settings](chrome://flags/#privacy-sandbox-settings) | Privacy Sandbox Settings | ✔️ (90.1+)
[#chrome-share-highlights-android](chrome://flags/#chrome-share-highlights-android) | N/A | ❌
[#cookie-deprecation-messages](chrome://flags/#cookie-deprecation-messages) | N/A | ❌
[#enable-android-dark-search](chrome://flags/#enable-android-dark-search) | Enable Android Dark Search | ✔️
[#enable-ephemeral-tab-bottom-sheet](chrome://flags/#enable-ephemeral-tab-bottom-sheet) | Enable Ephemeral Tab Bottom Sheet | ✔️ `Open at half state`
[#quiet-notification-prompts](chrome://flags/#quiet-notification-prompts) | Quit Notification Prompts | ✔️ `adaptive activation`
[#read-later](chrome://flags/#read-later) | Read Later (Reading List) | ✔️
[#share-button-in-top-toolbar](chrome://flags/#share-button-in-top-toolbar) | Share Button in Top Toolbar | ❌
[#toolbar-iph-android](chrome://flags/#toolbar-iph-android) | Toolbar IPH in Android | ❌
[#sharing-hub-desktop-app-menu](chrome://flags/#sharing-hub-desktop-app-menu) | Desktop Sharing Hub in App Menu | ✔️ (Chrome 91+)
[#sharing-hub-desktop-omnibox](chrome://flags/#sharing-hub-desktop-omnibox) | Desktop Sharing Hub in Omnibox | ✔️ (Chrome 91+)
[#omnibox-native-voice-suggestions-provider](chrome://flags/#omnibox-native-voice-suggestions-provider) | Omnibox Native Voice Suggestions Provider | ❌

[🔝 Back to top 🔝](#)
